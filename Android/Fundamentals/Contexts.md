# Contexts

Contexts refers to the context of what we are talking about and **where we are currently present**

Contexts could be : 
- Current state of the application
- Information regarding the application/activity
- Used to get access to database, resources and shared preferences

----

### Types of Contexts
1. Application Context : It is the application itself. Our application (ex MyApplication) which could have extended Application class, ApplicationContext will refer to the instance ie, MyApplication but not Application class. 
2. Activity Context : It is the activity itself. 


### Application Context 
Application Context refers to the our application. This instance of Application class ie our MyApplication is a singleton and can be accessed in activity via getApplicationContext(). This context is linked to the **lifecycle of application** itself.

Usage : Very useful when we need to initialize a library for the entire app itself (example : Room library) it's crucial to pass in the Application Context instead of Activity context and this makes sense because the Room database is serving for the entire application itself rather than for a specific activity. If we had passed in ActivityContext to the Room DB init, we wont get any errors, rather, we would have a memory leak when the activity gets destroyed since our RoomDB holds reference to the activity and hence the memory will not get Garbage Collected.

### Activity Context
This context refers to the activity and is tied to the lifecycle to the activity itself. 

Usage : If we want to show specific UI related stuff, Ex : Snackbar, Toast, Dialogs -> Use the ActivityContext().

> When we are declaring a singleton object for the entire application's use -> use **ApplicationContext**. By now its kinda obvious why so.

