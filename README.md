# Threads-and-Multithreading-Lab
Laboratory activity on Python threads

### Task 1 – Creating and Executing a Single Thread

1. **What is the purpose of `threading.Thread()`?**
   It creates a new thread object and assigns a target function (`display_numbers`) that will be executed in a separate thread of control.

2. **What happens when `start()` is executed?**
   It begins the thread's execution by scheduling it with the operating system and invoking the `run()` method, which executes the assigned target function concurrently with the main thread.

3. **What is the purpose of `join()`?**
   It blocks the calling thread (in this case, the main program) and forces it to wait until the target thread (`t1`) has completely finished executing before moving on to the next line of code.

4. **What happens if `join()` is removed?**
   The main program will not wait for `t1` to finish. It will immediately execute `print("Program completed.")` right after starting the thread, while `display_numbers()` continues printing numbers in the background.

