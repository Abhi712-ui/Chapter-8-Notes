# Classes (Unit 8)
---
## A "Brief" Introduction to OOP
 - OOP is a different way of thinking about 
problems
 - Requires thinking about the "objects" involved in the 
problem, their "state", and their "behaviors" or verbs 
that the objects can do
 - Write it all down – see UML diagrams

**This planning drives the organization of your code**
 - the files that make up your project
 - the variables that hold onto the state of each object
 - the methods that create the object's behaviors

---
## Classes and Objects
**Classes define everything about an object**
 - Information about it (its state/variables)
 - Behaviors (methods and constructors)
 - Real world analogies for classes?
**Multiple objects can be created from a Class**
 - You "bring them to life" or instantiate them using one of 
the constructor methods
---
## Classes (Again)
**Classes allow us to encapsulate behavior and state that could be useful for the future**
 - We have been using classes for some time now:
 - `PrintStream, String, Scanner`
 - We have actually been declaring classes all along!
 - `public class MyClass { ... }`
---
## Class Definition
**Classes are defined using the `class` keyword:**
```
public class <class-name> {
	<variables>
	<methods>
	}
```
**Remember our rules/conventions:**
 - Letters, digits, underscores only
 - Start with letter
 - But, class names begin with a **capital** letter
 - Use another capital letter for each new word
 - e.g. `Date`, `MixedFraction`, `TicTacToeBoard`

***Classes consist of three components:***
**Methods**
 - Provide class behavior
 - Defined just like we have been, except don't use `static`
**Constructors:** *Special Methods*
 - Define how to create *Instances* of a class
 - Really a special case of methods
**Variables**
 - Store Class State
 - Declared Like Normal, but use `private` instead of the usual no modifier
 - Variable scope should be the entire class - All Methods can see the variables that you declare at class level
---
## Access Control

**We’ve been using public in a lot of places**

**`public`** is a Java ***access specifier***
Others are **`private`** and **`protected`**
**Access specifiers** tell Java who should be able to see and use the class/method/variable we’re defining

Now that we’re defining classes, we’ll start using **`private`** for some things
Like with variable names, there are no rules about this, just conventions

**We’ll use the following conventions:**
 - Almost all fields will be **`private`**
 - Almost all constructors will be **`public`**
 - Methods will be **`public`** if other classes will want to use them, and **`private`** otherwise
![Modifiers](Modifiers.PNG)
---
## Classes Cont.

```
public class Movie {
	// Variables (Fields)
	private String title;
	private String[] actors;
	
	// Constructors
	public Movie(String title) { ... }
	public Movie(String title, String[] actors)  {... }

	// Methods
	public String getTitle() { ... }
	public String[] getActors() { ... }
	public String getLeadActor() { ... }
	public void setTitle(String newTitle) { ... }
	public void addActor(String actor) { ... }
	public boolean isInFilm(String actor) { ... }
	}
```

---
## Accessor Methods
**Because we declare our variables as `private`, others cannot access them**

```
Movie megamind = new Movie(“Megamind”);
System.out.print(megamind.title); // won’t work
```
**Instead, we use accessor methods to provide access to the data**

***This provides a layer of abstraction over our data***
Simple accessor methods typically names of the form getVariable and don’t take arguments

```
// simple accessor method
public String getTitle() {
	return title;
}

// another simple accessor method
public String[] getActors() {
	return actors;
}
```

 - We can also provide accessor methods for data for which we don’t store a variable
 - This is another reason we use methods instead of direct variable access
 - These getters are named similarly, but do not have a corresponding variable
```
public String getLeadActor() {
// lead actor always stored first in list
	return actors[0];
}
```

 - Modifier Methods are the analog of getter Methods
 - They are used to set The value of a variable
 - Modifier methods typically have names of the form **`setVariable`**, have a void return type, and take a single argument of the relevant type
 - We can also define modifier methods that don’t simply set a variable, but modify something more complex

```
// simple modifier method
public void setTitle(String title) {
	this.title = title;  // we'll get to this. soon
}

// modifier method
public void addActor(String actor) {
	String[] newActors = new String[actors.length + 1];
	for (int i = 0; i < actors.length; i++) {
	    newActors[i] = actors[i];
	}
	newActors[actors.length] = actor;
	actors = newActors;
}
```

We can also provide any other methods we might want or that might be useful
These other methods will use our variables, and can possibly call other methods

```
public boolean isInFilm(String actor) {
	for (int i = 0; i < actors.length; i++) {
	    if (actors[i].equals(actor)) {
	        return true;
      }
	}
	return false;
}
```
 - Constructors are defined just like other methods, but with no return type or value
 - Constructors can be overloaded, just like other methods

```
public Movie(){
	title = "tbd";
}
public Movie(String title) {
	title = title;
}
public Movie(String title, String[] actors) {
	title = title;
	actors = actors;
}

```
These constructors won’t work– why not?

