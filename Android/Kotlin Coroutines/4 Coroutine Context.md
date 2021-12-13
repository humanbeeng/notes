## Coroutine Contexts and Coroutine Scopes


> Coroutine Context is a set of elements which are 1. Job Object 2. Dispatcher 3. Coroutine name

Job Object are created through launch function. launch function return a type **Job** object

```java
val jobObject = scope.launch{}
// type of jobObject is Job

```

All coroutines must run in a scope. A CoroutineScope manages one or more related Coroutines

launch is used to create a coroutine and dispatches the execution of its function body to the corresponding dispatcher.



Types of dispatchers : 

Coroutines can be launched from IO, Main, Default(Complex and long running operations), Unconfined -> Not confined to any 

Dispatchers.IO indicates that coroutine should be executed in threads reserved for IO operations. These threads are optimized for its purpose.

> Note : Sleeping threads are not dead. 

----------


### Scopes

There are already predefined scopes such as GlobalScope, ViewModelScope

> Coroutine scopes are a way to keep track of all the Coroutines inside it. 

Coroutines scopes takes in CoroutineContext() as parameter. Context is made up of Job, Dispatcher and Name of the Coroutine -> CoroutineName

Coroutine Scope formalizes the way which Contexts are inherited (ie, from Parent to Children).

Example : When we create a new Coroutine scope(say, child scope) and launch a new Coroutine inside this child scope, the child scope inherits the context of parent. The Parent coroutine waits for all of its children coroutine to complete. When parent coroutine is cancelled, all of its children coroutines are cancelled as well.