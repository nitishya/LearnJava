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