---
## This Keyword
 - We can access the current object by using the `this` keyword
 - In a constructor, this is the object being created
 - In any other method, this is the target of the method call

```
public Movie(String title) {
	this.title = title;
}
public Movie(String title, String[] actors) {
	this.title = title;
	this.actors = actors;
}
```

---
## The `To String` Method

 - You can add a `.toString()` method to any Class you create
 - It's job is to create a String that represents whatever you choose for the object
```
public String toString(){
return this.lastName + ", " + this.firstName;
}
```

 - Java automatically looks for `.toString()` when you try to print an object
 - `return this.x + ", " + y;`

---
## Pierson can't cook
 - Think about the problem you're trying to solve, and the object(s) involved
 - Add a class file for each object to your project
 - Name it in the singular, not plural (Book, not Books)
 - Add the private variables to store state info
```
private int score;
private String[] shopping list;

```
 - Add the constructor(s)
```
public Book(parameter list with data types){
this.param1 = param1;  //etc.
```
 - Add the getters/setters
```
public String getScore(){
return score;
}
public void setScore(int score){
	this.score = score;
}

```

 - Add other methods to do actions needed for the object, decide if they need parameters and/or return values
---
## Class Methods

 - So far, all the OOP methods we’ve defined have been instance methods
 - The method corresponds to a particular instance of the class
 - There is another type of method, called a class method (that we we've been using all along before OOP)
 - Class methods do not relate to a particular instance– they belong to the class as a whole
 - Class methods are declared just like instance methods except:
 - They are preceded by the static keyword
 - They cannot call any instance methods or access any instance variables

```
public static Movie readFromInput() {
    Scanner kb = ...;
    System.out.print(“Enter a movie title: ”);
    String input = kb.nextLine();
    Movie newMovie = null;
    if (!input.equals("")){
	newMovie = new Movie(input);
       String actor = null;
       do {
           System.out.print(“Enter an actor, or press Enter to finish: “);
	    actor = kb.nextLine();
           if (actor != null){
               newMovie.addActor(actor);
           }
       } while (actor != null);       
    }
    return newMovie;
}

```

```
public static void main(String[] args) {
    	Scanner kb = ...;
	System.out.println(“How many movies in your library?”);
	int numMovies = kb.nextInt();
	Movie[] library = new Movie[numMovies];
	for (int i = 0; i < numMovies; i++) {
		library[i] = Movie.readFromInput();
	}

	System.out.println(“In your library you have:”);
	for (int i = 0; i < library.length; i++) {
		System.out.print(“\t”);
		System.out.print(“\”” + library[i].getTitle() + “\””);
		System.out.print(“ starring ”);
		System.out.print(library[i].getLeadActor());
		System.out.println();
	}
}
```

---
## Class Variables

 - Class variables don't belong to an instance
 - This is similar to class methods
 - They are declared as static
 - Used when you want to keep track of a value across all instances

 - We have a `Dog` class for registering dogs
 - We can create a `dog` instance:
`Dog mydog = new Dog();`
 - Instance variables don't use the static keyword, belong to an instance: `mydog`
`int age, String breed, String owner, int idNum, etc.`
 - Class variables use the static keyword, and don't belong to any instance:
`nextIdNum`  `// used to keep track of the next ID number to hand out`
 - Instance methods don't use the static keyword:
`mydog.run()`, `mydog.getBreed()`, etc.
 - must be called on an instance of Dog like `mydog`
 - Static methods use the static keyword, don't belong to any instance
 - don't affect or change an instance
 - called using the class name: `Dog.resetCounter();`
 - The constructor sets idNum using nextIdNum
`idNum = nextIdNum;`
`nextIdNum++;    // increments it for the next dog`

 - The number 30 in the original method is called a magic number
 - A number literal that has no context
***Magic numbers are bad for a couple reasons:***
 - Poor documentation
 - Potential for bugs if value changes
*Especially* if the value is used in multiple places
 - We avoid magic numbers by defining constants
 - A constant is a variable whose value cannot change once it has been assigned
 - REMEMBER: Constants are defined using the final keyword:
 ```
 public boolean isFull()
	final int MAX_CLASS_SIZE = 30;
	MAX_CLASS_SIZE = 35;		// won’t compile
	return (students.length > MAX_CLASS_SIZE); 
}

 ```
 
 Constants are typically named in **ALL_CAPS**
Constants follow normal scope rules for variables

We can also (and usually) define constants at the class level:

```
public class HighSchoolCourse {
	...
	public static final int MAX_CLASS_SIZE = 30;

	public boolean isFull() {
	    return (students.length <= MAX_CLASS_SIZE); 
	}
}
```

 - Class constants are typically declared as public and static (and final)
 - Class constants can be initialized either at the declaration of the class or in the constructor (but not both)
 - Class constants cannot be initialized or assigned anywhere else

 







 




 


 






















 
   