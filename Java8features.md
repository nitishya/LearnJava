1) Lambda  Expresions 
2) Functional Interfaces 
3) Default methods in Interfaces 
4) Static methods in Interfaces
5) Predicate }
6) Function  }---- predefined function in functional  interfaces 
7) Consumer  }
8) Method references and Constructor refernces By doublel colon (::) operator 
9) Stream Api 
10) Date and Time APi (Joda API )



---------------------------------------------------------------------------------------------------------------
why java 8 - to simplify the way of writing code. more clean code , more maintainable code 
           -> To utilize functional programmming 
           -> To enable parallel programming 



----------------------------------------------------------------------------------------------------------------

what is Lambda expression - lambda expression is annonymous function.

Lambda Expressions -> anonymous function ,nameless function
                   -> points to remember - not having name 
                                         - not having modifiers 
                                         - not having return type

   public❌ void❌ m1❌(){                      |
     System.out.println("Hello");                |   --   ()->{ System.out.println("Hello");}
   }                                             |

it is very easy ...if you know java method.

	public❌ void❌ add❌(int a,int b) {             |
		System.out.println(a+b);                        |-   (int a, int b) ->{System.out.println(a+b);};
	}                                                  |    based on situation compiler can guess the output type k/a Type Inference
                                                      |    (a,b)->System.out.println(a+b);

   public❌ int❌ getLength❌(String s){             |
      return s.length();                              |    ---> (String s) -> {return s.length();}
   }                                                  |         (s)->return s.length()  
                                                      |         (s)->s.length()
                                                      |          s->s.length()


why Lambda expression -> To enable functional programming in java 
                      -> Write more readable , maintainable and consize code 
                      ->To use APIs very easily and effectively.
                      ->To enable parallel processing.


public void m(){                |
 sys("Hello");                  |    ->  ()-> {sys("hello")} ;   => () -> sys("hello");
}                               |        if only one statement is there we can skip curly braces.
             

Characterstics/properties of lambda expression-
1.A lambda expression can  take any number of parameters.
2.If multiple parameters present then these parameters should be seperated with ,
3.If only one parameter available then parameter are optional.
4.Usually we specify the type of parameter if compiler expect the type based on content, then we can remove type [k/a Type Inference]
5.Similar to method body, Lambda expression body can contain any number of any muber of statements.If multiple statements are there then we should enclose with curly braces.
6.If body contains only one statement then curly braces are optional.



-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Functional Interface -> To invoke the lambda function we require functional Interface.
                     -> If the interface contain only one abstract method then that interface is called Fuctional Interface.

example - Runnable   -> contains only one method run().
        - Callable   -> conatins only one method call().
        - ActionListener -> contains only  one method actionPerformed().
        - Comparable  -> contains only one method compareTo() 

Rule if applicable only for abstract methods. How Many abstract methods - only one.
How many default methods can we take - any number of default methods.
How many static methods can we take - any number of static methods.


@FunctionalInterface ->To indicate the compiler that this will be functional interface by mistake if two abstract method creates than it will show Compile Time Error.
```
        @FunctionalInterface
	interface Interf{
		public void m1();
		
		default void m2() {
			
		}
		
		public static void m3() {
			
		}
		
	}
l
```

------Functional Interface with respect to inheritance -----

Case 1) IF an interface extends functional Interference and the child Interface does not contain any abstract method , then child interface is always functional interface.

Case 2) In the child Interface we can define exactly same parent interface abstract method .

Case 3) In the child interface we cant define any new abstract method if it is annotated as @functional Interface otherwise it will get Compilation Error.

Case 4) In the child interface we can define any new abstract method it is valid.



Implementation -- 

1) without Lmabda expression 

interface Interf{
public void m1();
}

class Demo implements Interf
{
 public void m1()
{    sys( m1() method implementation)
}
}

class Test {
 public static void main(String() args)
{
    Interf i = new Demo();
    i.m1();
}
}

-------------------------EXECUTED CODE -------------------------------
```
package collect;
interface Interf{
	public void m1();
}

public class LambdaDemo implements Interf {

		public void m1() {
			System.out.println("M1() method implemented");
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Interf i = new LambdaDemo();
		i.m1();	
	}
}
```

--------------------------------------------------------------------------------------
2) with lamda expression
```   
interface Interf{
public void m1();
}

class Test {
 public void main (String() args)
{
    Interf i = () -> sys("m1 method implemented");
     i.m1()
}
}
```

