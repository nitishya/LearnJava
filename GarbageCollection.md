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
