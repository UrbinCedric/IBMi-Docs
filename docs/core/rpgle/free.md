# Introduction to RPGLE Free

There might be a lot of bells and whistles specific to IBMi, but RPGLE is just another general purpose programming language.
If you can learn Java, C or C#, you can learn RPGLE. If you already know C, you'll probably notice a lot of similarities.

Its easier for a newer developer to learn mainly free format with a bit of fixed format for legacy code and general understanding.
New code should be written in fully free form if possible. 
New routines or procedures in existing fixed format code should be attempted to be written with free format.

Before starting this behemoth of a section:<br>
**Just hang in there, it does get fun.**


## Free Format Preprocessor
To use free format RPGLE, you have to include some preprocessor commands so the compiler knows to compile the correct format.

In older code, you could only do a mix of fixed and free formats using two preprocessor commands.
To mix fixed and free format, use ```/free``` to start a free format code block and ```/end-free``` to end it.
```php
D* (D spec comment)

/free
  // RPGLE free code goes here!
  //
  // NOTE: Don't worry about the code
  //       above or below yet
/end-free

C* (C spec comment)
```

<br>

Now there is the option to compile using only free format.
To specify only free format, include ```**free``` on the first line of the file. 
```php
**free

// Only RPGLE free format code is allowed in this file!
//
// Fixed format will not compile!

```
<br>

From this point on we will only be using fully free RPGLE for easier understanding of the language and its quirks. 
The next page will explain a bit about fixed format in comparison to free format.

**Update**: Apparently the RPG compiler has gotten a lot better. The use of ```/free``` and ```/end-free``` are entirely optional
and actually considered deprecated. Now if you **HAVE** to use fixed format and free format, the compiler will automatically know how to compile it without the preprocessor statements.
The use of ```**free``` still works the same, if you include then fixed format will not compile.


## Opcodes
Rather than overfill this page with big tables, here is the link to the IBM documentation https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzasd/operxcl.htm#operxcl


## Naming
**Important note: naming in RPGLE is not case sensitive**
However, naming should be consistent to avoid confusion.


## Comments
Comments in RPGLE free are single lined.
```php
// I am a comment
```


## Control Specifications
Control specifications allow you to specify information that should be used to compile or execute your program.
This includes date/time formats, usage of the RPG cycle, activation group configuration, and debug options.

Control specifications are the equivalent of **H specs** or **Header specifications**, more on this in a later section.
They need to be included directly under the ```**free``` preprocessor command and any other code.

Here are some common control specifications that you usually include in your programs.
```php
**free

ctl-opt main(main);
ctl-opt option(*srcstmt:*noDebugIO:*nounref) dftActGrp(*no);
```
<br>

```ctl-opt main(main);``` specifies that you will be using a **linear main**, you will **not** be using the RPG cycle mentioned previously.
This control option allows your program to behave a lot like you would expect it to like in C, Java, or Python.
In this case, the program will execute a subroutine named **main** first.


```ctl-opt option(*srcstmt);``` specifies the generated program to use source statement line numbers. 
When this program errors, you can go straight to the line number it occurred.


```ctl-opt option(*noDebugIO);``` specifies to not generate breakpoints for files' fields.
If this is not included, when you debug your program a breakpoint will be automatically generated at each field in each file.


```ctl-opt option(*nounref);``` specifies to not generate unreferenced fields and variables.


```ctl-opt dftActGrp(*no);``` **TODO**


Its worth noting that the usage of **' : '** in ```ctl-opt option(*srcstmt:*noDebugIO:*nounref);``` is the way that RPGLE
separates parameters.


More about control specifications can be read at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzasd/conspe9.htm



## Simple Data Types
Before learning how to declare a variable, the simple data types should be defined.

