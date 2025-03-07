intialise many variable -- individual approach
int x= 9 ;
int y= 10 ;
int z = 11;


to initialize 10000 variable - huge number of values 
--> Arrays come in 
Student[] s = new Student[1000];
biggest advantage - array can represent huge number of values by single variable.

Limitations of arrays ->
1. Arrays are fixed in size . we should know the size in advance which may not possible always .
2. Arrays can hold only homogeneous type of elements. problem can be solved by taking object array.
3. No underlying Data Structure i.e no readymade support available you need to code for your problems .


To overcome these  problems we go to collections -
1. Collections are growable in nature .
2. Collections can hold homogeneous as well as heterogeneous objects .
3. Collection class is implemented based on some standard data structure.


Which one to prefer -
Arrays - if you know the size in advance highly recommended .
Collections  - if you dont know the size or need to store heterogeneous objects . as it provides growable nature due to which we need to compromise with performance.


for example suppose  array - of crore elements 
                    in arrayList - to add 1 core 1th element -  1st all the elements are copied to new arraylist of bigger size than 1th element is added next to it 
                                                                and the pointer start pointing to the new arraylist making the older array eligible for garbage collection.



     Arrays                          |             collections
1.fixed in size                      |         Growable in nature 
2.with respect to memory ❌          |        with respect to memory ✔️
3.with resopect to performance✔️     |        with respect to performance ❌
4.can hold only homogeneous element  |        can hold both homogeneous and hetrogeneous element
5.underlying Data Structure ❌       |        Standard Data Structure ✔️
6.primitive and object can hold       |        hold only object 





Collections - a group of individual objects 
Collection Framework - several classes and interfaces which can be used to represent a group of object as a single entity.


Difference between collection and collections -

                             collection                                       |             collections 
1. interface                                                                  |                  class 
2.used to represent a group of individual objects as a single entity.         |          is an utility class present in java.util.package to define several utility methods 
                                                                              |          (like Sorting,Searching..) for collection objects 


Differences between List and Set  -
                      List                              |               Set 
    👉Duplicates allowed                               |           Duplicates not aloowed 
    👉insertion order preserved                        |           insertion order not preserved 


question - which one will provide much information - classs or interface 
answer  - interface will provide much information , class is dummy thing which implemnts interface 

Colections framework - 9 Key interfaces 

1.collection -  if we want to represent a group of objects as a single entity then we should go for collection .
             -  collection interface defines most common methods which are applicable for any Collection object.
             -  collection interface is considered as root interface of collection Framework.
             -  👉 There is no concrete class which implements collection interface directly.

2.List Interface  - Child interface of collection inteface 
                  - If we want to represent a group of individual objects as a single entity where duplicates are allowed and insertion order is preserved then we should go for list.
                  - implementation class for List interface are -> ArrayList  , Linked List and Vector ->Stack(leagcy classes).

3.Set Interface   -child interface of collection interface 
                  - duplicate not allowed and insertion order is not preserved.
                  - implementation class for Set InterFace are -> HashSet -> LinkedHashSet 

4.SortedSet Interface - Child interface of Set Interface
                      - represent a group of individual objects as a single entity where duplicates are not allowed but all objects should be inserted according to some 
                        sorting order then we should go for SortedSet.

5.NavigableSet Interface - Child interface of SortedSet Interface 
                          - several methods for navigation purposes

6.Queue Interface  - Child interface of collections 
                   - If we want to represent a group of individual objects prior to processing then we should go for Queue.
                   - implementation class for Queue - PriorityQueue 
                                                    - Blocking Queue ->LinkedBlocking Queue
                                                                     ->PriorityBlocking Queue

7.Map Interface - Map is not child interface of collection Interface .
                - Key value pairs - duplicate keys are not allowed but values can be duplicate
                - implementation classes of Map -> HashMap->LinkedHashMap
                                                -> WeakHashMap
                                                -> IdentityHashMap
                     Dictionary(abstract class) -> Hashtable->Properties
                                                -> SortedMap(I) -> NavigableMap(I) -> TreeMap

Need Sorting go for ->
8.Comparable(I) - default natural sorting order 
9.Comparator(I) - customised sorting order 

Want to collect object one by one go for ->
Cursors -> 1. Enumeration(I)
           2. Iterator(I)
           3. ListIterator(I)

Utility classes in collections framework 
1. Collections  - conatins several utility methods for collection classes
2. Arrays       - contains several utility methods for Arrays 



---

