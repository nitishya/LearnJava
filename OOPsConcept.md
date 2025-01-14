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
