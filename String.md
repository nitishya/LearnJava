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
