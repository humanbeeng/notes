# Contexts

Contexts refers to the context of what we are talking about and **where we are currently present**

Contexts could be : 
- Current state of the application
- Information regarding the application/activity
- Used to get access to database, resources and shared preferences


### Types of Contexts
1. Application Context : It is the application itself. Our application (ex MyApplication) which could have extended Application class, ApplicationContext will refer to the instance ie, MyApplication but not Application class. 
2. Activity Context : It is the activity itself. 


### Application Context 
Application Context refers to the our application. This instance of Application class ie our MyApplication is a singleton and can be accessed in activity via getApplicationContext(). 