| Type             | Size (bytes)   | Fixed Format Type | Free Format Example         |
| ---------------- | -------------- | ----------------- | --------------------------- |
| Pointer          | 16             | *                 | ```dcl-s x pointer;```      |
| Character        | 1 - 65535      | A                 | ```dcl-s x char(10);```     |
| Varchar          | ?              | A VARYING         | ```dcl-s x varchar(55);```  |
| Binary           | 2, 4           | B                 | ```dcl-s x bindec(9);```    |
| Date             | 6, 8, 10       | D                 | ```dcl-s x date;```         |
| Float            | 4, 8           | F                 | ```dcl-s x float(8);```     |
| Graphic (DBCS)   | 32766          | G                 | ```dcl-s x graph(10);```    |
| Integer          | 1, 2, 4, 8     | I                 | ```dcl-s x int(10);```      |
| Indicator        | 1              | N                 | ```dcl-s x ind;```          |
| Packed           | 1 - 31         | P                 | ```dcl-s x packed(15:2);``` |
| Time             | 8              | T                 | ```dcl-s x time;```         |
| Unsigned Integer | 1, 2, 4, 8     | U                 | ```dcl-s x uns(10);```      |
| Timestamp        | 26             | Z                 | ```dcl-s x timestamp;```    |

**Other things of note**:
* DBCS - Double byte character set (other languages such as Chinese and Japanese)
* Integer declaration - int(digits)
  * int(3) = 1 byte(s)
  * int(5) = 2 byte(s)
  * int(10) = 4 byte(s)
  * int(20) = 8 byte(s)


## Indicators
An indicator is used just like a boolean, they can be set to ```1, 0, *ON, *OFF```.
There are various dedicated indicators in RPG, but there's really only one that I care to remember.
In RPGLE, the **last record indicator** needs to be set to ```*ON``` in your main function.
```php
*INLR = *ON;
```


## Definition Statements
Definitions begin with opcode ```dcl-?``` and if needed end with ```end-?```.
More details on definition statements can be read at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzasd/freedatadef.htm

Definition statements have optional keywords that can further define the field.
More information on definition statement keywords can be read at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzasd/dskwd.htm


## Defining a Standalone Field
The definition opcode ```dcl-s``` is for defining a standalone field (variable).

Side note: String literals in RPGLE use single quotes instead of double quotes.

```php
// Simple examples of variable declaration:

dcl-s myString  varchar(64);
dcl-s myString2 varchar(50) inz('Hello World');
dcl-s myString3 char(50) inz('I am a fixed size');

dcl-s myNum int(10) inz(1234);
dcl-s myDecimal packed(8);
```

The ```inz``` keyword is used to initialize a variable.


## Defining a Named Constant
The definition opcode ```dcl-c``` is used to define a named constant.

```php
dcl-c myConst const(1234); // Using keyword
dcl-c myConst2 5;          // Define directly
```


## Defining a Data Structure
A data structure definition begins with the opcode ```dcl-ds``` and ends with ```end-ds```.
If you are comfortable with structs in C, data structures in RPGLE feel very familiar.

Each field in a data structure definition is defined like a standalone field,
except the ```dcl-s``` opcode is not included.

```php
// A qualified data structure
// Qualified forces the data structure to
//  be used in order to access fields
//
// Fields are accessed by:  myDs.myNum
dcl-ds myDs qualified;
  myNum int(5);
  myStr char(32);
end-ds;

// A qualified template data structure
// Used to provide a common template for
//  other data structure definitions
dcl-ds person qualified template;
  firstName char(16);
  lastName  char(16);
  age int(3);
end-ds;

// A data structure defined using a template
// likeds(person) -> Like data structure named person
dcl-ds friend likeds(person);

// Data structures are very useful for 
// dealing with indicators in display files 
// (more on this later) ->  if dspf.refresh ...
dcl-ds dspf qualified;
  exit      ind pos(3);
  refresh   ind pos(5);
end-ds;

// Also useful for just organizing constants
// such as SQL states ->  if sqlStates.success ...
dcl-ds sqlStates qualified;
  success char(2) inz('00');
  warning char(2) inz('01');
  noData  char(2) inz('02');
end-ds;

// Lastly, there are special data structures
// that can be accessed for various data.
// For example, this data structure has access
// to a ton of program information (PSDS).

dcl-ds pgmDs PSDS qualified;
  procName *proc; // Name of program
end-ds;
```

