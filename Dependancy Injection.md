## Dependency Injection
In object-oriented programming (OOP) software design, dependency injection (DI) is the process of supplying a resource that a given piece of code requires. The required resource, which is often a component of the application itself, is called a dependency.

Consider the following Java class.

    public  class  User{    
	    private  Database mDatabase;    
	    public  User(){	    
		    mDatabase  =  new  Database();	    
	    }    
    }
In the above class, we are creating the object of class **Database** inside the constructor of class **User**. So here, we can say that; the User is dependent on Database. So here, **Database** is a dependency for the class **User**.

It is indeed a bad idea. We should keep the classes as independent from other classes. It has the following advantages:
 - If the classes are independent, you can reuse them.
 - For unit test each class, it is necessary that the classes are
   independent of each other.

Instead of using new to instantiate the Database inside User’s constructor we can pas the Database as an argument to the User’s constructor.

    public class User{
	    private Database mDatabase;
	    public User(Database mDatabase){
		    this.mDatabase = mDatabase;
	    }
    }
So this is what we call as **Dependency Injection**. Means supplying the dependencies from outside the class. And more specifically for the above code, we can consider it as a *Constructor Injection*.