Using lambda expression we dont need to write a separate class, just we can replace total implementation with lamda expression.
To  invoke lambda expression we need Funtional Interface.


2) Example 2-----without lambda 
```
package collect;
interface Inter
{
	public void add(int a, int b);
}

class Demo implements Inter{

	@Override
	public void add(int a, int b) {
		// TODO Auto-generated method stub
		System.out.println("The sum is "+ (a+b));
		
	}
}
public class lambdaDemo1 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Inter i = new Demo();
		i.add(10, 20);
		i.add(100, 200);
	}
}
```
-----------with lambda ---------------------------------
```
package collect;
interface Inter
{
	public void add(int a, int b);
}
/*
class Demo implements Inter{

	@Override
	public void add(int a, int b) {
		// TODO Auto-generated method stub
		System.out.println("The sum is "+ (a+b));
		
	}
} */
public class lambdaDemo1 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Inter i = (a,b)->System.out.println("The sum is "+ (a+b));;
		i.add(10, 20);
		i.add(100, 200);
	}
}
```
3. Example Demo 3---------
```
package collect;
interface interfac{
	public int  getLength(String s);
	
}

class Demo implements interfac{

	@Override
	public int getLength(String s) {
		// TODO Auto-generated method stub
		return s.length();
	}	
}
public class LambdaDemo2 {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		interfac i = new Demo();
		System.out.println(i.getLength("Hello"));
        System.out.println(i.getLength("without lambda"));
	}
}
```

------with lambda -----------------------
```
package collect;
interface interfac{
	public int  getLength(String s);
	
}

public class LambdaDemo2 {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		interfac i = s->s.length();
		System.out.println(i.getLength("Hello"));
        System.out.println(i.getLength("with lambda"));
	}
}
```
4. Lambda Demo 4----------
without lambda --
```
package collect;
interface in{
	public int squareIt(int a);
}

class demo implements in{
	@Override
	public int squareIt(int a) {
		// TODO Auto-generated method stub
		return a*a;
	}	
}
public class LambdaDemo3 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		in i = new demo();
		System.out.println(i.squareIt(2));
		System.out.println(i.squareIt(5));

	}

}
```

----with lambda expressiion ------------
```
package collect;
interface in{
	public int squareIt(int a);
}

public class LambdaDemo3 {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		in i = a->a*a;
		System.out.println(i.squareIt(2));
		System.out.println(i.squareIt(5));

	}
}
```
------------------------------------------------------------------------------------------------------------------------
Two way to define a thread -
1) To extend the thread class
2) By implementing the runnable interface .
```
package collect;
class myRunnable implements Runnable{
	@Override
	public void run() {
		// executed by child thread
		for(int i=0;i<10;i++) {
			System.out.println("Child Thread");
		}	
	}	
}
public class ThreadsDemo {
	public static void main(String[] args) {
          Runnable r = new myRunnable();
          Thread t = new Thread(r);
          t.start();    //2 threads - main thread and child thread
          for(int i=0;i<10;i++) {
        	  System.out.println("Main Thread");  //main thread
          }     
	}
}
```
now using Lambda Expression-------
```
package collect;
public class ThreadsDemo {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
          Runnable r = ()->{for(int i=0;i<10;i++)
                               {
        	                      System.out.println("Child thread with lambda");
                                }
        	                };
          Thread t = new Thread(r);
          t.start();    //2 threads - main thread and child thread
          for(int i=0;i<10;i++) {
        	  System.out.println("Main Thread");  //main thread
          }     
	}
}
```
Ques- Why functional Interface should contain only one abstract method?
Compiler will get confused while infering the type of functional interface as there are 2 abstract method.

Ques- What is the advantage of @FunctionalInterface annotation?
By providing this annotation we convey the message that this interface cant contain more than one abstract method.


------Lambda expression in collection ---------

Collection - represent a group of objects as single entity .
1)List (I)  - insertion order preserved, duplicate objects allowed 
2)Set(I)   -  insertion order not preserved, duplicate objects not allowed
3)Map(I)   -  Key Value pair 
4)Comparator(I) - Customised sorting ,compare()<-abstract method


