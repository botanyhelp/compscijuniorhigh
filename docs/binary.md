## CompSci Binary Class

### Binary Representation

Computers deal with bits.  Here we see 8 bits in a row, one bit per square:

![https://upload.wikimedia.org/wikibooks/en/f/f5/Byte45.png](https://upload.wikimedia.org/wikibooks/en/f/f5/Byte45.png)

We might interpret that to mean the number 45 (**32+8+4+1**).

Computers are also **byte-oriented**.  A byte is 8bits and is the smallest thing that a computer will consider.  Here we see bytes, one byte (8bits) per blue square:

![http://www.cs.colostate.edu/~anderson/cs253/wiki/lib/exe/fetch.php?w=400&media=lectures:typespic.png](http://www.cs.colostate.edu/~anderson/cs253/wiki/lib/exe/fetch.php?w=400&media=lectures:typespic.png)

The names to the left of the blue squares are some common data types: char bool int double long.  The last one with 5 bytes is an array of 5 char.  The sixth one in the list above is a **pointer to int**.  We will talk about arrays and pointers another time. 

Notice that the boolean (**bool** in the picture above) takes a whole byte.  Boolean is a data type that has two representations: **TRUE** or **FALSE**.  Therefore, to represent a boolean, we should only need one bit **1=TRUE** or **0=FALSE**.  Using 8bits (a whole byte!) to represent a boolean is a waste of 7 bits.  But computers are **byte-oriented**.  The smallest unit that will be considered is a byte, not a bit.  

Notice that some data types (like **long int** in the picture above) take several bytes.  To represent large numbers, like 32767, you're going to need some more bytes.  

Here we see a representation of a number, (sint16, signed integer 16 bits) that is using two bytes, 16 bits, to represent one number.  Notice also that the red bit is being used to allow for the representation of negative numbers.  It takes a whole bit to tell the **sign** of the number (**negative=1** or **positive=0**):

![http://i.stack.imgur.com/LqMAx.png](http://i.stack.imgur.com/LqMAx.png)

The list below shows the names and maximum/minimum values for numbers that are using increasing numbers of bytes to represent the number (the CHAR uses one byte, LONG uses 8 bytes):

* The minimum value of CHAR = -128
* The maximum value of CHAR = 127
* The minimum value of UNSIGNED CHAR = 0
* The maximum value of UNSIGNED CHAR = 255
* The minimum value of SHORT INT = -32768
* The maximum value of SHORT INT = 32767
* The minimum value of INT = -2147483648
* The maximum value of INT = 2147483647
* The minimum value of CHAR = -128
* The maximum value of CHAR = 127
* The minimum value of LONG = -9223372036854775808
* The maximum value of LONG = 9223372036854775807
* The minimum value of UNSIGNED LONG = 0
* The maximum value of UNSIGNED LONG = 18446744073709551616 

Those first four, CHAR and UNSIGNED CHAR, (**in the list above**) would look like these bits:

* 10000000
* 01111111
* 00000000
* 11111111

Those last two UNSIGNED LONGs would look like these bits:

* 0000000000000000000000000000000000000000000000000000000000000000
* 1111111111111111111111111111111111111111111111111111111111111111

Here we see commonly used data types and how many bytes are required to use them:

![http://image.slidesharecdn.com/dweiss-sizeof-120509022400-phpapp02/95/sizeofobject-how-much-memory-objects-take-on-jvms-and-when-this-may-matter-11-728.jpg](http://image.slidesharecdn.com/dweiss-sizeof-120509022400-phpapp02/95/sizeofobject-how-much-memory-objects-take-on-jvms-and-when-this-may-matter-11-728.jpg)

Notice that if you are treating those 64 bits as an UNSIGNED LONG, then there is no way to represent negative 1 (-1) or any negative number.  

How those 64 bits are treated is up to you.  If you want an extremely large positive integer, then UNSIGNED LONG might be a good choice.  

Other ways you might want to treat 64 bits include:

* an array of 8 UNSIGNED CHAR, eight 8-bit numbers
* an array of 8 SIGNED CHAR, eight 8-bit numbers
* an array of 4 SHORT int, four 16-bit numbers
* an array of 2 LONG, two 32-bit numbers


### ASCII

A much more common way to deal with 64 bits is to treat it as text.  

Did you know that billions of computers think that this 64 bit stream means something very specific:

0011100001110100011010000100011101110010011000010110010001100101

It means precisely this:

**8thGrade**

There is a long standing agreement that specific bytes (8bits) represent specific letters/characters.  Its called the ASCII table and it looks like this:

![https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/ASCII-Table-wide.svg/2000px-ASCII-Table-wide.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/ASCII-Table-wide.svg/2000px-ASCII-Table-wide.svg.png)

If you break that 64bit number into eight 8bit numbers like this:

00111000 01110100 01101000 01000111 01110010 01100001 01100100 01100101 

Then you can use the ASCII table to convert those 8 numbers to the letters that they represent.  Lets take the first 8bit number: 

00111000

That number as an integer is 56 (32+16+8).  Using the ASCII table above, we can see that the **Char** represented by the decimal number 56 is "8".  Lets take the second 8bit number from above:

01110100 

That number as an integer is 116 (64+32+16+4).  Using the ASCII table above, we can see that the **Char** represented by the decimal number 116 is "t", lowercase t.  

8 t h G r a d e

If you grow tired of the ASCII table, you can instead treat those 64bits as a large integer, and get this large number:

4067991019493352549

* How many bits do you need to represent DNA, which has 4 nucleotides GACT?
* How many bits do you need to represent all of the world's characters (not just ABC123) including Chinese, Arabic and Klingon?  
* How would that happen, how would you expand beyond ASCII?

### Reals

So far we've been talking about integers.  Representing **real** numbers (numbers with decimal places) is also required.  Reals are also represented with bits.  We'll leave reals for another day but the representation looks like this:

![https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/IEEE_754_Double_Floating_Point_Format.svg/2000px-IEEE_754_Double_Floating_Point_Format.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/IEEE_754_Double_Floating_Point_Format.svg/2000px-IEEE_754_Double_Floating_Point_Format.svg.png)

### Objects

We've been covering "standard" ways of treating 64 bits.  You can treat 64 bits however you want.  We could decide that those 64 bits represent a game character, like this:

* bit #1, the bit on the far right side, represents whether the character is GOOD=1 or EVIL=0
* bit #2, the second bit from the far right side, represents whether the character is FEMALE=1 or MALE=0
* bit #3, the third bit from the far right side, represents whether the character is HUMAN=1 or NONHUMAN=0
* bit #4, the fourth bit from the far right side, represents whether the character is AWAKE=1 or ASLEEP=0

Under this treatment, this number:

* 0000000000000000000000000000000000000000000000000000000000001111

..would represent a GOOD, FEMALE, HUMAN and AWAKE.  This number:

* 0000000000000000000000000000000000000000000000000000000000000000

..would represent an EVIL, MALE, NONHUMAN and ASLEEP.  It might be easier to talk about these characters by saying that:

* character 1 is a 15
* character 2 is a 0

..any program that understood the format would know four important characteristics of these characters. We know that a 3 represents a character that is GOOD FEMALE, NONHUMAN and ASLEEP. 

```
What is the state of a character that is a 6?
```

Using bits to represent something besides numbers is very common and is the basis of **objects** in programming.  An **object** typically has a state (like a "1" character has a state of: GOOD, MALE, NONHUMAN and ASLEEP).  An object also usually has **behavior** represented in those bits.  For example, we could use some bits to represent a function **castSpell()**.  castSpell() might do different things based on the state of the object.  For example, it might not do anything at all if the character doing the castSpell() has a state of ASLEEP.  

How castSpell() is represented as bits is a complex topic that we won't cover.  As programmers, we care about the syntax of the programming language.  As programmers, we want to write code that does the things that castSpell() should do.  As programmers, we do NOT care how the actual bits look inside of castSpell() when its running on the machine.  We do care about the python, for example, that we write, and we do care about what happens when we run the python program.  We want to see, for example, when we run the python, that any sleeping characters are unable to cast any spells.  As computer scientists, we do care about the representation of information (**data structures**) and what to do with it (**algorithms**). 