Collection Interface -
-> If we want to represent a group of individual objects as a single entity then we should go for collectuion.
-> In  general collection interface is considered as root interface of collection framework.
-> Collection interface defines the most common methods which are applicable for any collection object.
-> general methods are - add(Object O)
                       - addAll(Collection C)
                       - remove(Object O)
                       - removeAll(Collection C)
                       - clear()
                       - retainAll(Collection C)
                       - isEmpty()
                       - size()
                       - contains(Object O)
                       - containsAll(Collection c)
                       - toArray()
                       - iterator()

-> Collection interface doesn't contain any method to retrieve objects there is no concrete class which implements collection class directly.

---

List Interface -> child interface of collection 

when go for list - need duplicates and insertion order preserved 

index is used to differentiate between two duplicate objects
insertion order preserved by placing 1st element at index 0 , 2nd at index 1 similarly insertion order can  be  preserved.

methods available in List->  all collection methods 
                         -> add(int index, Oject O )
                         -> addAll(int index, Collection c)
                         -> remove(int index)
                         -> indexOf( "A")
                         -> lastIndexOf("A") 
                         -> get(int Index)
                         -> set(int index,Object new )
                         -> ListIterator listIterator()

Implementation classes - ArrayList , Linked List , Vector 

ArrayList -> Resizable array or growable array
          -> Duplicates are allowed 
          -> Insertion order is preserved 
          -> Hetrogeneous objects are allowed (Except TreeSet and TreeMap )
          -> "null" insertion is possible 

constructors =>

1. ArrayList l = new ArrayList();
   new array of default size - 10 will be created and if  we try to insert the 11th element than its 
   new capacity = (current capacity * 3/2) + 1 ;
   and the pointer will start pointing to the new array making the previous arrray eligible for garbage collection.

2. ArrayList l = new ArrayList(int initialCapacity);
   contructor with predefined capacity to increase the performance 

3. ArrayList l = new ArrayList(Collection c)
   constructor with any collection object it may be linkedList , Stack  . If you want to create a equivalent object . 
   It is meant for interconversion of objects.

in any collection the output will be like [A,10,A, null] i.e.. in square brackets because whenever we try to print any object 
refrence internally toString() method will be called and in every collection the toString method is implemented like [...] .



----------------------java code for the arrayList --------------------------------
```
package collect;

import java.util.ArrayList;
import java.util.List;

public class ListOperationsExample {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		List<Object> num = new ArrayList<>();  //generics of object type used 
		num.add(12);
		num.add(57);
		num.add(21);
		num.add("A"); 
		num.add(null);

		System.out.println("List after adding elements " + num);		
		num.add(2, 65);		
		System.out.println("List after adding elements " + num);		
		
		ArrayList l = new ArrayList();   //generics came lator will go on that 
		l.add(1);
		l.add("P");
		l.add(null);
		
		System.out.println("the arraylist with heterogeneos object is" + l);
		
	}
}
```
---------------------------------------------------------------------------------------------------------------------------

goal of collection - to hold and transfer objects from one place to another place 
->To hold the data and transfer compulsaraly it should be serializable
=> To support this type of requirement every collection class implements serializable interface.


sender ->arrayList (serializable) ----------- --------- --------- ----> arraylist (cloned to use)<-reciever

->every collection class already implements clonnable interface

------------------------------------------------------------------------------------------------------------------------------
ArrayList and Vector implements Random Access Interface-> any random element we can acess with the same speed.
-> If our frequent operation is retrieval operation then arrayList is the best choice.
RandomAccess Interface -> present in java.util
                        -> Marker (Interface)


    ArrayList l1 = new ArrayList();
		LinkedList l2 = new LinkedList();
		System.out.println(l1 instanceof Serializable); //true
		System.out.println(l2 instanceof Serializable); //true
		System.out.println(l1 instanceof Cloneable);    //true
		System.out.println(l2 instanceof Cloneable);    //true
		System.out.println(l1 instanceof RandomAccess); //true
		System.out.println(l2 instanceof RandomAccess); //false
		
->If our frequent operation is insertion/removal in the middle than Arraylist is the worst choice(because several shift operation are required).


What  is the difference between the arrayList and the vector.
                    ArrayList                                   |                Vector 
  👉   non synchronized methods                                 |         synchornized methods
  👉   not thread Safe                                          |        thread Safe
  👉   performance is relatively high                           |        relatively performance is low 
  👉   1.2 v non legacy class                                   |        1.0 v legacy class


