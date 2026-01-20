# 4 Classes and Objects

***Ensure you commit the exercises to GitHub.***

Resources:
The Java API documentation is located at: (http://java.sun.com/javase/6/docs/api/)_

## Programming Projects:
***1) Using String Objects***


Fill in the blanks in the program below as follows: 


(a)         declare the variable town as a reference to a String object and initialise it to "Anytown, UK".

(b)         write an assignment statement that invokes the length method of the string class to find the length of the college String object and assigns the result to the stringLength variable

(c)         complete the assignment statement so that change1 contains the same characters as college but all in upper case

(d)         complete the assignment statement so that change2 is the same as change1 except all lowercase “e's” are replaced with the asterisk (*) character.

(e)         complete the assignment statement so that change3 is the concatenation of college and town (use the concat method of the String class rather than the + operator) 

```
// **************************************************
//   StringPlay.java
//
//   Play with String objects
// **************************************************
public class StringPlay
{
   public static void main (String[] args)
   {
      String college = new String ("Leeds Beckett University"); //Similar for part (a)


      ________________________________________________________; // part (a)


      int stringLength;
      String change1, change2, change3; 


      ________________________________________________________; // part (b)


      System.out.println (college + " contains " + stringLength + " characters.");


      change1 = ______________________________________________; // part (c)


      change2 = ______________________________________________; // part (d)


      change3 = ______________________________________________; // part (e)


      System.out.println ("The final string is " + change3);
    }
}
```
```
Sample Output:




Popple College contains 14 characters.
The final string is Popple College Anytown, UK
________________
```

***2) Dice***


Write a program that simulates rolling two dice using the following steps:
1. Prompt the user for the number of sides for two dice.
2. “Roll” the dice three times by generating a random number between 1 (inclusive) and the number of sides (inclusive).
3. Keep track of the sum of the rolls for each die and output the sum and average for each die.

```
Sample Output:




How many sides does die 1 have? 6
How many sides does die 2 have? 20
Die 1 first roll = 5.
Die 2 first roll = 14.
Die 1 second roll = 1.
Die 2 second roll = 20.
Die 1 third roll = 3.
Die 2 third roll = 9.
Die 1 rolled a total of 9 and rolled 3 on average.
Die 2 rolled a total of 43 and rolled 14.333 on average.

```
	


***3) Pin Encryption***


Write a block of source code to encrypt a four digit pin number by doing the following:
1. Convert the pin number to hexadecimal.
2. Generate two random numbers greater than 1000 and less than 65536 and convert them to hexadecimal.
3. Sandwich the converted pin between the two random hexadecimal numbers.


Sample Output:
```

Enter a 4 digit pin number to encrypt: 8491
Your encrypted pin number is 1787212b12ef.

```
	





***4) Sphere Calculations***


Write and application that reads the radius of a sphere and prints its volume and surface area. Use the following formulas, where r represents the radius of the sphere. Print the output to four decimal places.


Volume =  4πr3 / 3


Surface area = 4πr2
