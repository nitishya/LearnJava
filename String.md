**String**
- In any java project in 1000 objects , over 900 are string object.
- String objects are immutable,StringBuffer objects are mutable.
- immutable means non-changeable i.e. you cant change.
- all immutable object including String are thread safe.
- once string object is created than we can't change its content.
```
public class StringVsBufferDemo {

	public static void main(String[] args) {
		String s = new String("Nitish");
		s.concat("Yadav");
		System.out.println(s);   //Nitish
		
		
		StringBuffer sb = new StringBuffer("Nitish");
		sb.append("Yadav");
		System.out.println(sb);  //NitishYadav
	}
}
```
**Equals or ==**
```
public class EqualsDemo {

	public static void main(String[] args) {
		String s1 = new String("Nitish");
		String s2 = new String("Nitish");
		
		System.out.println(s1==s2); //false
		System.out.println(s1.equals(s2)); //true
		
		
		StringBuffer sb1 = new StringBuffer("Nitish");
		StringBuffer sb2 = new StringBuffer("Nitish");
		
		System.out.println(sb1==sb2); //false
		System.out.println(sb1.equals(sb2));  //false

	}

}
```
- s1==s2 as both are pointing to different objects , == always meant for reference comparison only.
- s1.equals(s2) , by default equals() method present inside Object class is for reference comparison but in che child classes as String/Stringbuffer equals method is overridden in  for content comparison.
- equals method is overridden in String class for content comparison while in StringBuffer class it is not overridden.
---
**Case 1:**
- String s = new String("Nitish");
- 2 Object will be created.
- whenever we are using new operator compulsary a new object is created in heap area with content Nitish with reference to s.
- For the future purpose one object will be created in SCP area i.e. String Constant Pool, No explicit refernece variable but internally implicit reference varaible is maintained by JVM.Using same object for future purpose.
- SCP Area - till 1.6 V ->Method Area /PERMGEN(Fixed) after 1.7 V it is moved to heap area(expandable).

**Case 2:**
- String s = "Nitish"
- Only one object is created in SCP Area.
- First JVM will check if any object containing the same content is available or not.If it is already there then it will reuse the same object else a new object will be created.

**Case 3**
```
String s1 = new String("nitish");  2 Heap,SCP
String s2 = new String("nitish");  1 Heap
String s3 = "nitish";  0  SCP
String s4 = "nitish" ; 0  SCP
```
How many object will be created? 3
In heap area , there can be 2 object with same content
but in SCP area, there can be only one object with same content

**Case 4:**
String s = new String("nitish") - 2 Heap,SCP
s.concat("kumar"); 1SCP as we are not assigning to any variable, GC(eligible)
beacuse of runtime operation if object is created 1 -heap
s = s.concat("yadav"); 1SCP,1 Heap,assigning to s

**Case 5:**
```
public class HeapVsSCP {

	public static void main(String[] args) {
		String s1  = new String("Spring"); 2
		s1.concat("Fall"); 2
		String s2 = s1.concat("winter"); 2
		s2.concat("Summer"); 2
	    System.out.println(s1); //spring
	    System.out.println(s2); //springwinter

	}
}
```
**Case 6:**
```
public class StringDemo {

	public static void main(String[] args) {
		String s1 = new String("You cannot change me");//2
		String s2 = new String("You cannot change me");//1
		System.out.println(s1==s2);//false
		
		String s3 = "You cannot change me"; //0
		System.out.println(s1==s3);//false
		
		String s4 = "You cannot change me";//0
		System.out.println(s3==s4);//true
		
		String s5 = "You cannot " + "change me";//if both are constant -compile time//0
		System.out.println(s4==s5);//true
		
		String s6 = "You cannot ";//1
		String s7 = s6+"change me";//compile time//1
		System.out.println(s4==s7);//false
		
		final String s8 = "You cannot "; //0
		String s9 = s8+"change me"; //every final variable can be replaced by a variable at compile time
		System.out.println(s4==s9);//true
	}

}
```
**Importance of String Constant Pool(SCP):**
Example - Voter Registration Form - form include many details like name,fname,mname etc in which state is constant like Hyderabad so for 1 crore registrations 1 crore object will be created for string Hyderabad.
  - to make it memory efficient we have SCP in java which create only one String constant in SCP and all object will refer to same .
  - In SCP single object can be referenced by multiple references.
  - **Problem** : Suppose a voter in 1 crore want to change its City to Voijaywada and is allowed to change than 1 crore will get effected.
  - Than Mutability Concept came,so String is immutable it can't be changed.
  - If a voter want to change his city a new object will be created only for that voter.
  - So immutablity concept is required only for SCP concept.
        
