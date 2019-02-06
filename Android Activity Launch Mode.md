

### Android Activity Launch Mode

Launch mode is an instruction for Android OS which specifies how the activity should be launched. It instructs how any new activity should be associated with the current task and Back Stack.

> Tasks : A task is a collection of activities that users interact with
> 
> Back Stack : Activities are arranged with the order in which each activity is opened. This maintained stack called Back Stack.

There are four launch modes for activity.They are:
1. Standard
2. SingleTop
3. SingleTask
4. SingleInstance

> In the AndroidManifest you can use “launchMode” attribute inside the <activity> element to declare the activity’s launch mode like

    <activity android:launchMode = [“standard” | “singleTop” | “singleTask” | “singleInstance”] />

***Standard*** : This is the default launch mode of an activity. It creates a new instance of an activity in the task from which it was started. You can create the same activity multiple times in the same task as well as in different tasks. `<activity android:launchMode=”standard”/>`

    A -> B -> C -> D
    Activity B launched with launchMode=”standard”
    A -> B -> C -> D -> B

***SingleTop*** : If an instance of activity already exists at the top of the current task, a new instance will not be created and android system will pass the intent information through onNewIntent(). If an instance is not present on top of task then new instance will be created. In this launch mode you can create multiple instance of the same activity in the same task or in different tasks only if the same instance does not already exist at the top of stack. `<activity android:launchMode=”singleTop”/>`

    A -> B -> C
    Activity D launched with launchMode=”singleTop”
    A -> B -> C -> D (Here D launch as usual)
___
    A -> B -> C -> D (D launched with launchMode=”singleTop”)
    Activity D again launched with launchMode=”singleTop”
    A -> B -> C -> D (Here old instance gets called and intent data route through onNewIntent() callback)  

***SingleTask*** : If there is no singleTask Activity instance existed in the system yet, new one would be created and simply placed on top of stack in the same Task. But if there is an existed one, all of activities placed above that singleTask activity would be automatically and cruelly destroyed in the proper way to make our activity to appear on top of stack and Android system will route the intent information through onNewIntent(). `<activity android:launchMode=”singleTask”/>`

    A -> B -> C
    Activity D launched with launchMode=”singleTask”
    A -> B -> C -> D (Here D launch as usual)
___
    A -> B -> C -> D (B launched with launchMode=”singleTask”)
    Activity B again launched with launchMode=”singleTask”
    A -> B (Here old instance gets called and intent data route through onNewIntent() callback)
    
***SingleInstance*** : This is very special launch mode and only used in the applications that has only one activity. It is similar to singleTask except that no other activities will be created in the same task. Any other activity started from here will create in a new task. `<activity android:launchMode=”singleInstance”/>`


    A -> B -> C
    Activity D launched with launchMode=”singleInstance”
    Task1 : A -> B -> C
    Task2 : D (here D will be in different task)

___

    Task1 : A -> B -> C
    Task2 : D
    Activity D launched with launchMode=”singleInstance”
    Task1 : A -> B -> C
    Task2 : D (Here old instance gets called and intent data route through onNewIntent() callback)


### Intent Flags
Android also provides Activity flags by which you can change the default behavior of Activity association with Tasks while starting it via startActivity() method. These flags values can be pass through Intent extra data.

**FLAG_ACTIVITY_NEW_TASK** : This flag works similar to “launchMode = singleTask”.

**FLAG_ACTIVITY_CLEAR_TASK** : Any existing task that would be associated with the activity to be cleared before the activity is started.

**FLAG_ACTIVITY_CLEAR_TOP** : The activity being launched is already running in the current task, then instead of launching a new instance of that activity, all of the other activities on top of it will be closed and Intent will be delivered to the as a new Intent.

**FLAG_ACTIVITY_SINGLE_TOP** : This flag works similar to “launchMode = singleTop”.


### Thread 
A thread, in the context of Java, is the path followed when executing a program. All Java programs have at least one thread, known as the main thread, which is created by the Java Virtual Machine (JVM) at the program's start, when the main() method is invoked with the main thread.

We use Threads to make Java application faster by doing multiple things at same time. Thread helps you to achieve parallelism in Java program. Since CPU is very fast and even contains multiple cores, just one thread is not able to take advantage of all the cores. By using multiple threads, you can take full advantage of multiple cores by serving more clients and serving them faster. Multi-threading is one way to exploiting huge computing power of CPU in Java application. Thread is also using for doing multiple tasks simultaneously. If you have lot of tasks to be done and If you are doing all this task in one thread, they would be executed sequentially. By using multiple threads in Java you can execute each of this task independently and parallelly. 

### Multithreading
Multithreading in java is a process of executing multiple threads simultaneously. Java application contains at least one thread, that is called main thread which executes your main method. Instead of that you can also add new user threads to make your application faster and more efficient and it's called as multi-threading. The following are the reasons and scenarios to use multiple threads in Java. Multithreading is mostly used in games, animation, etc.

> Multiprocessing and multi-threading, both are used to achieve
> multitasking. However, we use multi-threading than multiprocessing
> because threads use a shared memory area. They don't allocate separate
> memory area so saves memory, and context-switching between the threads
> takes less time than process. 

 - To make a task run parallel to another task : By Using multi-threading we can execute multiple task at a time parallelly.
 - To take full advantage of CPU power : Another common reason for using multiple threads in Java is to improve throughput of the application by utilizing full CPU power.
 - For reducing response time : You can also use multiple threads to reduce response time by doing fast computation by dividing a big problem into smaller chunks and processing them by using multiple threads.
 - To sever multiple clients at the same time : One of the most common scenarios where using multiple threads significantly improve an application's performance is a client-server application. A single threaded application means only one client can connect to the server at a time, but a multi-threaded server means multiple clients can connect to the server at same time. This means next client don't have to wait until your application finish processing request of the previous client.

### Multiprocessing
A multiprocessing system is one which has more than two processors. The CPUs are added to the system to increase the computing speed of the system. Each CPU has its own set of registers and main memory. Just because CPUs are separate, it may happen that one CPU may not have anything to process and sit idle and the other may be overloaded with the processes. In such cases, the processes and the resources are shared dynamically among the processors.

Multiprocessing can be classified as **symmetric multiprocessing** and **asymmetric multiprocessing**. In symmetric multiprocessing, all processors are free to run any process in a system. In Asymmetric multiprocessing, there is a master-slave relationship among the processors. The master processor is responsible for allotting the process to slave processors.
