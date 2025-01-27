f**String**
- In any java project in 1000 objects , over 900 are string object.
- String objects are immutable,StringBuffer objects are mutable.
- immutable means non-changeable i.e. you cant change.
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
```
public class MethodCharReplaceDemo {

	public static void main(String[] args) {
		String s = "ababababa";	
		System.out.println(s.replace('a','b'));
                String b = "abcdefg";
		System.out.println(b.substring(3)); //from 3rd index to end //defg
                System.out.println(b.substring(3,5));//from 3rd to end-1 //de
	}
}
```