**FAQ**
1. Why SCP concept is available only for String object but not for StringBuffer?
   -The most commonly used constant in java is String object
2. Why String Objects are immutable where as StringBuffer Objects are mutable?
   - In String beacuse of SCP same object can be reused multiple times,by using one refernce if we are going to change the content the remaining refrences are going to be affected.So we need immutablity concept.
   - In StringBUffer SCP is not there.Seperate reference is there for evey object.
3. In addition to String Objects any other objects are immutable in java?
   - All wrapper class object are also immutable.Byte,Short,long,Integer

**Importance Constructors of String Class**
1. String s = new String(); ->creates an empty String Object
2. String s = new String(String literal);
3. String s = new String(StringBuffer sb);
4. String s = new String(StringBuilder sb);
5. String s = new String(char[] ar);
6. String s = new String(byte[] b);

**Important methods of String Class**
1. public char charAt(int index)
```
public class MethodCharAtDemo {

	public static void main(String[] args) {
		String s = "Nitish";
		System.out.println(s.charAt(2)); //t
		System.out.println(s.charAt(20)); // java.lang.StringIndexOutOfBoundsException: String index out of range: 20
		
	}
}
```
2. public String concat(String s)
```
public class MethodConcatDemo {

	public static void main(String[] args) {
	   String s = "Nitish";
	   s = s.concat("Yadav");
	   s = s + "Yadav";
	   s += "Yadav";
       System.out.println(s);
	}
}
```
3. public boolean equals(Object o) ->To check equality of string objects
```
public class MethodBooleanEqualsDemo {

	public static void main(String[] args) {
		String s  = "NITISH";
		System.out.println(s.equals("nitish"));//false

	}
}
```
4. public boolean equalsIgnoreCase(String s) -> where case is ignored
```
public class MethodBooleanEqualsDemo {

	public static void main(String[] args) {
		String s  = "NITISH";
		System.out.println(s.equals("nitish"));//false
		System.out.println(s.equalsIgnoreCase("nitish"));//true

	}
}
```
5. public boolean isEmpty()
6. public int length() for string but for array we have length variable
```
public class MethodIsEmptyDemo {

	public static void main(String[] args) {
		String s = "";
		String m = "Nitish";
		System.out.println(s.isEmpty()); //true
		System.out.println(m.isEmpty());//false
                System.out.println(m.length()); //6
                //but for array we have length varible 
		int[] x = {10,20,30,65,73};
		System.out.println(x.length);//5	

	}
}
```
7. public String replace(char Old,char new)
8. public String substring(int begin) -> from begin index to end of String
9. public String substring(int begin, int end) -> from begin index to end-1
10. public int indesOf(char ch); ->will return the first occurance of any character only.
```
public class MethodCharReplaceDemo {

	public static void main(String[] args) {
		String s = "ababababa";	
		System.out.println(s.replace('a','b'));
                String b = "abcdefg";
		System.out.println(b.substring(3)); //from 3rd index to end //defg
                System.out.println(b.substring(3,5));//from 3rd to end-1 //de
                System.out.println(b.indexOf("d")); //3
	}
}
```
11. public String toLowerCase();
12. public String toUpperCase();
```
public class MethodLowerUpperDemo {

	public static void main(String[] args) {
		String s = "super";
		System.out.println(s.toUpperCase());
		String t = "HAPPY";
		System.out.println(t.toLowerCase());

	}
}
```
---
**Trim() method**
- public String trim(); ->if there is any spaces at the begining of string or end of string than it will be removed but not at the middle of the String.
```
public class MethodTrimDemo {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("Enter your city name:");
		String name = sc.nextLine().toLowerCase().trim();
		if(name.equals("hyderabad")) {
			System.out.println("Hello Hyderbadi, Adaab..");
		}else if(name.equals("chennai")) {
			System.out.println("Hello Madrasi, Vanakkam..");
		}else if(name.equals("bangalore")) {
			System.out.println("Hello kannadiga, Namaskara..");
		}else {
			System.out.println("Please enter valid city name");
		}
	}
}
```
---
Once we create a string object you are not allowed to make any changes in that object ,if we are trying to perform any changes in that object than new object is created.
```
public class ConceptDemo {

	public static void main(String[] args) {
		String s1 = new String("nitish"); //2
		String s2 = s1.toString();//0
		String s3 = s1.toLowerCase(); //0
		String s4 = s1.toUpperCase(); //1
		System.out.println(s1==s2);  //true
		System.out.println(s1==s3);  //true
		System.out.println(s1==s4);  //false

	}
}
```
---
**Final vs Immutablity**
- How to make StringBuffer as immutable -> making reference variable as final - No it is different.
- Final = if you dont want to perform reassignment to an variable.
- Immutable = if you dont want to perform any changes to the object.
```
public class FinalVsImmutableDemo {

	public static void main(String[] args) {
         final StringBuffer sb = new StringBuffer("nitish");
         sb.append("Yadav");
         System.out.println(sb);
         sb = new StringBuffer("Kumar"); //will give error as final cant be assigned.
	}
}
```

