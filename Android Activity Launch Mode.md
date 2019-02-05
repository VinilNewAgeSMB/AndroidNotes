## Android Activity Launch Mode

Launch mode is an instruction for Android OS which specifies how the activity should be launched. It instructs how any new activity should be associated with the current task and Back Stack.
> **Tasks** : A task is a collection of activities that users interact with
> **Back Stack** : Activities are arranged with the order in which each activity is opened. This maintained stack called Back Stack.

There are four launch modes for activity.They are:
1. Standard
2. SingleTop
3. SingleTask
4. SingleInstance

> In the AndroidManifest you can use “launchMode” attribute inside the <activity> element to declare the activity’s launch mode like

    <activity android:launchMode = [“standard” | “singleTop” | “singleTask” | “singleInstance”] />

***Standard*** : This is the default launch mode of an activity. It creates a new instance of an activity in the task from which it was started. You can create the same activity multiple times in the same task as well as in different tasks.

> Activity Stack before : A -> B -> C -> D
> Launching activity B with launchMode=”standard”
> Activity Stack after : A -> B -> C -> D -> B

    <activity android:launchMode=”standard”/>

***SingleTop*** : If an instance of activity already exists at the top of the current task, a new instance will not be created and android system will pass the intent information through onNewIntent(). If an instance is not present on top of task then new instance will be created. In this launch mode you can create multiple instance of the same activity in the same task or in different tasks only if the same instance does not already exist at the top of stack.

> Activity Stack before : A -> B -> C
> Launching activity D with launchMode=”singleTop”
> Activity Stack after : A -> B -> C -> D (Here D launch as usual)

> Activity Stack before : A -> B -> C -> D
> Launching activity D with launchMode=”singleTop”
> A -> B -> C -> D (Here old instance gets called and intent data route through onNewIntent() callback)

    <activity android:launchMode=”singleTop”/>

***SingleTask*** : If there is no singleTask Activity instance existed in the system yet, new one would be created and simply placed on top of stack in the same Task. But if there is an existed one, all of activities placed above that singleTask activity would be automatically and cruelly destroyed in the proper way to make our activity to appear on top of stack and Android system will route the intent information through onNewIntent().

> Activity Stack before : A -> B -> C
> Launching activity D with launchMode=”singleTask” 
> Activity Stack after : A -> B -> C -> D (Here D launch as usual)

> Activity Stack before : A -> B -> C -> D
> Launching activity B with launchMode=”singleTask” 
> Activity Stack after : A -> B (Here old instance gets called and intent data route through onNewIntent() callback)

    <activity android:launchMode=”singleTask”/>
***SingleInstance*** : This is very special launch mode and only used in the applications that has only one activity. It is similar to singleTask except that no other activities will be created in the same task. Any other activity started from here will create in a new task. 

    <activity android:launchMode=”singleInstance”/>