comparator demo code - without using lambda 
```
package collect;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class myComparator implements Comparator<Integer>{

	@Override
	public int compare(Integer o1, Integer o2) {
		/* TODO Auto-generated method stub
		if(o1>o2) {
			return -1;
		}else if(o1<o2) {
			return 1;
		}else 
		return 0;*/	
		return (o1>o2)?-1:(o1<o2)?+1:0;
	}	
}
public class ArrayListDemo {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		ArrayList<Integer> l = new ArrayList<>();
        l.add(10);
        l.add(0);
        l.add(15);
        l.add(5);
        l.add(20);
        
        System.out.println("Before Sorting:"+l);
        Collections.sort(l);
        System.out.println("After sorting:"+l);
        Collections.sort(l,new myComparator());
        System.out.println("After cusomised sorting:"+l);
	}

}
```

-----------------code with lambda expression ------------------
```
package collect;
import java.util.ArrayList;
import java.util.Collections;

public class ArrayListDemo {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		ArrayList<Integer> l = new ArrayList<>();
        l.add(10);
        l.add(0);
        l.add(15);
        l.add(5);
        l.add(20);
        
        System.out.println("Before Sorting:"+l);
        Collections.sort(l);
        System.out.println("After sorting:"+l);
        Collections.sort(l,(I1,I2)->(I1>I2)?-1:(I1<I2)?+1:0);
        System.out.println("After cusomised sorting:"+l);
	}

}
```

Now for TreeSet ---SOrting 
if you want sorting order in Map than go for TreeMap -Key Value Pair is inserted according to sorting order
TreeMap<Integer,String> k = new TreeMap<Integer,String>(); <-default natural sorting order


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Anonymous inner classes vs Lambda Expressions 

1)wherever anonymous class we are using there may be a chance of using lambda expression 
2) Nameless inner class = anoonymous inner class 
Runnable r = new Runnable();   <--Gives the error 

Runnable r = new Runnable()  <--No error , No name for implementation class such type of class is called as anonymous inner class 
{
    public void run()
     {   ---
     }
}


Every anonymous inner class can be replaced with lambda expression? --- > No 
lambda expression not came for replacing the anonymous inner class.
Anonymous inner class more powerful than lambda expression 

features of anonymous inner class - >
1) Anonymous inner class can extend concrete class.
2) Anonymous inner class that extends abstract class.
3) Anonymous inner class that implements an interface which contains multiple methods.
4) Anonymous inner class that implements an interface with only one abstract method than that class can be replaced with lambda expression.

Anonymous inner class != Lambda expression 

This functionality also differ in Anonymous inner class and Lambda expression .

Interface Interf{
 public void m1();
}
class Test {
  int x= 888;
  public void m2(){
   Interf i = new Interf()
   {    int x = 999; } instance variable 
       public void m1()
       {   sys(This.x)  <-this refers to current inner class object only = 999
           sys(Test.this.x) <-this refers to outer class object  = 888
       }
};
} ; m1();

public void main (String() args ){
 Test t = new Test();
 t.m2();
  }
}


Inside Anonymous inner class it is posible to declare instance variable but inside lambda expression it is not possible to declare instance varibales.
In the lambda expression  this always refers current object outer class only , but inside anonymous inner class , this always refers inner class only.

-----------------------program code -----------------------------
package collect;

interface InterfD {
    public void m1();
}

class AnonymousVsLambda {
    int x = 888; // Outer class variable

    public void m2() {
        // Creating an anonymous inner class that implements InterfD
        InterfD i = new InterfD() {
            int x = 999; // Instance variable in the anonymous inner class

            @Override
            public void m1() {
                // `this.x` refers to the instance variable of the anonymous inner class
                System.out.println("this.x: " + this.x); // Output: 999

                // `Test.this.x` refers to the `x` variable of the outer class (Test)
                System.out.println("Test.this.x: " + AnonymousVsLambda.this.x); // Output: 888
            }
        };
        i.m1(); // Call m1() method on the anonymous class instance
    }

    public static void main(String[] args) {
        // Create an instance of Test and call m2
    	AnonymousVsLambda t = new AnonymousVsLambda();
        t.m2();
    }
}
---------------now with lamba expression -------------
package collect;

interface InterfD {
    public void m1();
}
class AnonymousVsLambda {
    int x = 888; // Outer class variable
    public void m2() {
          InterfD i = ()->
              {
        	      int x = 999;
        	      System.out.println(this.x);       //output = 888
              };
        i.m1(); // Call m1() method on the anonymous class instance
    }
    public static void main(String[] args) {
        // Create an instance of Test and call m2
    	AnonymousVsLambda t = new AnonymousVsLambda();
        t.m2();
    }
}

