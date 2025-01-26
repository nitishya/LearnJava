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
