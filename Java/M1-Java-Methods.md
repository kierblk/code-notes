# Module 1: Java Methods

To be able to create large programs, we have to be able to break the job down into small, manageable parts.

The process of breaking a task down into smaller parts is called "procedural decomposition", and almost programming languages provide a way to do this. Java does it using what it calls "methods".

In general, you should break your program up into methods when:

- You can break a task into distinct non-trivial subtasks in order to understand it better. For example:

  	Fly airplane
  	1. Take off
  	2. Fly
  	3. Land

- You could even break one or more subtasks down further:

	Fly airplane
	1. Take-off
   		1. Push back from gate
   		2. Taxi to runway
   		3. Increase speed until off ground
   		4. Climb to cruise altitude
	2. Fly
	3. Land

- You have "redundant code": unnecessarily repeated code that appears more than once in your program. It’s OK to use methods to eliminate redundancy for even a single, complicated line. That way if you ever have to change it, you only have to change it in one place!

- Your method is getting bigger than 20-30 lines of code; look for groups of statements that are related pull them out into a method.

When you decompose a program into methods, examine each method to make sure it is doing a single, specific thing – not a random collection of unrelated things. Try to capture what the method is doing in a few words like we did in the airplane example above. If you can’t describe your method's task in a few words, maybe it needs to be broken down further.

Ideally, once you have organized your program with methods, your main method turns into a list of method calls, each that handle their own small piece of the task to be performed. Thus your main method turns into a sort of outline of what your code is doing, making it easier for someone reading your code to quickly understand what it does.

## Method Names

Every method in a Java program has its own name. In Hello World, the single method’s name was main:

`public static void main (String[] args) {`

**main** is a special method name in Java – it’s the method Java will use to execute your program. Since this is a special method, you cannot use the name "main" for any of your other methods.

As the purpose of a method is typically to accomplish a task, it's a good idea to start a method’s name with a verb: calculate, report, print etc... Followed by whatever item that task is performed on: calculateAge, reportResults, printSummary etc...

The Java convention is for method names to start with a lower case letter, and use uppercase letters to start each following word with no spaces.

**Remember:** Methods start with a lower case letter while classes start with an uppercase letter.

## Writing a Method

The first line of a method is called the "method header" and it contains some specific keywords:

`public static void myMethod() {`

Within the curly braces will be the method statements (what your method actually does).

## Calling a Method

To actually run the code inside a declared method, you need to **call** or invoke the method by name.

Each method invocation statement starts with the name of the method you want to execute, followed by a pair or parentheses finishing with a semicolon. Example:

```Java
public static void main(String[] args) {
   takeOff();
   fly();
   land();
}

public static void takeOff () {
   pushBackFromGate();
   taxiToRunway();
   increaseSpeedUntilOffGround();
   climbToCruiseAltitude();
}
```