This is a very high level overview of data structures,
more can be read about them here https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzasd/freedatastructure.htm


## Arrays and Data Structure Arrays
Declaring an array is the same as declaring a standalone field (with ```dcl-s```), but to make it an array you include the keyword ```dim```.

There are also variable sized arrays (IBMi 7.4+) and compile time arrays. (Not covered in this documentation. TODO?)

**Important Note** - Arrays in RPGLE are **one-indexed** (indexing starts at one and not zero!).
Additionally, indexing an array uses parentheses instead of square braces.

Data structure arrays are defined in a similar fashion as regular arrays, just include the ```dim``` keyword on the definition.

```php
dcl-s myArray char(16) dim(40);    // Define a char array with 40 elements

dcl-ds myDs qualified;
  myArray int(3) dim(10);          // Arrays can also be defined in data structures
end-ds;

dcl-ds myDsArr dim(25) qualified;  // Data structure arrays are declared in a similar way
  field1 char(99);
  field2 int(5);
  field3 ind;
  field4 int(3) dim(10);           // Array in a data structure array
end-ds;

myArray(1) = 'Hello World';        // To reiterate, arrays are one-indexed
myDs.myArray(3) = 'Woah';          // Parentheses instead of square braces

myDsArr(10).field1 = 'Awesome';    // Data structure arrays are accessed as expected
myDsArr(10).field2 = 100;
myDsArr(10).field3 = *ON;
myDsArr(10).field4(5) = 1234;
```


## Operators
Operators in RPGLE are slightly different than languages like Java or C.

| Name                  | Operator       | Type          | Example                       |
| --------------------- | -------------- | ------------- | ----------------------------- |
| Addition              | ```+```        | Arithmetic    | ```x = 1 + 1;``` > 2          |
| Subtraction           | ```-```        | Arithmetic    | ```x = 1 - 1;``` > 0          |
| Multiplication        | ```*```        | Arithmetic    | ```x = 1 * 1;``` > 1          |
| Division              | ```/```        | Arithmetic    | ```x = 1 / 1;``` > 1          |
| Exponentation         | ```-```        | Arithmetic    | ```x = 2 ** 4;``` > 16        |
| Equality              | ```=```        | Relational    | ```1 = 1``` > true            |
| Inequality            | ```<>```       | Relational    | ```1 <> 1``` > false          |
| Greater Than          | ```>```        | Relational    | ```1 > 2``` > false           |
| Greater Than or Equal | ```>=```       | Relational    | ```1 >= 1``` > true           |
| Less Than             | ```<```        | Relational    | ```1 < 5``` > true            |
| Less Than or Equal    | ```<=```       | Relational    | ```2 <= 4``` > true           |
| Logical And           | ```AND```      | Logical       | ```1=1 and 2=2``` > true      |
| Logical Or            | ```OR```       | Logical       | ```1=1 or 2=5``` > true       |
| Assignment            | ```=, +=, -=, *=, /=, **=```   | Assignment | ```x = 4; x += 2;``` |
| Unary Plus            | ```+```        | Unary         | ```x = +3```                  |
| Unary Minus           | ```-```        | Unary         | ```x = -x```                  |
| Logical Negation      | ```NOT```      | Unary/Logical | ```x = not x;```              |

As you can see its just slightly different than a normal set of operators that everyone is used to.


## Conditional Statements
RPGLE has the standard conditionals you would expect in a general purpose language.

Blocks of statements in RPGLE all follow a similar pattern of ending with a specfic opcode.
For example, if blocks end with 'endif' and data structure blocks end with 'end-ds'.

```php
  if (st = 'A');
    dsply ('IF');
  elseif (st = 'B');
    dsply ('ELSE IF');
  else;
    dsply ('ELSE');
  endif;

  // Indicators allow you to be "truthy" with conditionals, 
  // much like booleans in C.
  dcl-s a ind inz(*ON);

  if (a);
    // Do some stuff
  endif;
```
Its worth a small note that the parenthesis are optional on a conditional statement.
For readability, concider using them in some cases.

