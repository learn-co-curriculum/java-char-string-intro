# Characters and Strings

## Learning Goals

- Define character encoding as ASCII and Unicode values
- Discuss escape sequences
- Compare character array and string representations in memory

## Introduction

So far, we have seen the `char` data type reference in passing, and we know it
stores a single character or ASCII value, but we really haven't used it or
talked too in-depth about it. In this section, we will explore characters some
more, talk about what an ASCII value is, point out a few special characters,
and explain how it might relate to the `String` class.

## The `char` data type

A `char` is a primitive data type that stores a single character or an ASCII value.
Let's explore what "ASCII value" means.

`char grade = 'A';`

The above code is how we would declare a variable named `grade` to store a `char` value,
and then assign an initial value by enclosing the character in single quotes, such as 'A'.

Since everything in memory is stored as a binary value, we need to
convert the letter 'A' into some type of numeric value in order to store it.
**ASCII** is a standard for encoding characters as decimal values.
An **ASCII Table** is a tabular representation that links characters to decimal
values. We can see what each letter represents using the ASCII table below. We can
also see that the uppercase characters have different values from the lowercase
letters. This means that 'A' would not be the same as 'a' in Java!

![ASCII Table](https://curriculum-content.s3.amazonaws.com/java-mod-2/chars-and-strings/ASCII-Table.png)

[Medium: ASCII Table in Java Programming](https://medium.com/@aidafarihabaharunsuratman/did-someone-actually-use-ascii-table-in-java-programming-9710a65c6ed9)


Let's consider our example again: `char grade = 'A';` We can see in the ASCII
table that the character 'A' has a decimal value of 65. Does this mean, that if
we set `char grade` to the number 65 that it would be the same as setting it to
'A'?

```java
public class CharExample1 {

   public static void main(String[] args) {
      char firstGrade = 'A';
      char secondGrade = 65;
      if (firstGrade == secondGrade) {
         System.out.println("Wow! 'A' is the same as 65!");
      } else {
         System.out.println("Told you 'A' wasn't the same as 65!");
      }
   }
}

```

The output to the code above is:

```text
Wow! 'A' is the same as 65!
```

Let's set a breakpoint at the first line in the `main` method and debug the code.
Step over the first two assignment statements to see the values
stored in `firstGrade` and `secondGrade`.  The Java Visualizer shows both
storing the character 'A':

![visualizer character A](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/char_decimal_visualizer.png)

The debugger view is interesting because it shows both the character 'A' and the decimal
value 65.  Keep in mind the actual value stored in memory is a single binary number
representing of the decimal value 65.

![debugger character A](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/char_decimal_debugger.png)


As we can now see, the definition of a `char` data type makes more sense when
we say "stores a single character or an ASCII value" since we could set it to
either a numeric value or use single quotes to wrap a character! For readability
in Java, we tend to set `char` data types to the characters using single quotes
instead of using the decimal values. In other words, `char grade = 'A';` is
preferred over `char grade = 65;`.

## Comprehension Check

<details>
    <summary>Look at the ASCII table. What is printed when the code shown below executes?</summary>

  <p>Answer: p</p>
  <p>The decimal value 112 is equivalent to the character 'p'. </p>

</details>

<br>

```java
public static void main(String[] args) {
    char letter = 112;
    System.out.println(letter);
}
```

<details>
   <summary>Look at the ASCII table. What is printed when the code shown below executes?</summary>

  <p>Answer: false.</p>
  <p> The character 'k' is equivalent to the decimal value 107, which is not within the range of 100 and 105.</p>

</details>

<br>

```java
public static void main(String[] args) {
    char letter = 'k';
    boolean inRange = 100 <= letter && letter <= 105;
    System.out.println(inRange);
}
```


<details>
   <summary>Look at the ASCII table. What is printed when the code shown below executes?</summary>

  <p>F<br>G<br>H<br>I</p>
  
</details>


```java
public static void main(String[] args) {
    for (char c=70; c<74; c++){
        System.out.println(c);
    }
}
```

## Unicode

Older programming languages like C or C++ use ASCII to store
a `char` in memory as a 2 byte decimal value based on the ASCII standard.
ASCII uses 8 bits and can represent only 255 characters.
Java uses a more recent standard called "Unicode".  Unicode was initially designed
to store 16 bits and could represent 65,536 characters. Unicode's first 255 characters are the same as ASCII.
But even 16 bits is not enough to represent all characters used in the world,
so Unicode was extended to 32 bits and can represent over one million characters.
However, Java still uses only 16 bits to represent a character, so characters
outside this range are called **supplemental characters** and require a pair
of `char` values.


## Escape Sequences

Java also has several special characters. These special characters can be
accessed using the backslash character '\', also known as the **escape**
**character**. Whatever follows the escape character is known as an
**escape sequence.**

For example, if we want to use a double quotation mark within a `String`, we
can use the escape sequence `\"`. The backslash escapes the double quote and in
turn, tells Java that we are to use the double quote within the `String` and not
end the `String` (since we usually wrap `String` values in double quotes). Let's
look at an example of this:

```java
System.out.println("\"You must be the change you wish to see in the world.\" - Mahatma Gandhi");
```

Output:

```text
"You must be the change you wish to see in the world." - Mahatma Gandhi
```

Notice how the backslashes are not printed but the double quote immediately
following the backslash is printed. This is because the escape character
notifies Java that we are to print the escape sequence instead that results in
just a double quotation mark. Java also treats the escape sequence as one
character - meaning `\"` would be considered one character, not two.

Consider the table of escape sequences:

| Escape Sequence | Display      |
|-----------------|--------------|
| `\t`            | Tab          |
| `\n`            | New Line     |
| `\'`            | Single Quote |
| `\"`            | Double Quote |
| `\\`            | Backslash    |

A few notes on the escape sequences: The tab and new line characters are
representatives of whitespace. Consider the example below of how to use these
characters:

```java
String firstString = "Hello\tWorld!";
String secondString = "What a beautiful\nday!";

System.out.println(firstString);
System.out.println(secondString);
```

Output:

```plaintext
Hello   World!
What a beautiful
day!
```

We can see in the above output that when we placed the character `\t` between
"Hello" and "World!", it placed a tab or an indent between the two words. In the
`secondString`, we place a `\n` character between the words "beautiful" and
"day!". When we print that to the screen, it will actually write the word "day!"
on a new line separate from "What a beautiful".

## Strings and Character Arrays

A variable declared with data type `String` stores a sequence of characters.

A `String literal` is a sequence of characters surrounded with double quotes,
such as "Hello" or "123 Main St".

A sequence of characters can be treated as a single unit... and that is
where the `String` data type comes in. But we also learned about arrays. So
wouldn't an array of characters be the same thing as a `String`?

The answer is: no - but pretty close!

In Java, there are a few differences between a `String` and a `char[]`:

1. A `String` is a sequence of characters where a `char[]` is a collection of
   `char` data types. In a `char[]`, each element could be treated independently
   and separately. For example, we could have a character array of grades:  
   `char[] grades = {'A', 'B', 'C', 'D', 'F'};`    
   Since it is an array, we can
   change the element at a particular position in the array. For example, we can
   reassign the first element as `grades[0] = 'Z'`;
2. A `String` is an immutable type whereas a `char[]` is still mutable.
   We can't change any of the characters stored in a string, we would need to create an
   entirely new string.
3. We can use a `+` to concatenate two `String` values together but cannot do
   the same for a character array.
4. The `String` class has built-in methods that we will cover in the next couple
   of lessons. But a `char[]` does not have any built-in methods; however, we
   can pass it in as a parameter to the `Arrays` class as we saw with the method
   `Arrays.sort()`.


Let's see what memory looks like when it stores a character array versus a `String` class instance.

```java
public class StringExample1 {
    public static void main(String[] args) {
        char[] gradesAsCharArray = {'A', 'B', 'C', 'D', 'F'};
        String gradesAsString = "ABCDF";
        System.out.println(gradesAsCharArray);
        System.out.println(gradesAsString);
    }
}
```

We can use IntelliJ's  debugger to compare the character array assigned to the variable `gradesAsCharArray`
with the `String` object assigned to the variable `gradesAsString`:


![character array vs string](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/chararray_vs_string.png)

The `gradesAsCharArray` stores the array of characters as ASCII decimal values
(notice the number next to each character ('A' is 65, etc).

The  `String` object referenced by `gradesAsString` has many fields
(`value`, `coder`, `hash`, etc), with the `value` field storing
the character sequence as unicode values (65, 66, etc).

While a character array is stored differently than a `String`,
there is a way for us to convert a character array into a `String` and
vice versa!

To convert a character array into a `String`, we could make use of the `String`
constructor:

```java
char[] gradesAsCharArray = {'A', 'B', 'C', 'D', 'F'};
String gradesAsString = new String(gradesAsCharArray);
```

To convert a `String` into a character array, we can actually use a method of
the `String` class called `toCharArray()`. We will learn more about the methods
within the `String` class in the next lesson, but here is how we can use that
method to go from a `String` to a `char[]`.

```java
String gradesAsString = "ABCDF";
char[] gradesAsCharArray = gradesAsString.toCharArray();
```



## Resources

- [Medium: ASCII Table in Java Programming](https://medium.com/@aidafarihabaharunsuratman/did-someone-actually-use-ascii-table-in-java-programming-9710a65c6ed9)  
- [Unicode](https://docs.oracle.com/javase/tutorial/i18n/text/unicode.html)    
- [Java 17 Character](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Character.html)   
- [Java 17 String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)   