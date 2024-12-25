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
Case 4.Overloading of run() method 
Overloading of run() method is always possible but thread class start() can invoke no argument run() method the other overloaded method we have call explicityly like a normal method call.
```
package multiThreading;

class MyThread extends Thread{
	public void run() {    
		System.out.println("No argument run method");
	}              //job of thread	
	
	public void run(int n) {    
		System.out.println("No argument run method");
	}              //job of thread		
}

public class ThreadDemo {
	public static void main(String[] args) {
		MyThread t = new MyThread();   //thread instantiation
		 t.run();  //starting of thread		
	}  //output : No argument run method
}
```
Case 5.If we are not overriding run() method than thread class run() method will be executed which has empty implementation. Hence we wont get any output.

 **Note : It is highly recommended to override run() method otherwise dont go for overriding concept**

Case 6. Override Start()
If we override start() method than our start method will be executed just like a normal method call and new thread wont be created.

**Note :It is recommended to not override start() method otherwise dont go for multithreading concept **
```
package multiThreading;

class MyThread extends Thread{
	
	
	public void start() {
		super.start();	
		System.out.println("start method");
	}
	
	public void run() {    
		
		for(int i=0;i<10;i++) {
			System.out.println("child method");//executed by child class
		}	
	}              //job of thread		
}

public class ThreadDemo {
	public static void main(String[] args) {
		MyThread t = new MyThread();   //thread instantiation
		 t.run();  //starting of thread
		 
		 for(int i=0;i<10;i++) {
			 System.out.println("main method");
		 }
	}
}
```
Case 7. 
![image](https://github.com/user-attachments/assets/c0ff2298-0069-4979-9ed9-1639c6070491)


Case 8. IllegalThreadStateException
After starting a thread if we try to restart the same thraead once again that it will get runtime exception saying illegalThreadStateException
```
package multiThreading;

public class ThreadStateExceptionDemo {

	public static void main(String[] args) {
		MyThread t = new MyThread();
		t.start();
		System.out.println("main method");
		t.start();   //java.lang.IllegalThreadStateException
	}
}
```


**Defining a thread by Implementing runnable(I):**
![image](https://github.com/user-attachments/assets/37c8ada1-fb3d-46ba-ad0c-1d6b67f89197)

Runnable interface present in java.lang package and it contains only one method run().
```
package multiThreading;

class myRunnable implements Runnable{
	 public void run() {
		 for(int i=0;i<10;i++) {
			 System.out.println("Child Thread");
		 }
	 }
}

public class RunnableThreadDemo {

	public static void main(String[] args) {
		 myRunnable r = new myRunnable();
                 Thread t1 = new Thread();
		 Thread t2 = new Thread(r); //target runnable
		 t2.start();
	}
}
```
Case 1: t1.start();  - A new thread will be created and which is responsible for the execution of thread class run method which has empty implementaion.
Case 2: t1.run();    - No new thread will be created and thread class run() method will be executed just like a normal method call.
Case 3: t2.strart();   - A new thread will be created which is responsible for the execution of myRunnable class run().
Case 4: t2.run();   - A new thread wont be created and myRUnnable run() will be executed just like a normal method call.
Case 5: r.start();   -we will get compile time error saying myRunnable class doesnt have start capability.
case 6: r.run();    -No new thread will be created and myRunnable run() will be executed like normal method call. 


**Amoung two ways which one is best**
recommended - myRunnable implements Runnable
Reason - we will miss inheritance benefit in 1st approach as only one class is already extended.
but in the second approach while implementing runnable interface we can extend any other class.Hence we wont miss any inheritance benefit.


**Thread class Constructors**
1. Thread t = new Thread();
2. Thread t = new Thread(Runnable r);
3. Thread t = new Thread(String name);
4. Thread t = new Thread(Runnable r, String name);
5. Thread t = new Thread(ThreadGroup g, String name);
6. Thread t = new Thread(ThreadGroup g, Runnable r);
7. Thread t = new Thread(ThreadGroup g,Runnable r,String name);
8. Thread t = new Thread(ThreadGroup g,Runnable r,String name,long StackSize);

Approach to define a thread (Not recommended):
```
package multiThreading;

class myThread extends Thread{
	public void run() {
		System.out.println("Child thread");
	}
}

public class MyOwnImpleementationDemo {
	public static void main(String[] args) {
		myThread t = new myThread();
		Thread t1 = new Thread(t);
		t1.start();
		System.out.println("Main Thread");
                System.out.println(t.currentThread().getName());
                 t.currentThread().setName("Pawan Kalan");
		System.out.println(t.currentThread().getName());
                    
	}
}

```
**To know the current executing thread : Thread.currentThread().getName()**

Every thread in java has some name it may be default name generated by JVM or customised name provided by programmer

We can get and set name of a thread by using the following two methods of thread class 
public final String getName()
public final void setName(String name)
```
class MyThread extends Thread {
}
class Test {
public static void main(String[] args){
                 System.out.println(t.currentThread().getName());
                 MyThread t = new MyThread();
                 t.currentThread().setName("Pawan Kalan");
                 System.out.println(t.currentThread().getName());
  }
}
```


**Thread Priority**

Priority : 0 - 10

Every Thread in java has some priority it may be default priority generated by JVM or customised priority provided by programmer.THe valid range of thread priority is 1-10 where 1 is min priority and 10 is max priority.
Thread class defines these to reperesent some standard priorities.

- Thread.MIN_PRIORITY=1
- Thread.NORM_PRIORITY=5
- Thread.MAX_PRIORITY=10

If two thread have same priority than we cant expect exact execution order it depends on thread schedular.

Thread class defines the following method to get and set priority of a thread 
- public final int getPriority()
- public final void setPriority(int P)
- allowed values range 1-10 otherwise IllegalArgumentException. Ex-t.setPriority(17);