RPGLE also has something called a select that works similar to a switch statement.
```php
  select;
    when someValue = 1;
      dsply ('Case A');
    when someValue = 2;
      dsply ('Case B');
    when someValue = 3;
      dsply ('Case C');
    other;
      dsply ('Default Case');
  endsl;
```

## Looping Statements
For and Do loops are a staple of any language. <br>

There are two types of **do loops**, do while and do until.
```php
dcl-s num int(10) inz(0);

// Do while
dow num < 10;
  if (num = 5);
    iter;  // skip 5th iteration
  endif;

  dsply (%char(num));
  num += 1;
enddo;

// Do until
num = 0;

dou num < 10;
  if (num = 5);
    leave;  // leave a loop early
  endif;

  dsply (%char(num));
  num += 1;
enddo;
```

A for loop has some optional/alternative syntax to control increment size and direction.
```php
dcl-s num int(10);

// For loop counting up by 1
for num = 1 to 3;
  dsply (%char(num));
endfor;

// For loop counting down by 1
for num = 5 downto 1 by 1;
  dsply (%char(num));
endfor;
```


## Built in Functions
RPGLE also comes with a handful of built in functions that can be pretty convenient.
Here are a few of them just for reference, much more can be found here https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzasd/bifs.htm

```php
dcl-s myNum int(5) inz(10);

dcl-s i int(5);
dcl-s myArr char(10) dim(25);

dcl-s myDate1 date;
dcl-s myDate2 date;
dcl-s myTime date;

// dsply accepts characters, convert int to char
dsply (%char(num)); 

// Get number of elements allocated in array
for i=1 to %elem(myArr);
  dsply (arr(i));
endfor;

// modulus
myNum = %rem(5:4) // 1

// dates and times
myDate1 = %date('2020-03-13');
myDate2 = %date();
myTime = %time();
```


## Monitor
```monitor``` and ```on-error``` are RPGLE's equivalent of a try/catch.
A monitor block starts with the opcode ```monitor``` and ends with the opcode ```endmon```.
Monitor includes the ability to specify 'catches' depending on the error type.

IBM documentation at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_71/rzasd/sc092508966.htm#zzmonit

```php
monitor;
  dsply ('Working...');
on-error *ALL;
  dsply ('Error occurred!');
  // You can also specify status code(s) delimited with ':'
  // *FILE - All file errors
  // *PROGRAM - All program errors
  // *ALL - Both *FILE and *PROGRAM errors
endmon;
```



## Subprocedures
A subprocedure is any procedure defined after the main source or linear main procedure (more on this later).

Subprocedures are just like functions in C, they have a signature and their own scope.
They are defined with opcodes ```dcl-proc``` and ```end-proc```.

To define a subprocedure's interface, the opcodes ```dcl-pi``` and ```end-pi``` are used.
Inside of a subprocedure interface, the subprocedure name, return type, and the parameters are defined.4

Each parameter has an implied opcode ```dcl-parm``` that the compiler automatically includes.
The only time it needs to be included is if the parm name is the same as an opcode, such as ```dsply``` or ```select```.

To return a value from a subprocedure, use the ```return``` opcode. If the subprocedure doesn't return anything, using ```return``` is optional.

Lastly, to invoke a subprocedure you use the declared name in the subprocedure's interface and pass parameters delimited with ':'.
Parameters can be of type ```const``` or ```value```. Const parameters cannot be changed in a subprocedure, but value parameters can.

Subprocedures are awesome at segmenting complicated code into more reusable and readable code.

IBM documentation at https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzasd/subpdef.htm

