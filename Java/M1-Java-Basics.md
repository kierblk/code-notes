# Module 1: Java Basics

Mod 1 covers:

- Writing your first Java program
- The different parts of a Java program
- Printing text to the console
- Organizing your code using methods
- How Java views and stores basic types of data
- Different methods of manipulating data
- How to create programs that allow a user to interact with the software

----

Java is an Object-Oriented Language, a compiled language, and has memory management.

Released in 1996 by Sun Microsystems, and in 2010 Oracle acquired Sun.

## Naming conventions

Java is case sensitive. `MyClassName` != `myclassname`.

Java uses camel casing, where you capitalize the first letter of every word with no spaces between words.


## Hello World 

```Java
public class HelloWorld {
   public static void main(String[] args) {
      System.out.println("Hello World");
   }
}
```

## Anatomy of a Java Program


### 1. Class - the outermost layer of the program

This always starts the same way, with the keywords `public class`

```Java
public class HelloWorld {
}
```

The class name, here `HelloWorld`, will ALWAYS be the same exact name as the file name.

### 2. Main Method - the wrapper that tells your computer which lines of code to run.

In Java, this has a very specific set of keywords: `public static void main(String[] args){}`

Between the curly braces are lines of code you wish to run. 

Indentation is a readability convention.

### 3. Statements - the lines of code you wish to run

Each line within the main method is called a "statement" and should end with a semi-colon.

You can have as many statements as you want. The computer will run each line from top to bottom, one after another. 

These are indented from the main method for readability.

## Comments

It is recommended that you add comments...

- at the top of any Java class to describe its overall function
- at the top of a "method" or a small subsection of code to help explain its contribution to the overall solution
- to explain what is happening when you have particularly complicated bits of code
- to isolate lines of code when looking for issues without having to delete code

There are two different ways to add comments

1. Single line comments

	`// comment text, on one line`

2. Multi line comments

	```Java
	/* comment text
	You can have as many lines as you like
	Between these two indicators 
	*/
	```
## Strings and Printlns

