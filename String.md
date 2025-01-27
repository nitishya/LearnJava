**String**
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
	