```php
dcl-s myNum int(10) inz(*zeros);

doThing();
myNum = addTwo(1 : 4);     // myNum = 5
myNum = subTwo(2 : 2);     // myNum = 0

// subprocedure with no parms or return
// therefore, it won't need an interface
dcl-proc doThing;
  dsply ('Did the thing!');
end-proc;


// this subprocedure returns the sum of two integers as an integer
dcl-proc addTwo;
  dcl-pi *N int(10);      // *N -> addTwo
    num1 int(10) const;   // const ensures num1's value cannot be changed
    num2 int(10) const;
  end-pi;

  dcl-s sum int(10) inz(*zeros);  // variables can be defined!

  sum = num1 + num2;
  
  return sum;
end-proc;


// this subprocedure returns the difference of two integers as an integer
dcl-proc subTwo;
  dcl-pi subTwo int(10);
    num1 int(10) const;
    num2 int(10) const;
  end-pi;

  return num1 - num2;
end-proc;

```



## Subroutines
Although its generally recommended not to use subroutines in RPGLE anymore, its still good to know about them.
They are defined with opcodes ```begsr``` and ```endsr```. To invoke a subroutine, the opcode ```exsr``` is used.

Unlike a subprocedure, a subroutine is simply just a block of reusable code.
A subroutine does not have its own local scope, therefore new fields cannot be defined.
```php
// snippet from when I was screwing around trying
//   to implement the SHA-256 algorithm.

dcl-s hash uns(10) dim(8);

exsr initHash;

// Subroutine to initialize hash value array
begsr initHash;
  hash(1) = X'6a09e667';
  hash(2) = X'bb67ae85';
  hash(3) = X'3c6ef372';
  hash(4) = X'a54ff53a';
  hash(5) = X'510e527f';
  hash(6) = X'9b05688c';
  hash(7) = X'1f83d9ab';
  hash(8) = X'5be0cd19';
endsr;

```


## Pointers
Just like C, RPG has the ability to use pointers. If you've never used pointers before, I'd suggest reading up on some examples in C.
To declare a pointer, use the ```pointer``` keyword.<br>
[This page](https://developer.ibm.com/technologies/systems/articles/i-rpg-pointers/) by IBM is going to do a good job at explaining concepts.

TODO: Add more pointer explaination & examples.

```php
// Declare a pointer
dcl-s myPointer pointer;
dcl-s myVar int(10);

// set pointer to memory address of 'myVar'
myVar = 10;
myPointer = %addr(myVar);
```



## Prototypes
Prototypes in RPGLE work similar to prototypes in C. They tell the compiler how to call a program or procedure.
This is useful for calling utility functions or external programs written in CL, RPGLE, C, etc.

IBM documentation at https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_72/rzasd/freeprototype.htm

```php
// Declare a prototype to an external program (EXTPGM) named 'SOMEPGM'
dcl-pr somePgm EXTPGM;
  num1 int(5) const;
  num2 int(5) const;
end-pr;

// Prototype with no parms
dcl-pr doThing int(2) end-pr;

```

## Linear Main
As seen in the introduction to RPGLE [section](https://barrettotte.github.io/IBMi-Book/#/core/rpgle/intro), there is the concept of the RPG cycle.
In newer RPGLE programs it is in your best interest to **not** use the RPG cycle.

Instead a **linear main** is used, much like how C's main function works.
Using a ```ctl-opt``` (control option), you can tell the RPG compiler to use a program's procedure as it's main procedure.
The main procedure doesn't have to be named ```main```, but probably should for easy understanding.
Additionally ```*INLR = *ON``` isn't necessary and very well could just be a ```return``` instead.

IBM documentation at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_71/rzasd/sc092508384.htm

```php
ctl-opt main(main); // specify main procedure

dcl-proc main;  
  dsply ('I am a main procedure');
  *INLR = *on;  
end-proc;       
```



## On-Exit
One of the cool and new features RPGLE recently implemented was ```ON-EXIT```.
This opcode is used for running code whenever a procedure ends no matter what.
The ```ON-EXIT``` block is ran even if an uncaught error is thrown.

IBM documentation at https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/rzasd/zzonexit.htm

```php
ctl-opt main(main);

dcl-proc main;
  dsply ('Hello world');
  // do some things...

  on-exit;
    // clean up, close files, etc...
    dsply ('Exiting...');

end-proc;
```


## Conclusion
So, this is a brief overview of RPGLE free format.<br>
This section is just a reference that will probably evolve as we learn more every day.
