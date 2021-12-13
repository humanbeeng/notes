## Coroutines	
 
> Coroutines are light weight tasks that an actual thread can execute. Coroutines are not in itself a thread and does not create a new thread when launched. They are executed within a Thread. They use a predefined thread pools and smart scheduling algorithms to decide which coroutine to execute next.


A coroutine is not bound by any particular thread. In fact it can **suspend** its execution in one thread and resume in another one.

----------

**Thread** : A thread is a single sequential flow of control within a program.
**Thread and Process** : A process, in the simplest terms, is an executing program. One or more threads run in the context of the process. A thread is the basic unit to which the operating system allocates processor time.


launch -> Coroutine builder. It launches a new coroutine concurrently with the rest of the code, which continues to work independently.