Difference between Anonymous inner class and Lambda expression 
1-class without name                                                |
2-can extend abstract class &concrete class                         |
3-can implement interface with multiple abstract method             |
4-Inside anonymous inner class , can declare instance variable      |
5-Anonymous inner class can be instantiated                         |
6-Inside AIC this refers to current AIC object                      |
7-best option to handle multiple methods                            |
8-



Advantages of Lambda Expression - 
1) handle functional programming in java.
2) reduce length of the code so that readability will be improved.
3) resolve the complexity of the anonymous  Inner class with some extent.
4) can handle procedures/functions just like values .
5) can pass procedures/function as arguments.
6) easier to use updated APIs and Library.
7) Enable support for parallel processing.


Default Methods inside interface ---------------------------

before 1.7 every method inside interface are public and abstract .
every variable inside interface is considered as public static final.

after 1.8 version we can define concrete methods also inside interface.- called default methods 

demo code -
package collect;

interface interfaceD{
	default void m1() {
		System.out.println("default method");
	}
}

public class defaultMethodDemo implements interfaceD {
	
	public void m1() {
		System.out.println("my own implementation");
	}

	public static void main(String[] args) {
		defaultMethodDemo d = new defaultMethodDemo();
		d.m1();
	}

}


default methods wrt multiple inheritence --------
if two implementated interface contains same method than
1.we need to provide default implementation in the class to overcome this problem.
2.or you can use Left.super.m1() ; to call the particular interface method.

Demo COde -----
package collect;

interface Left{
	   default void m1(){
	     System.out.println("Left Default Method");
	   }
	}
interface Right{
	   default void m1(){
	   System.out.println("Right Default Method");
	   }
	}

	class DefaultInterfaceDemo implements Left,Right
	{
	    public void m1() {
	      // System.out.println("My own implementation ");
	    	Left.super.m1();
	    }

	   public static void main (String[] args )
	    {
	       DefaultInterfaceDemo d = new DefaultInterfaceDemo();
	       d.m1();
	    }	   
}

** Difference between Interface with Default Methods and Abstract Classes **

1)Inside interface every variable is always public,static and final            |  1)  Inside abstract class we can declare instance variables
  we can not declare instance variables.                                       |        which are required to child class.
2)Interface never talks about state of object.                                 |  2)  Abstract class can talk about state of object.
3)Inside interface we can't declare constructors.                              |  3)  Inside abstract classes we can declare constructors 
4)Inside interface we can't declare instance and static blocks.                |  4)  Inside abstract classes we can declare constructors 
5)Functional Interface with default methods can refer Lambda expression        |  5)  Abstract class can't refer Lambda expression.
6)Inside interface we can't override object class methods.                     |  6)  Inside Abstract classes we can override object class methods.



Static Methods inside interface --
from 1.8 onwards we can declare static methods inside interface .
Static methods no way related to object.
Interface also no way related to object.

What is the need of defining static methods inside class 
to define general utility methods.

Demo Code --
package collect;

interface InterfaceS{
	  public static void m1(){
	    System.out.println("Interface static method");
	    }
	}

	class InterfaceStaticDemo implements InterfaceS{
	  public static void main(String[] Args){
	    InterfaceStaticDemo s = new InterfaceStaticDemo();
	   //no s.m1();   //by using implemented class object 
	   //no  InterfaceStaticDemo.m1();  //by using class name 
	    InterfaceS.m1();       //by using interface name-- Right 
	 }  
}


overriding concept is not applicable for interface static method.
before 1.7 we can't declare main method ,can't run interface directly from command prompt 

inteface InterfaceM{
   public static void main(String[] args){
    System.out.println("Interface main method");
   }
}

SO from 1.8 onwards we can run interface directly from the command prompt


why default methods ?  
without affecting implementation classes if we want to add new methods to the interface (extending interface functionality) .
To define general utility methods inside interface with static 

Predefined Functional Interfaces-----
1)Predicate 
2)Function 
3)Consumer 
4)Supplier 
-----------------
Two argument Predefined functional interfaces --
1)BiPredicate 
2)BiFunctional 
3)BiConsumer 

-------------------------------------
Primitive Functional Interfaces :
1)IntPredicate 
2)IntFunction 
3)IntConsumer 


Predicate(I) ----- it is a boolean valued function 
1)perform some conditional checks and returns true and false based on some conditions
2)introduced in 1.8 version 
3)in java.util.function
4)test()

