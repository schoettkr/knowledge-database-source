+++
title = "Algos & Programming - Lecture 05"
author = ["eo shiru"]
date = 2018-10-22
lastmod = 2019-04-06T00:17:14+02:00
draft = false
+++

## Type and signature {#type-and-signature}

Similar to functions in math functions in C (or programming for that matter) have a domain (Defintionsbereich/Definitionsmenge) and a codomain (Wertebereich/Zielmenge). Additionally to the name a function declaration (respective definiton) contains the domain and codomain:

```C
int euclid(int, int);
```

The type of the return value of euclid is `int` and defines the codomain, which in this case is a set of integers. The domain is specified via the parameter types in this case `int` and `int` so also sets of integers. Mathematically expressed the code would look like this `euclid: int x int ⟶ int` (an element out of the integer set emerges out of the domain `int x int`).

Technically `int x int ⟶ int` is the type of the function "euclid". Practically however it became established to view the codomain as "type" of the function. Following this you'd say "euclid" has the type `int`, however _return type_ would be the more accurate term.

The type together with the name of a functions builds the functions _signature_. A declaration therefore introduces function signature to the compiler.

Many operators look the same e.g `+` but do different things depending on the context, which is the particular type. Typing helps the compiler to find the right procedure. Although there are other programming languages that do not require type declarations and infer types automatically for instance Javascript. This is called _type inference_.


## Basic types (primitive data types) {#basic-types--primitive-data-types}

C provides few basic types. Yet it is possible to "build" more types. Since the sets are described by the C types are not infinite they are subsets of for example the natural numbers.
C99 knows the following basic types:

-   subsets of integers
-   subsets of rational numbers
-   boolean values
-   subset of complex numbers
-   empty set
-   memory addresses (which are derived types!)