Amount this which of the following are meaningful?
- final variable✔️
- final object❌
- immutable Variable❌
- Immutable object✔️
---
**StringBuffer**
- If the content is not fixed and keep on changing never recommended to use String concept,to handle this requirement we are recommended to use StringBuffer.
- In the case of StringBuffer you can add something in the character that is known as capacity i.e amount of character it can hold. and the character present is known as length.
- Example - Room - 20 students present = length
                 - 100 students can accomodate = capacity

Important constructors of StringBuffer:
- StringBuffer sb = new StringBuffer();   capacity->16 , if new element added than new capacity=(CC+1)*2=34
```
public class StringBufferCapacityDemo {

	public static void main(String[] args) {
		StringBuffer sb = new StringBuffer();
		System.out.println(sb.capacity()); //default -16 
		
		sb.append("a bus is moving");
		System.out.println(sb.capacity());  //default -16
        sb.append("ra");
		System.out.println(sb.capacity());  //capacity -34
                StringBuffer sb1 = new StringBuffer(1000);
		System.out.println(sb1.capacity());
	}
}
```
- StringBuffer sb = new StringBuffer(int intialcapacity);
- StringBuffer sb = new StringBuffer(String s);

Methods in SpringBuffer ->
- public int length();
- public int capacity();
- public char charAt(int index);
- public void setCharAt(int index,char newChar);
- public StringBuffer append(String s);
- public StringBuffer insert(int index,String s);
- public StringBuffer delete(int begin,int end); -> delete char from beg to end-1.
- public StringBUffer deleteCharAt(int index);
- public StringBuffer reverse() ->only order is reversed; System.out.println(sb2.reverse());
- public void setLength(int length); only char= length will be considered.
- public void ensureCapacity(int capacity)->if want to increase the capacity dynamically than we require this method.
- public void trimToSize(); ->to deallocate extra memory.

**Every method in StringBuffer is synchronised, at a time only one thread is allowed to work at a time i.e Thread Safe.**
---
**StringBuilder**
why - Every method in StringBuffer is synchronised, at a time only one thread is allowed to work at a time.Threads are executed one by one which will increase the waiting time of the thread which will decrease the performance of the applicacation.
- To overcome this problem in 1.5 V String Builder came.
- Changes in StringBuilder comparison to String buffer
- Buffer -> Builder
- Synchronized keyword ❌❌ removed
---
![image](https://github.com/user-attachments/assets/2f4d9bb4-e39d-483b-9acc-2a3e825a0268)
---

**Method Chaining**
sb.m1().m2().m3()......