interface Predicate<T>{
  boolean test(T t);
}

public boolean test(Integer I)
{
  if(I>10){
    return true ;
   }
   else {
     return false;
   }
}

Lambda expression 
I->I>10;

Predicate<Integer> P =I->I>10;
System.out.println(P.test(100));

Code Demo --
package collect;
import java.util.function.Predicate;
public class predicateDemo {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Predicate<Integer> p = I->I>10;
		System.out.println(p.test(100));  //true
		System.out.println(p.test(5));  //false
	}
}



Code Demo --
package collect;
import java.util.function.Predicate;
public class CheckLength {

	public static void main(String[] args) {
		Predicate<String> p = s->s.length()>5;
		System.out.println(p.test("abcdef")); //true 
		System.out.println(p.test("abc"));  //false
	}
}


Code Demo --
package collect;

import java.util.*;
import java.util.function.Predicate;
public class CheckIsEmpty {
	public static void main(String[] args) {
		Predicate<Collection> p = c -> c.isEmpty();
		ArrayList l1 = new ArrayList();
		l1.add("A");
		System.out.println(p.test(l1));  //false 
		
		ArrayList l2 = new ArrayList();
		System.out.println(p.test(l2));   //true 
	}
}


Predicate inteface contains one method what is that method - test method what is its return type boolean 


Predicate Joining -----
1)p1-to check whether the given number greater than 10 or not.
2)p2-given number is even number or not.

p1.negate() <-opposite of the given predicate 
p1.and(p2)  <-both conditions is checked 
p1.or(p2)  <-atleast one condition should be satisfied

negate() , and() , or()  <- default methods inside predicate 

Demo code ---
package collect;
import java.util.function.Predicate;
public class CombinePredicate {
	public static void main(String[] args) {
		int[] x = {0,5,10,15,20,25,30};
		Predicate<Integer> p1 = i->i>10;
		Predicate<Integer> p2 = i->i%2==0;
		System.out.print("The numbers greater than 10 are :");
		m1(p1,x);
		System.out.println();
		System.out.print("The even numbers are :");
		m1(p2,x);
		System.out.println();
		System.out.print("The numbers not greater than 10 are:");
		m1(p1.negate(),x);
		System.out.println();
		System.out.print("The numbers greater than 10 and are even numbers are :");
		m1(p1.and(p2),x);
	}	
	public static void m1(Predicate<Integer>p,int[] x) {
		for (int x1: x) {
			if(p.test(x1))
				System.out.print(x1);
		}
	}
}


program to diplay names started with 'k' by usung predicate --

package collect;
import java.util.function.Predicate;
public class PredicateDemoforName {
	public static void main(String[] args) {
		String[] names = {"Sunny","Kajal","Mallika","Katrina","karina"};
		Predicate<String> startsWithK = s->s.charAt(0)=='K';
		System.out.println("The names starts with K are :");
        for(String s:names) {
        	if(startsWithK.test(s)) {
        		System.out.println(s);
        	}
        }
	}
}


Remove null values and empty strings using Predicate -----------

package collect;
import java.util.ArrayList;
import java.util.function.Predicate;

public class CheckNullEmptyString {
	public static void main(String[] args) {
		String[] names = {"Durga","",null,"Ravi","","Shivam",null};
		
		Predicate<String> p=s->s !=null && s.length()!=0;
		ArrayList<String> l = new ArrayList<String>();
		for(String s:names) {
			if(p.test(s)) {
				l.add(s);
			}
		}
		System.out.println("The list of valid strings are:");
		System.out.println(l);
	}
}

program for user authentication by using predicate------
Predicate<User> P= user->user.username.equals("Nitish") && user.password.equals("java");
Scanner s = new Scanner(System.in);



program for software engineer whether he is allowed i pub or not ----
package collect;

import java.util.function.Predicate;

class SoftwareEngineer{
	String name ;
	int age ;
	boolean isHavingGf;
	SoftwareEngineer(String name, int age, boolean isHavingGf){
		this.name = name ;
		this.age = age ;
		this.isHavingGf = isHavingGf;
	}	
	public String toString() {
		return name ;
	}
}

public class CheckSoftwareEngineer {

