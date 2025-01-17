Java Source File Structure :
 1. We can Take any number of classes
 2. A java program can contain atmost 1 public class.
 3. Any class which is public the program is named on that class name
 4. If a program contain many classes and each classes have main method than that main method is called on compiling that class
    if class doesnt contain main method it will give error.
 5. If we run program name by any name when public class is present it will give error.
 6. Inside any java program atmost 1 package statement is allowed.If you are taking more than 1 package statement than compiler will give error.
---
SO the oreder will be like this 

Package Statement     -- Atmost 1
import statement      -- Any number 
class/interface/enum  -- Any number 

---
*** Class Level Modifiers ***
  1. MOdifier describe the behavior of the class
  2. If the class is public you can access this class from anywhere within the package , outside the package no restrictions at all.
  3. If the class is abstract than object creation is not possible.
  4. If the class is final,Child creation is not possible

**Top Level Class Modifiers**
- public
- default
- abstract   (important)
- final
- strictfp

But for inner level class Modifiers are - 8
- public
- default
- abstract
- final
- strictfp
- private
- protected
- static

Public - It is accessible in same package as well as outside the package also
Default - If a class have no access modifier means it can be only accessible in the same package and we cant access the class outside the package.

**Abstract**
1. Abstract modifier are applicable for methods ✔️
2. Abstract modifier are applicable for class ✔️
3. Abstract modifier are not applicable for variable ❌

Abstract Methods 
- If we dont know about implementation we can declare that method as abstract.
- Abstract method have only declaration not implementation.So it ends with semicolon not with curly braces.
- Child class is responsible for its implementation.

**Which will give error?**
1. public abstract void m1(){}; ❌
2. public void m1(); ❌
3. public abstract void m1(); ✔️
4. public void m1(){}; ✔️

Abstract Class
- Sometimes when class implementation is not complete such type of partially implemented/completed class we have to declare it as Abstract.
- Noone is allowed to create its object.
- Noone can call its methods
- **For Abstract classes object creation is not possible.**
```
package oopsConcept;

public abstract class AbstractClassDemo {

	public static void main(String[] args) {
		AbstractClassDemo d = new AbstractClassDemo();
   //Cannot instantiate the type AbstractClassDemo
	}
}
```
**Abstract class vs Abstract method**
1. If a class contain atleast one abstract method than definitely that class should be declared as abstract.
2. We can declare a class abstract even if it don't contain any abstract method.
3. For every method in the abstract class the child class should provide implementation.

Member Modifier ->
- public : can acess it anywhere within same package outside package within class outside class.
- If a member is public then it accessible but make sure its class is also public than only you can access it outside the class.
- If a member declared as default we can acess that only in current package.
- If a memeber declared as private than it is acessible only in the same class.

- **Data Members : variable should be private**
- **Methods : public -> Make it accessible by the public for services**
- Protected : within the current package anywhere you can access but from outside package only in the child class.
- Protected member outside package you can acess only in the Child classes and compulsory we should use child class reference only.

**PRIVATE < DEFAULT < PROTECTED < PUBLIC**

---
**Interface**
- Any service requirement specification(SRS).
- Any contract between client and Service Provider.
- 100% pure abstract class.❌ after 1.9 version
```
interface Interf {
  public void m1();
  public void m2();
}

class ServiceProvider implements Interf{
 public void m1(){ }

 public void m2(){ }
}
```
- While overriding we can not reduce the scope of method.
- Whenever we are providing implementation for each and every abstract method.


**OOPS CONCEPT**
1. Data Hiding
   - Outside person should not acess our internal data directly.
   - By declaring member private we can achieve data hiding.And can get 
     using public methods.
   - Advantage : Security

2. Abstraction
   - Hiding internal implementation and highlight the set of services that is offered.
   - Advantage : Security
   - Advantage : ENhancement become easy.
   - Advantage : Maintainability improved.
   - Advantage : Modularity improved.

3. Encapsulation
   - Grouping data members and corresponding methods into a single unit is 
     called encapsulation.
   - Data Hiding + Abstraction
   - Hiding Data behind methods is the concept of Encapsulation.
   - declare every data members as private and provide getter and setter 
     for every data member.
   - ADvantage: Security
   - Advantage : Enhancement becomes easy
   - Advantage : Maintainability become easy
   - Disadvantage : Increase in code length -> Performance down- as we need 
     getter setter for every data member and validation is required for 
     every data member.

**Tightly Encapsulated class**
- If and only if every variable present inside the class is private than 
  such type of class is said to be tightly encapsulated.
4. Inheritance
   - IS-A Relationship
   - Code Reusability
   - extends keyword
   - Whatever member parents have we can use it in child class we are not 
     required to redefine it.
   - Whatever method in child class is not available to parent class.
   - Parent reference can be used to hold child class object but by using 
     that reference we can't call child specific method.
   - Child reference can't be used to hold parent object.


  **Super class of all java classes is -> OBJECT**
