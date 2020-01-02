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

Java is a strictly typed language. 

In Java, a String is any sequence of characters – letters, digits, spaces, punctuation, and other “special characters”.

| String         | Explanation                                                                                                                                                                                                                                  |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| "Hello, World" | You used this String in the previous section! It has 12 characters. The space between the comma and “w” is also counted as a character. The double quotes are not part of the String, they define where the String starts and where it ends. |
| "1234"         | This is a String, not an integer number because it’s enclosed in double quotes.                                                                                                                                                              |
| "!"            | This String is just a single character: an exclamation point.                                                                                                                                                                                |
| "><}{_^$#@^"   | This is a String with 10 special characters in it.                                                                                                                                                                                           |
| ""             | This is a special String: an “empty String” that contains NO characters at all. The two double quotes are right next to each other, without even a space between them.                                                                       |

### Escape Sequences

| escape  sequence | Name         | Example           | String as printed |
|------------------|--------------|-------------------|-------------------|
| ""               | Double Quote | John \"JJ\" Doe | John "JJ" Doe     |
| \                | Backslash    | Use \\, not /   | Use \, not /      |
| \t               | Tab          | 1\titem         | 1    item         |
| \n               | New line     | line 1\nline 2  | line 1   line 2   |


### Printlns

To produce string based output, we use the *println statement*.

Java prints text to the console using a `System.out.println` statement.

Example:

`System.out.println("Hello, world!");`

It’s kind of wordy, but the words do make sense in a way:

- **System** essentially refers to the computer as a whole
- **out** refers to the standard output device: the console
- **println** indicates that you want to “print” as a complete line (ln) of text

Our statement above will print `Hello, world!` to the console area on your screen. It also advances to the next line on the display, just as if you typed it and then hit the Enter (or Return) key.

You can also use the println statement to produce an empty line.

`System.out.println();`

### Prints

Sometimes you may want to use several print statements and have all the output produced on the same line. For this, you can write print instead of println. For example, these statements:

```Java
System.out.print("Hello, ");
System.out.print("Joe");
System.out.print("! Hello, ");
System.out.print("Jane");
System.out.println("!");
```

…would print out:

`Hello, Joe! Hello, Jane!`

… and advance to a new line only after the last exclamation point. That is because you can see that the first 4 calls leave off the "ln" at the end of print. These are simply "prints" instead of "print lines" and do not add the carriage return or "Enter" at the end of a line of output.

Finally, you can also print multiple lines with a single println statement by using the new line escape sequence from above:

```Java
System.out.println("line 1\nline 2\nline3");
```

… prints out these three lines:

```
line 1
line 2
line 3
```
