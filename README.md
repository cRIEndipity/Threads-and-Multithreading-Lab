# Threads and Multithreading Laboratory

## Student Information
- **Name:** Longcob, Sherie Q.
- **Section:** B186.1
- **Date:** November 23, 2026

## Laboratory Description
This laboratory demonstrates thread creation, multithreading, thread coordination, and shared-resource management using Python.

## Completed Tasks
1. Single Thread
2. Multiple Threads
3. Thread Synchronization using join()
4. Shared Resource Management using Lock()

## Learning Outcomes
- Create and execute threads.
- Demonstrate concurrent execution.
- Explain thread coordination.
- Apply locks to protect shared resources.

---

## Laboratory Questions and Answers

### Task 1 – Creating and Executing a Single Thread

1. **What is the purpose of `threading.Thread()`?**
   It creates a new thread object and assigns a target function (`display_numbers`) that will be executed in a separate thread of control.

2. **What happens when `start()` is executed?**
   It begins the thread's execution by scheduling it with the operating system and invoking the `run()` method, which executes the assigned target function concurrently with the main thread.

3. **What is the purpose of `join()`?**
   It blocks the calling thread (in this case, the main program) and forces it to wait until the target thread (`t1`) has completely finished executing before moving on to the next line of code.

4. **What happens if `join()` is removed?**
   The main program will not wait for `t1` to finish. It will immediately execute `print("Program completed.")` right after starting the thread, while `display_numbers()` continues printing numbers in the background.

---

### Task 2 – Implementing Multiple Threads

1. **How many threads are created in the program?**
   Two worker threads (`t1` and `t2`) are explicitly created using `threading.Thread()`, running alongside the main program thread (making three threads in total).

2. **Do the two threads execute independently?**
   Yes. Once started with `start()`, both `t1` and `t2` run independently and concurrently without waiting for each other's iterations to finish.

3. **Why might the output order change when the program is executed again?**
   Because the operating system's thread scheduler controls when each thread gets CPU time and switches between them unpredictably, causing the print statements from `Thread 1` and `Thread 2` to interleave differently across runs.

4. **What is the difference between sequential and concurrent execution?**
   - **Sequential execution** runs tasks one after another in a strict order—a second task cannot begin until the first task completely finishes.
   - **Concurrent execution** allows multiple tasks to make progress during overlapping time periods by switching between them (or running them simultaneously on multiple CPU cores), improving efficiency and responsiveness.

---

### Task 3 – Thread Synchronization Using `join()`

1. **Why does the main program wait when `join()` is used?**
   `t1.join()` pauses the execution of the `main()` thread until the `download_file` thread (`t1`) terminates, ensuring that dependent code (`"Main program continues."`) only runs after the download finishes.

2. **What happens when `join()` is removed?**
   The main program does not wait for `t1` to complete its 3-second sleep. It immediately prints `"Main program continues."` right after `"Main program is waiting..."`, while the background thread finishes printing `"Download completed."` 3 seconds later.

3. **In what situations is thread synchronization necessary?**
   Synchronization is necessary whenever one thread depends on the result or completion of another thread before proceeding, or when multiple threads read and write to shared variables, files, or hardware resources at the same time.

---

### Task 4 – Managing Shared Resources Using Thread Locks

1. **What is a shared resource?**
   A shared resource is any variable, data structure, memory space, or file (such as the global `counter` variable) that can be accessed and modified by multiple threads concurrently.

2. **What is a race condition?**
   A race condition occurs when two or more threads access and modify a shared resource simultaneously without proper synchronization, causing the final outcome to depend on the unpredictable timing of thread execution (often resulting in lost updates or corrupted data).

3. **What is the purpose of `threading.Lock()`?**
   `threading.Lock()` provides a mutual exclusion mechanism (mutex) that allows only one thread at a time to acquire the lock and access a protected block of code, forcing other threads to wait until the lock is released.

4. **What is a critical section?**
   A critical section is the specific segment of code where a thread accesses or modifies a shared resource (in this program, the `counter += 1` operation inside the `with lock:` block).

5. **Why is synchronization important when multiple threads access shared data?**
   Synchronization ensures data integrity and consistency by preventing race conditions, guaranteeing that operations on shared data complete atomically without interference from other threads.

---

## VII. General Review Questions

1. **What is the difference between a process and a thread?**
   A **process** is an independent program in execution with its own dedicated memory space, resources, and process control block (PCB). A **thread** is the smallest unit of execution within a process; multiple threads within the same process share the same code, data, and heap memory while maintaining their own execution stack and registers.

2. **What are the advantages of using multithreading?**
   - **Responsiveness:** Keeps applications interactive even when performing lengthy operations.
   - **Resource Sharing:** Threads share the memory and resources of their parent process naturally, making communication faster than inter-process communication (IPC).
   - **Economy:** Creating and context-switching threads requires significantly less overhead and memory than creating separate processes.
   - **Scalability:** Allows programs to take full advantage of multi-core processors by running threads across multiple CPU cores.

3. **How does multithreading improve application responsiveness?**
   Multithreading separates time-consuming background tasks (such as file downloads, database queries, or heavy computations) from the main user interface (UI) thread. While a worker thread handles the blocking operation in the background, the main thread remains free to respond immediately to user input.

4. **What is the difference between concurrency and parallelism?**
   - **Concurrency** is about *dealing with* multiple tasks at once by interleaving their execution over overlapping time periods (even on a single CPU core).
   - **Parallelism** is about *doing* multiple tasks at the exact same instant across multiple CPU cores or processors.

5. **Why is a lock necessary when multiple threads access shared data?**
   A lock ensures mutual exclusion so that only one thread can read or modify the shared data at a time. Without a lock, threads can overlap during read-modify-write operations, overwriting each other's changes and producing incorrect results.

6. **What might happen if a thread is not properly synchronized?**
   Lack of proper synchronization can lead to **race conditions**, **data corruption**, **lost updates** (inconsistent shared state), or unpredictable execution order where dependent operations run before required tasks finish.

7. **Can multiple threads execute simultaneously on a single-core processor? Explain.**
   **No**, not at the exact same instant. A single-core processor can execute only one thread instruction at a given moment. Instead, it achieves **concurrency** through rapid time-slicing (context switching)—switching between threads so quickly that they appear to run simultaneously.

8. **How does the operating system manage kernel-level threads?**
   The operating system kernel creates, schedules, and manages kernel-level threads directly in kernel space using thread control blocks (TCBs) and a kernel scheduler. The OS allocates CPU time slices to each thread, performs context switches when threads block or yield, and can distribute multiple kernel threads across separate CPU cores for true parallel execution.