More on [C data types](https://en.wikipedia.org/wiki/C%5Fdata%5Ftypes).


### Integers & Chars {#integers-and-chars}

C offers the following keywords in regards to integers

-   type specifiers: `int`, `char`
-   modifiers: `short` (not for `char`!), `long` (not for `char`!), `unsigned`, `signed`

When the type `int` is modified it may be omitted as a keyword.

But why do different types exist for integers? Well differently sized values need different amounts of storage space. A computer stores values in bits (**bi** nary dig **its**). In \\(n\\) bits it is possible to store \\(2^n\\) different values. Typically the smallest addressable unit is a **byte** (= 8 bit). Values are therefore stored in one or more bytes.

Choosing the the "right" type is hence always a compromise between the amount of different values and the size in storage (+ access speed).

All types which name contains `unsigned` are "vorzeichenlos", those which contain `signed` are "vorzeichenbehaftet". In case of just `int` without a sign modifier the type is always signed. In case of `char` this is up to the compiler. For most types there are no concrete sets defined, however some ranges are guaranteed:

| Type                                                                  | Range                                                                                                                                                                                      | Format specifier                  |
|-----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
| `char`                                                                | Smallest addressable unit of the machine that can contain basic character set. It is an integer type. Actual type can be either signed or unsigned.                                        | %c                                |
| `signed char`                                                         | Of the same size as `char`, but guaranteed to be signed. Capable of containing at least the [−127, +127] range                                                                             | %c (or %hhi for numerical output) |
| `unsigned char`                                                       | Of the same size as `char`, but guaranteed to be unsigned. Contains at least the [0, 255] range                                                                                            | %c (or %hhu for numerical output) |
| `short` `short int` `signed short` `signed short int`                 | Short signed integer type. Capable of containing at least the [−32,767, +32,767] range\* thus at least 16 bits in size                                                                     | %hi                               |
| `unsigned short` `unsigned short int`                                 | Short unsigned integer type. Contains at least the [0, 65,535] range;                                                                                                                      | %hu                               |
| `int` `signed` `signed int`                                           | Basic signed integer type. Capable of containing at least the [−32,767, +32,767] range thus, it is at least 16 bits in size.                                                               | %i or %d                          |
| `unsigned` `unsigned int`                                             | Basic unsigned integer type. Contains at least the [0, 65,535] range                                                                                                                       | %u                                |
| `long` `long int` `signed long` `signed long int`                     | Long signed integer type. Capable of containing at least the [−2,147,483,647, +2,147,483,647] range;[3][4] thus, it is at least 32 bits in size                                            | %li                               |
| `unsigned long` `unsigned long int`                                   | Long unsigned integer type. Capable of containing at least the [0, 4,294,967,295] range                                                                                                    | %lu                               |
| `long long` `long long int` `signed long long` `signed long long int` | Long long signed integer type. Capable of containing at least the [−9,223,372,036,854,775,807, +9,223,372,036,854,775,807] range thus, it is at least 64 bits in size, specified since C99 | %lli%                             |
| `unsigned long long` `unsigned long long int`                         | Long long unsigned integer type. Contains at least the [0, +18,446,744,073,709,551,615] range, specified since C99                                                                         | %llu%                             |
|                                                                       |                                                                                                                                                                                            |                                   |

&lowast;The negative value is −32767 (not −32768) due to the one's-complement and sign-magnitude representations allowed by the standard, though the two's-complement representation is much more common

Since C99 there is a header file called `stdint.h` which defines integers with a fixed bit size like/if(?) they're present on the current platform/system. For example:

-   `int8_t` and `uint8_t` for signed and unsigned integers with _exactly_ 8 bit and therefore a cardinality of \\(256\\)
-   `int16_t` and `uint16_t` for signed and unsigned integers with _exactly_ 16 bit and therefore a cardinality of \\(65536\\)
-   `int32_t` and `uint32_t` for signed and unsigned integers with _exactly_ 32 bit and therefore a cardinality of \\(4294967296\\)
-   `int64_t` and `uint64_t` for signed and unsigned integers with _exactly_ 64 bit and therefore a cardinality of \\(18446744073709551616\\)

PS. Cardinality means the number of (distinct) elements in a set

C90 doesn't specify how a value "looks" in memory/storage meaning how it is exactly represented in bits. Nevertheless most platforms use a binary positional notation with two's complement for the representation of negative integers:

-   unsigned: value \\( = \sum\_{i=1}^{n} b\_i \* 2^{i-1} \\)
-   signed: value  \\( = \begin{cases} \sum\_{i=1}^{n-1} b\_i \* 2^{i-1}, \text{wenn } b\_n = 0 \\ (- \sum\_{i=1}^{n-1} (1- b\_i ) \* 2^{i-1}) - 1, \text{wenn } b\_n = 1  \end{cases}\\)

Now a bit onto "char"s. Why is the name of an integer type `char`?

Originally this type was meant to represent values in the range of **ASCII-Codes** (7 bit) respective **ANSI-Codes** (8 bit) &rarr; _character_. C doesn't provide an explicit type for characters. The usage through `char` is solely achieved through the interpretation of the integer when outputting.

Depending on the platform the same `char` value can represent different characters. That's why today the usage of `wchar_t` is encouraged because it eases internalization and standardization (importable from `wchar.h`).

However in this lecture we will continue with ASCII/ANSI codes for now.

```C
/* char .c -- interpretation of char type */
#include <stdio.h>

char addchar ( char c1 , char c2 )
{
return c1 + c2 ;
}

int main ()
 {
 printf (" Result is %c with the code %d\n",
 addchar ('a' ,1) , addchar ('a' ,1));
 return 0;
 }
```

```text
Result is b with the code 98
```


### Rational numbers {#rational-numbers}

Because of internal representation C can only represent rational numbers \\(\mathbb{Q}\\) and not generic reals \\(\mathbb{R}\\) (allgemeine reelle Zahlen). These numbers are commonly called _floating points numbers_. C provides the following types to represent floating point numbers:
`float`, `double` and `long double`. Besides a limited codomain floats in C have a limited precision. Again there are no fixed sizes provided, but minimum ranges are guaranteed:

-   `float` has a codomain of at least \\(\pm 10^{\pm 37}\\) and a precision of at least 6 decimal places (Nachkommastelle)
-   `double` at least the codomain of `float` and a precision of at least 10 decimal places
-   `long double` at least as "good" as `double`

In practice almost all compilers follow the IEEE-754 standard that defines the binary representations of floats.


### Void {#void}

C knows the base type `void`. `void` is basically an "anti-type" because it is used when no type is wanted (&rarr; empty set; leere Menge). Is helpful when parameters and/or return value are not needed.

If the return value of a function is `void` the `return` statement in the function can be omitted. Is the parameter list of a function empty (`void` is its sole element) than it can be omitted as well.


## Type conversion {#type-conversion}

The types in `a + b` could be different for instance `unsigned char` and `signed int`. In those cases the types are automatically (implicit) converted. Generally all the data types of the variables are upgraded to the data type of the variable with largest data type.

However besides the implicit automatic conversion, type conversion may be triggered manually and therefore explicitly by writing the type in parens before the variable/expression. Using a type like this, it acts as a _cast operator_ and is type casting the value. Doing this type conversion to lower data types is possible as well.

```C
/* cast .c -- type cast */
int printf ( const char * ,...);
long ladd (long , long );

int main ()
{
printf (" Ergebnis : %d\n", (int)ladd(23 ,42)); // "(int)" type cast to int to get rid of warning and implicit conversion because of "%d" formatter
return 0;
}

 long ladd ( long x , long y )
 {
 return x + y ;
 }
```

A type declaration like in C is not needed in all languages. In python for example the types are dynamic, that means they're determined at runtime. Python in contrast to C also offers strings and numbers with arbitrary size and precision (and more!).


## Literals {#literals}

A "direct value" of a specific type is called _literal_. Literals of specific types require a special notation, to prevent an unneccessary type conversion:

-   `int` literals can be written in decimal, octal and hexadecimal and if needed with a sign:
    -   decimal: only digits `0-9` however not leading with a `0` &rarr; e.g `42`
    -   octal: prefix of `0` and then only digits `0-7` &rarr; e.g `052`
    -   hexadecimal: prefix of `0x` and then only digits `0-9` and letters `A-F` &rarr; e.g `0x2a`
-   `unsigned int` like int but with the suffix "u"/"U" &rarr; e.g `123U`
-   `long/unsigned long` like int/unsigned int but with the suffix "l"/"L" &rarr; e.g `123L` respective `123UL`
-   `long long/unsigned long long` like int/unsigned int but with the suffix "ll"/"LL" &rarr; e.g `123LL` respective `123ULL`
-   `double` as a decimal with decimal place(s), decimal point, and/or "e"/"E" with following exponent&rarr; e.g `1.23e10`, `.23` or `1e10`
-   `float` like double but with the suffix "f"/"F" &rarr; e.g `1.23e10f`, `.23f` or `1e10f`
-   `long double` like double but with the suffix "l"/"L" &rarr; e.g `1.23e10L`, `.23l` or `1e10l`
-   `char` literals have to be written in single quotes &rarr; e.g `'*'`
-   `wchar_t` literals are written like `char` with the prefix `L` &rarr; e.g `L'a'`. There also escape sequences to display sequences or characters that are difficult to represent else. [Here's a list](https://en.wikipedia.org/wiki/Escape%5Fsequences%5Fin%5FC#Table%5Fof%5Fescape%5Fsequences).
