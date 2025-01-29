1. Introduction
2. The ways to make an object eligible for GC.
3. The methods for requesting JVM to run GC.
4. Finalization.

**Introduction**
- In java programmer is responsible only for creation of object and programmer is not reponsible to destroy useless objects. deletion is done by garbage collector.
- Sun people provided one assistant to destroy useless objects this assistant is always running in the background(deamon thread) and destroy useless objects.
- Just because of this assistant the chance of failing java program with memory problem is very low.This assistant is nothing but Garbage Collector.
- Hence the main objective of garbage collector is to destroy useless objects.

**The ways to make an object eligible for GC:**
- We are not responsible for destruction still you feel that this object is no longer required , it is highly recommended to make that object eligible for GC.
- When object is eligible for GC, When object doesn't have reference variable.

ways to make an object eligible for GC - 4 ways 
1. Case I: Nullifying the reference variable.
          - if an object no longer required, then assign a null to all its refernece variable than that object automatically eligible for garbage collection.
   ![image](https://github.com/user-attachments/assets/26f70c80-e374-4e17-907d-a9267f876b7c)

2. Case II: Reassigning the reference variable
           - If an object no longer required than reassign its reference variable to some other object than old object by default eligible for garbage collection.
   ![image](https://github.com/user-attachments/assets/413fcf1e-2021-4fcb-acdc-6bfa8bb11cb0)

3. Case III: Objects created inside a method
            - The objects that are created inside a method are by default eligible for GC once method completes.
```
public class MethodGCDemo {

	public static void m1()   {
		MethodGCDemo s1 = new MethodGCDemo();
		MethodGCDemo s2 = new MethodGCDemo();
	}
	
	//after running method m1() the s1 and s2 are eligible for Garbage Collection.
	public static void main(String[] args) {
            m1();
	}

}
```
    - If an method returns an object, if that returned object we capture using refrence varible than that object is not eligible for GC.If we didn't capture than it is eligible for GC.
![image](https://github.com/user-attachments/assets/09fcfc32-b1b8-47db-989a-8b128b8f77a2)

![image](https://github.com/user-attachments/assets/365c2717-b7a7-4bf7-b179-f9171296f9e7)

![image](https://github.com/user-attachments/assets/bf774ae1-bb5d-4117-b65a-ffc0a9218283)

4. Case IV: Island of Isolation
![image](https://github.com/user-attachments/assets/625924ec-9471-4a04-bbad-7b961ecdedda)
      - if an object doesn't contain reference variable it is always by default eligible for GC.
      - If object contain different variable even though somethimes it is eligible for garbage collection like in Island of Isolation.

The ways for requesting JVM to run GC 
- Once  we made an object eligible for GC,it may not be destroyed immideately by GC , whenever JVM runs GC than only the object will be destroyed.but when exactly JVM runs GC it is varied from JVM to JVM instead of waiting until JVM runs GC we can request JVM to run GC programmatically but whether JVM accept our request or not there is no guarantee but most of the JVM accept our request.
  
- The following are two ways for requesting JVM to run GC
   - By using System Class:System class contains static method gc() for this purpose 
     - System.gc();
   - By using Runtime class
     - Runtime r = Runtime.getRuntime();
     - r.totalMemory()
     - r.freeMemory()
     - r.gc()

Java application can communitacate with JVM by using Runtime object.RUntime class present in java.lang package and it is a singeleton class we can create runtime object by using Runtime.getRuntime(); 
Once we got runtime object we can call the following methods on object 
- totalMemory -> it returns NUMBER of bytes present in the HEAP i.e heap size
- freeMemory -> it returns NUMBER of BYTES of free memory present in the HEAP
- gc()  -> FOr requesting JVM to run Garbage collector.
```
public class RuntimeGCDemo {

	public static void main(String[] args) {
		Runtime r = Runtime.getRuntime();
		System.out.println(r.totalMemory());
		System.out.println(r.freeMemory());
		for(int i=1;i<=10000;i++) {
			Date d = new Date();
		        d = null;

		}
		System.out.println(r.freeMemory());
		r.gc();
		System.out.println(r.freeMemory());
	}
}
```
which of the following is appropriate method to call GC?
1. System.gc()✔️
2. Runtime.gc()❌
3. (new Runtime()).gc()❌
4. Runtime getRuntime().gc()✔️

**Note-GC method present in System class is a static method whereas GC method present in Runtime class is Instance method**
- Recommended method = Runtime.gc() why System class contains runtime internally.
```
class System{
  public static void gc() {
     Runtime.getRuntime().gc();
     }
   }  
 ```
So if we call runtime.gc we can skip one method in hirarchy which will reduce time. and performance will be improved.

**Finalization**
- protected void finalize() throws Throwable  ->it is present in Object class so we can override finalize() method in our class to define our own cleanup activities.
- Just before destroying an object GC calls finalize method to perform cleanup activities.once finalize method completes automatically GC destroyes that object.

1. Case I: 
```
public class FinalizeDemo {

	public static void main(String[] args) {
		String s = new String("nitish");
		s = null;  //GC calls finalize method on String class
		System.gc();
		System.out.println("End of Main");//output - End of Main

	}
	//this finalize method is not called.
	public void finalize() {
		System.out.println("Finalize method called");
	}
}
```
- Just before destroying a object grabage collector calls finalize method on the object which is eligible for GC than corresponding finalize method class will be executed.
- If String class object is eligible for GC than String class finalize class will be executed but not FinalizeDemo class finalize method.
- Based on our requirement we can call finalize method explicitly than it will be executed just like a normal method call and object wont be destroyed

```
public class FinalizeDemo {

	public static void main(String[] args) {
		FinalizeDemo f = new FinalizeDemo();
		f.finalize();
		f.finalize();
		f= null;
		System.gc();
		System.out.println("end of main");
	}
	//this finalize method is not called.
	public void finalize() {
		System.out.println("Finalize method called");
	}
}

/*output
Finalize method called
end of main
Finalize method called*/
```
```
public class FinalizeDemoGC {
	static FinalizeDemoGC s;

	public static void main(String[] args) throws InterruptedException {
		FinalizeDemoGC f = new FinalizeDemoGC();
		System.out.println(f.hashCode());
		f=null;
		System.gc();
		Thread.sleep(5000);
		System.out.println(s.hashCode());
		s= null;
		System.gc();
		Thread.sleep(10000);
		System.out.println("End of main");

	}
	
	public void finalize() {
		System.out.println("Finalize method called");
		s = this;
	}

}
```

- Even though  object eligible for GC but GC calls finalize method only once.

**Call GC by ourself**
```
public class CallGCbySelf {
	static int count=0;
	public static void main(String[] args) {
	for(int i=0;i<1000000;i++) {
		CallGCbySelf t = new CallGCbySelf();
		t = null;
	}
	}
	public void finalize() {
	    System.out.println("Finalize method called" + ++count);
	}	
 }
```
- Start from 100 and keep increasing the value of i until GC called to destroy the object.
- We cant expect exact behaviour of GC it is varied from JVM to JVM hence we cant provide exact answer
    - When exactly JVM run GC
    - in which order GC destroys eligible objects
    - whether GC destroys all eligible object or not
    - what is algorithm followed by GC.

**Note**
- Whenever program runs with low memory than JVM runs GC but we can't expect exactly at what time.
- Most of the GC follows standard algorithm - MARK AND SWEEP ALGORITHM , it doesnt mean every GC follow the same algorithm.

**Memory Leaks**
- The objects which we are not using in our program and which are not eligible for GC such type of useless objects are called memory leaks
- In our program if memory leaks present than program will be terminated by out of memory error
- Hence if a object no longer required than it is highly recommeded to make that object eligible for GC.
- There are some third party tools to find memory leaks-
   - HP OVO
   - HP J METER
   - JPROBE
   - Patrol
   - IBM Tivoli
