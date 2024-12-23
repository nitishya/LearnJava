**MultiThreading -**

- The ways to define a thread?
  1. By Extending Thread Class.
  2. By Implementing Runnable(I).

- Getting and Setting name of the thread.
- Thread Priorities
- The Methods to prevent Thread execution.
   1. Yield()
   2. join()
   3. sleep()
  
- Synchronisation
- InterThread Communication
- DeadLock
- Deamon Threads
- Multithreading enhancement


**What is multitasking?**
Executing multiple task simulteneously .
   1. Process Based - Executing several Task simultaneously where each task seperate independent program.   Example: while typing a java program in the system we can listen to the audio song in the music application from the same system at the same time we can download a file from Internet using browser , all these task will be executed simultaneously and independent of each other.Hence it is process based multi tasking.
   2. Thread Based - Executing several task simultaneously where each task is separate independent part of a same program and each independent part is called thread.


whether it is process based or thread based the main objective of multitasking is to reduce response time of the system and to improve performance.

The main important application areas of multi threading are 
- To develop multimedia graphics
- To develop animations
- To develop video games
- To develop web servers and application servers

When compared with old languages developing multithreaded application in java is very easy beacause java provides inbuild support for multithreading with rich api(Thread, Runnable, Thread Group...).

**What is Thread?**
A seperate flow of execution.
for every flow of execution there is some job 

We can define a thread in the following two ways
- By extending thread class
- By implementing runnable interface

1) By Extending thread class->
  ```
package multiThreading;

class MyThread extends Thread{
	public void run() {    
		
		for(int i=0;i<10;i++) {
			System.out.println("child method");//executed by child class
		}	
	}              //job of thread	
}

public class ThreadDemo {
	public static void main(String[] args) {
		MyThread t = new MyThread();   //thread instantiation
		 t.start();  //starting of thread
		 
		 for(int i=0;i<10;i++) {
			 System.out.println("main method");
		 }
	}
}
```
Case 1. Thread Schedular : It is the part of JVM . It is responsible to schedule threads i.e. if multiple threads are waiting to get a chance of execution then in which order threads will be executed is decided by thread schedular.We can't expect exact algorithm from thread schedular it is varied from JVM to JVM hence we can't expect thread execution order and the output.
Hence whenever situation comes to multithreading there is no guarantee for exact output but we can provide several possible outputs.

Case 2. In the case of t.start() a new thread will be created which is responsible for the execution of run() method but 
In the case t.run() a new thread wont be created and run method will be executed just like a normal method call by main thread hence in the above program if we replace t.start() with t.run() than the output is child thread..10 main thead ...10 this total output produced by only main thread.

Case 3. Importance of Thread Class Start()
Thread class start() is responsible to register the thread with thread schedular and all other mandatory activities.Hence without executing thread class start() method there is no chance of starting a new thread in java due to this thread class start method is considered as Heart of multithreading
```
start(){
      1. Register this thread with the Thread Schedular 
      2. Perform all other mandatory activities
      3. Invoke run();
	}

```

   