	public static void main(String[] args) {
		SoftwareEngineer[] list = {new SoftwareEngineer("Nitish", 25, true),
				                   new SoftwareEngineer("Rahul", 28, false),
				                   new SoftwareEngineer("Raja",17,true),
		                           new SoftwareEngineer("Ashwani",30,true),
		                           new SoftwareEngineer("Ravi", 21, true)
				                  };
		
		Predicate<SoftwareEngineer> allowed = se->se.age >=18 && se.isHavingGf;
		for(SoftwareEngineer se:list) {
			if(allowed.test(se)) {
				System.out.println(se);
			}
		}
	}
}
Employee Management Application -------------------------------------------
package collect;

import java.util.ArrayList;
import java.util.function.Predicate;

class Employee{
	String name;
	String designation;
	double salary ;
	String city ;
	
	Employee (String name , String designation , double salary , String city){
		this.name = name ;
		this.designation = designation ;
		this.salary = salary;
		this.city = city ;
	}
	
	public String toString(){
		String s = String.format("(%s,%s,%.2f,%s)",name,designation,salary,city);
		return s;
	}
	
	public boolean equals(Object obj) {
		Employee e = (Employee)obj;
		if(name.equals(e.name)&&designation.equals(e.designation)&&salary==(e.salary)) {
			return true;
		}else {
			return false;
		}
	}
}

public class EmpManagementApp {
	public static void main(String[] args) {
		ArrayList<Employee> list= new ArrayList<>();
		populate(list);
	    //System.out.println(list);
		Predicate<Employee> p1=emp->emp.designation.equals("Manager");
		System.out.println("Manager Information :");
		display(p1, list);
		
		Predicate<Employee> p2 = emp-> emp.city.equals("Bangalore");
		System.out.println("Bangalore Employee Information :");
		display(p2, list);
		
		Predicate<Employee>p3 = emp->emp.salary<20000;
		System.out.println("All Employees Infromation whose salary < 20000");
		display(p3, list);
		
		System.out.println("All Manager from Bangalore to give pink slip :");
		display(p1.and(p2),list);
		
		System.out.println("All manager whose salary less than 20000 :");
		display(p1.and(p3),list);
		
		System.out.println("All Employee who are not manager:");
		display(p1.negate(), list);
		
		Predicate<Employee> isCEO = Predicate.isEqual(new Employee("Nitish","CEO",10000,"Delhi"));
		Employee e1= new Employee("Nitish","CEO",10000,"Delhi");
		System.out.println("Employee equal to Nitish is: ");
		System.out.println(isCEO.test(e1));   //override equal method is compulsary
	}	
	
	public static void display(Predicate<Employee> p,ArrayList<Employee>list) {
		for(Employee e:list) {
			if(p.test(e)) {
				System.out.println(e);
			}
		}
		System.out.println("********************************************************************");
	}
	public static void populate(ArrayList<Employee> list) {
		list.add(new Employee("Nitish","CEO",10000,"Delhi"));
		list.add(new Employee("Sunny","Manager",20000,"Bangalore"));
		list.add(new Employee("anushka","developer",4000,"Bangalore"));
		list.add(new Employee("Raja","Manager",10000,"Chennai"));
		list.add(new Employee("Sowmya","Lead",70000,"Delhi"));
		list.add(new Employee("Ramya","Developer",60000,"Pune"));
	}	
}



default static method in PRedicate is isEqual() override equal method is compulsary.

---
package collect;
import java.util.function.Function;
public class FunctionalInterfDemo {
	public static void main(String[] args) {
	   Function<String,Integer> f= s->s.length();
	   System.out.println(f.apply("Nitish"));
	   System.out.println(f.apply("Software"));
	}
}

---
package collect;
import java.util.function.Function;

public class FunctionDemo2 {
	public static void main(String[] args) {
		Function<Integer, Integer> f = n->n*n;
		System.out.println("Square of 2:"+f.apply(2));
		System.out.println("Square of 3:"+f.apply(3));
	}
}

---
difference between predicate and function interface 

| Tables        | Predicate           | function |
| ------------- |:-------------:| -----:|
| 1 | To implement condition check go for predicate                               | To perform certain operation and to return some result we should go for function|
| 2 | Predicate can take one parameter which represent input argument Predicate<T>|Function can take 2 parameters,input and return type Function<T,e> |
| 3 |  Predicate interface defines one abstract method called test()              |Function interface defines one abstract method called apply() |
| 4 |  public boolean test(T t)                                                   |   public R apply(T t) |
| 5 |  Predicate can return only boolean value                                    |   Function can return any type of value |


