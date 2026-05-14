#### A java source file:
- Contains at most one package statement
	- Which must come first
- Contains any number of `import` statements
	- Which must come after all `import` statements
- Declare types after all import statements
- Has a name that matches the base name of any public type it contains
	- hence can contain at most one public type

#### A top-level type can be
- a class which can be
	- "regular", sealed, non-sealed, or final
- an abstract class
- an enum
- a record
- an interface
- an annotation

#### A class declaration has an overall form
```Java
<modifiers> class <ClassName> 
	[generalizations] [permits clause] {
	<body>	
}
```
- Acceptable `<modifiers>` depends on specifics of the class
- The `<ClassName>` must be a valid identifier, unique among the types in the current package
- `[generalizations]` can be extends and implements clauses on `class` types.
- A `[permits clause]` is only used for sealed types

#### Modifiers for Class Declarations
There are nine possible modifiers for a class, but not all can be used in all situations and combinations
- Annotations
- `public` - may be used on top-level and member classes but not for local or anonymous classes
- `protected, private` - may only be used on member classes
	- At most, one of `public, protected` and `private` may appear
- `static` may be used on member classes.
- An `abstract` class must not prevent creation of valid concrete subtypes
	- Therefore it must not be `final`
	- Its methods, including abstract ones, must validly coexist
	- The name of an abstract class may not follow `new`
- At most one of `sealed, non-sealed`, or final may appear
	- A `sealed` type must (perhaps implicitly) declare the children it permits
	- Local types cannot be `sealed` or `non-sealed`
	- A `non-sealed` type must have a parent type that is `sealed`
- The modifier `strictfp` is obsolete

#### Top-level Class Declarations
A regular or abstract class declared at the top-level of a source file can contain
- static an instance fields
- static an instance methods 
- static an instance  initializers
- constructors
- static and instance classes
	- Static classes are called "nested"
	- Instance classes are called "inner"
- implicitly static enums
- implicitly static records 

#### Top-level Class Declarations
In terms of what they can contain
- Abstract classes, enum types, and recxords are classes
	- Records can have their own restrictions and syntax
- Annotations are interfaces
- Interfaces are abstract in nature
- Abstract things
	- cannot be final
	- can contain abstract methods
- Interface types have some unique rules too
- Their fields and types can only be static, and are so by default

##### What happens?
```Java
package scr;
public class DoThat {
}

public class TryThis {
}
// End of file: scr/TryThis.java
```

Answer: Fails to compile
Two public types: The file name cannot match both

##### Describe x
```Java
interface Thing {
	int x = 99;
}
```
Answer: x is implicitly public, static and final

```Java
public final abstract class Thing {
	public void doStuff() {
		System.out.println("Hello from abstractland!");	
	}
}
```
Answer: Compilation fails
An abstract class cannot be final

##### What happens?
```Java
public class TryThis {
	static {System.out.println("Hello");}
	{System.out.println("Hello");}
	
	static class A{}
	class B{}
	
	static enum X {}
	static interface Y {}
}
```
Answer: Compilation succeeds
(Inner enums and interfaces are implicitly static, so those modifiers are redundant )