I want to use ArrayList Only and also want thread safety . How to achieve synchronized version of ArrayList Object ?
by using Collection class synchronizedList() method.

        public static List synchronizedList(List l)

        ArrayList l = new ArrayList();               //non- synchronized
        List sl = Collections.synchronizedList(l);  //synchronized

-------------------------------------------------------------x----------------------------------------------------------x----------------------------------------------------

LinkedList class -> If we want to insert/delete in the middle of the list 
                 -> In linked List the elements is not stored at consecutive location of the memory 
                 -> underlying data structure is Doubly LinkedList
                 -> Insertion order is preserved.
                 -> Duplicates are allowed.
                 -> Heterogeneous Elements are allowed
                 -> null insertion is possible.
                 -> Linked List implements Serializable and Clonable interfaces but not RandomAccess Interface.

disadvantage ->  retrival operation takes time as it have to go to each node for next node address.

methods in Linked list -> addFirst()
                       -> addLast()
                       -> getFirst()
                       -> getLast()
                       -> removeFirst()
                       -> removeLast()

Constructors ->
1. LinkedList l = new LinkedList();   //creates an empty LinkedList Object
2. LinkedList l = new LinkedList(Collection c);  //creates an equivalent LinkedList Object for the  given Collection

---
```
package collect;
import java.util.LinkedList;
public class linkedListDemo {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		LinkedList l = new LinkedList();
		l.add("nitish");
		l.add(30);
		l.add(null);
		l.set(0,"Software");
		l.add(0,"venky");
		l.removeLast();
		l.addFirst("CCC");
		System.out.println(l);		
	}

}
```

diffeerence between ArrayList and LinkedList 

                    ArrayList               |          LinkedList
Best choice for Retrieval                   |        Best Choice for insertion or deletion in the middle 
Worst choice for insertion and deletion     |        Worst choice for retrieval 
Resizable or growable array                 |        Double LinkedList 
Implement RandomAccess                      |        doesnt implement RandomAccess Interface 


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. Vector class -> UNderlying data structure is Resizable Array /Growable array 
                -> Duplicates are allowed 
                -> Insertion order is preserved 
                -> 'null' insertion is possible 
                -> Heterogeneous objects are allowed 
                -> implements Serializable and clonable and RandomAccess Interface.
                -> Most of the methods present in vector are synchronized . Hence vector object is thread Safe.
                -> Best Choice is the frequent operation is retrieval.

Vector Specific Methods -> as its older version its method name are lengthy 
                        -> Remove(Object O)
                        -> removeElement(Object o)
                        -> remove(int index)
                        -> RemoveElementAt(int index)
                        -> clear()
                        -> removeAllElements()
To retireive elements -> Object get(int index)
                      -> Object elementAt(int index)
                      -> Object firstElement ()
                      -> Object lastElement()
other methods  ->
               int size();  <- current how many object are there
               int capacity();   <- Total how many object we can accomodate 
               Enumeration elements ();   <-get objects one by one 


Vector class constructors ->
1. Vector v = new Vector();   default intial capacity - 10
   new capacity = 2* current capacity 

2. Vector v = new Vector(int initial Capacity);   <-performance will be improved 
3. Vector v = new Vector (int initial Capacity,int incremental capacity)
4. Vector v = new Vector ( Collection C);  <- create an equivalent Vector Object for the given Collection


example code ----
```
package collect;

import java.util.Vector;

public class VectorDemo {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Vector v = new Vector();
	    System.out.println(v.capacity());   //10
	    for(int i= 1;i<=10;i++) {
	    	v.addElement(i);
	    }
	    System.out.println(v.capacity());    //10
	    v.addElement("A");
	    System.out.println(v.capacity());     //20
	    System.out.println(v);

	}

}
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Stack -> Child class of Vector 
      -> Speacially designed class for Last In First Out (LIFO)

contructor -> Stack s = new Stack();

various methods for Stack -> push ()= to add an object to the queue 
                          -> pop()  => to remove and return last element of the stack 
                          -> peek()  => to return the top of the stack without removal 
                          -> empty() => to check whether stack is empty or not 
                          -> search("A") => whether a particular element is present or not , return offset 


<------ example program ---->
```
package collect;

import java.util.Stack;

public class stackDemo {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Stack s = new Stack();
		s.push("A");
		s.push("B");
		s.push("C");
		System.out.println(s);  //A,B,C
		System.out.println(s.search("A"));  //3
		System.out.println(s.search("Z"));  //-1 if it is not available 
	}
}
```
---

                       