---
Program to remove space present in the given string by using function 

package collect;
import java.util.function.Function;

public class RemoveSpaceFunction {
	public static void main(String[] args) {
		String str = "Nitish is a senior software developer";
		Function<String, String> f=s->s.replaceAll(" ","");
		System.out.println(f.apply(str));
	}
}


---
Program to count space present in the given string by using function 
package collect;
import java.util.function.Function;

public class CountNoOfSpaces {

	public static void main(String[] args) {
		String str = "Mera Joota Hai Japani";
		Function<String,Integer> f=s->s.length()-s.replaceAll(" ","").length();
		System.out.println(f.apply(str));
	}
}

---
Program to find the grade for students using funtion 

```
package collect;
import java.util.ArrayList;
import java.util.function.Function;

class Student{
	String name;
	int marks;	
	Student(String name,int marks){
		this.marks = marks;
		this.name = name;
	}
}

public class FindGradeFunction {
	public static void main(String[] args) {
		ArrayList<Student> l = new ArrayList<>();
	    populate(l);
	    Function<Student,String> f=s->{
	    	int marks=s.marks;
	    	if(marks>=80) {
	    		return "A";
	    	}else if(marks>=60) {
	    		return "B";
	    	}else if(marks>=50) {
	    		return "C";
	    	}else if(marks>=40) {
	    		return "D";
	    	}else {
	    		return "Fail";  
	    	}
	    };
		    
	    for(Student s: l) {
	    	System.out.println("Student Name:"+s.name);
	    	System.out.println("Student Marks:"+s.marks);
	    	System.out.println("Student Grade:"+f.apply(s));
	    	System.out.println();
	    }
	}
	public static void populate(ArrayList<Student> l) {
		l.add(new Student("Sunny",100));
		l.add(new Student("Bunny",65));
		l.add(new Student("Chinny",55));
		l.add(new Student("Vinny",45));
		l.add(new Student("Pinny",25));
	}	
}
```
---
Program to find total month salary of all Employee by using Function 
```
package collect;
import java.util.ArrayList;
import java.util.function.Function;

class Employees{
	String name ;
	double salary;
	Employees(String name, double salary){
		this.name = name;
		this.salary = salary;
	}	
	public String toString() {
		return name+":"+salary;
	}
}
public class FindSalaryFunction {
	public static void main(String[] args) {
		ArrayList<Employees> l = new ArrayList<Employees>();
		populate(l);
		System.out.println(l);
		Function<ArrayList<Employees>,Double> f = l1 ->{
			double total=0;
			for(Employees e:l1) {
				total=total+e.salary;			
			}
			return total;
		};
		System.out.println("The toal salary of this month:"+f.apply(l));
	}	
	public static void populate(ArrayList<Employees> l) {
		l.add(new Employees("Sunny",1000));
		l.add(new Employees("Bunny",3000));
		l.add(new Employees("Chinny",3000));
		l.add(new Employees("Vinny",4000));
		l.add(new Employees("Pinny",5000));
	}
}
```

Program to increament salary using predicate ------------------------
```
package collect;
import java.util.ArrayList;
import java.util.function.Function;
import java.util.function.Predicate;

class Employees{
	String name ;
	double salary;
	Employees(String name, double salary){
		this.name = name;
		this.salary = salary;
	}	
	public String toString() {
		return name+":"+salary;
	}
}
public class FindSalaryFunction {
	public static void main(String[] args) {
		ArrayList<Employees> l = new ArrayList<Employees>();
		populate(l);
		
		System.out.println("Before Increment:");
		System.out.println(l);
		
		Predicate<Employees> p=e->e.salary<3500;
		Function<Employees,Employees> f= e->{
			e.salary=e.salary+477;
			return e;
		};
		
		System.out.println("After Increment:");
		ArrayList<Employees> l1 = new ArrayList<>();
		for(Employees e:l) {
			if(p.test(e)) {
				l1.add(f.apply(e));
			}
		}
		System.out.println(l);
		System.out.println("Employees with increamented salary:");
		System.out.println(l1);
	}		
	
	public static void populate(ArrayList<Employees> l) {
		l.add(new Employees("Sunny",1000));
		l.add(new Employees("Bunny",3000));
		l.add(new Employees("Chinny",3000));
		l.add(new Employees("Vinny",4000));
		l.add(new Employees("Pinny",5000));
	}
}
```

**Function Chaining**  -- andThan & compose  & identity()
```
package collect;
import java.util.function.Function;

public class FunctionChaining {

	public static void main(String[] args) {
		Function<String, String> f1=s->s.toUpperCase();
		Function<String, String> f2=s->s.substring(0,9);
		
		System.out.println("The result of f1:"+f1.apply("AishwaryaAbhi"));
		System.out.println("The result of f2:"+f2.apply("AishwaryaAbhi"));
		System.out.println("The result of f1.andThen(f2):"+f1.andThen(f2).apply("AishwaryaAbhi"));
		System.out.println("The result of f1.compose(f2):"+f1.compose(f2).apply("AishwaryaAbhi"));
	}

}
```
---
**Consumer**
- want a function to consume a value only
- interface Consumer<T>{  accept(){} }
```
package collect;
import java.util.function.Consumer;

public class ConsumerDemo {
	public static void main(String[] args) {
	    Consumer<String> c=s->System.out.println(s);
	    c.accept("Hello");
	    c.accept("Nitish");
	}
}
```

Program to display movie information using consumer --
```
package collect;

import java.util.ArrayList;
import java.util.function.Consumer;

class Movie{
	String name ;
	String hero ;
	String heroine ;
	Movie(String name,String hero, String heroine){
		this.name = name;
		this.hero = hero;
		this.heroine = heroine;
	}
}
public class ShowMovie {
	public static void main(String[] args) {
		ArrayList<Movie> l = new ArrayList<>();
		populate(l);
		Consumer<Movie> c = m->{
			System.out.println("Movie Name :"+m.name);
			System.out.println("Movie Hero :"+m.hero);
			System.out.println("Movie Heroine :"+m.heroine);
			System.out.println();
		};
		
		for(Movie m: l) {
			c.accept(m);
		}
	}
	
	public static void populate(ArrayList<Movie> l) {
		l.add(new Movie("Bahubali" ,"Prabahas","Anushka"));
		l.add(new Movie("Koi Mil Gya" ,"Ritik","Ana"));
		l.add(new Movie("Ram" ,"Pra","Anushdfoka"));
		l.add(new Movie("rakashak" ,"Salman","Anush"));
	}
}
```













----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Streams in java 

Java 8 streams and Java I/O Streams are different from each other.

Java I/O Streams >> Working with files i.e. Reading and Writing 
Java 8 Streams >> Processing and filtering data over different data Sources.


Collections and Streams purpose also different from each others.

Collections  >> Storing the data 
Streams      >> Processing and Filtering data over different data sources.



Definition of Streams ->
Stream represent sequence of objects derived from a source (Arrays, COllections, IO resources ) over which aggregate operations can be performed .
Technically Stream is Typed Interface which means that stream can be defined for any kind of objects , Stream of characters , Stream of employees/customer/cities.

Characterstics of Streams ->

Element Sequence -> Stream provide a set of elements of particular type in seqential manner.The Stream gets an element on demand and never store an item.
Source -> Stream can take the data from different sources such as Collection , Arrays , I/O Resources etc.
Aggregate Operations -> Streams support aggregate operations such as forEach, filter , Map , Sorted and so on .
Automated Iterations -> Stream operations carry out iterations internally over the sources of elements as opposed to collections where explicit iteration is required.


How to get stream object -> just by calling the stream method on collection object.


Different ways to create Stream Object 

1) Creating empty Stream object which allowed to string values only 
   Stream <String> names = Stream.empty();

2) Creating stream object from collection Object
   Collection<String> names = Arrays.asList("Mahesh","Suresh","Ramesh");
   Stream nameStream = names.stream();

3) Creating stream object from Array
   String[] arr = new String[]{"a","b","c"};
   Stream<String> streamOfArrayFull = Arrays.stream(arr);

4) We can create Stream object by using builder method 
   when builder is used , the desired type should be additionally specified in the right part of the statement, otherwise the build() method will create an instance of the 
   Stream<Object>:
   Stream<String> nameStream = Stream.<String>builder()
                               .add("a")
                               .add("b")
                               .add("c")
                               .build()


In a java program we can perform 2 Kind of operation 

<a href="the-url-you-want-to-go-when-image-is-clicked.com" />
<img src="https://javagoal.com/wp-content/uploads/2020/01/22-1.jpg" />
![alt text](https://javagoal.com/wp-content/uploads/2020/01/22-1.jpg)








