+++
title = "Computer Science I - Lecture 04"
author = ["eo shiru"]
date = 2018-11-02
lastmod = 2019-04-06T00:14:36+02:00
draft = false
+++

## Comparison {#comparison}

There are the following comparison operators which yield a boolean value ( `0` for false and `≠0` for true usually 1): `==`, `!=`, `>`, `<`, `>=`, `<=`.


## Assignment Shortcuts {#assignment-shortcuts}

`a = a+5` can be written more concise as `a+=5` this is possible with all operators (\*, /, %, +, -). Yes this is also possible with `%`:

```cpp
int a,b, c;
a = 5;
b = 2;

a %= b; // -> a = a % b;

cout << a << endl;
```

Which yields `1` for `a`. But this is rather hard to read!

To increment/decrement by one it is even possible to write `a++` and `a--` , as well as `++a` and `--a`. The difference between `--` and `++` as a pre- or postfix operaror is that as a prefix operator (eg `--a`) `a` is first decremented and then evaluated and in case of a postfix operator (`a++`) `a` is first evaluated and then incremented. So in regards to the continued use `a++` is incremented after the usage and `++a` would be incremented before the usage so `a` is already up by one when it is then used.


## Flow Control {#flow-control}

Flow in C++ can be controlled via `if (cond) { ... } else if (cond) { ... } else { ... }` statements. Take a look at the following example to solve quadratic equations:

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
  float a, b, c, d, x1, x2;
  cout << "Solve Quadratic Equations \n";
  cout << "Enter coefficient a, b, c: ";
  cin >> a >> b >> c;
  if (a == 0)
    cout << "Not a quadratic equation \n";
  else
    {
      d = (b * b) / (4 * a * a) - c / a;
      if (d < 0)
        cout << "no real resolution \n";
      else
        {
          x1 = -b / (2 * a) - sqrt(d);
          x2 = -b / (2 * a) + sqrt(d);
          cout << "x1 = " << x1 << "x2 = " << x2 << endl;
        }
    }
}
```

The flow can also be controlled with a `switch-case` statement. For example to "build a simple calculator":

```cpp
int a, b;
char op;
cin >> op;

switch (op) {
 case '+': // notice the single quotes '' because it is a char
   cout << a + b;
   break;
 case '-':
   cout << a - b;
   break;
 case '/':
   cout << a / b;
   break;
 case '*':
   cout << a * b;
   break;
 case '%':
   cout << a % b;
   break;
 default:
   cout << "*** Error ***";
 }

cout << endl;
```

Notice that without the `break;` at each case the other cases would be checked and might be executed as well! Also the case values (eg `+`) have to be unique and constant! Constant in that sense that there are no computations allowed (eg function calls).


## Repetition {#repetition}

There may be a situation, when you need to execute a block of code several number of times. In general, statements are executed sequentially: The first statement in a function is executed first, followed by the second, and so on.

Programming languages provide various control structures that allow for more complicated execution paths.

A loop statement allows us to execute a statement or group of statements multiple times. C== provides the following types of loops:

-   **while loop**
    -   repeats a statement or group of statements while a given condition is true
    -   it tests the condition before executing the loop body
    -   eg `while (count < 100) { ... count++; ... }`
-   **do..while loop**
    -   like a ‘while’ statement, except that it tests the condition at the end of the loop body &rarr; therefore the "do..while" loop is executed at least one time
    -   eg `do { ... count++; ... } while ( count < 100);`
-   **for loop**
    -   execute a sequence of statements multiple times and abbreviates the code that manages the loop variable
    -   eg `for (int x = 0; x < 10; x++) { ... }`

It is also possible to nest loops inside any other loop.

An infinite loop like

```cpp
for( ; ; ) {
  printf("This loop will run forever.\n");
}
```

wont stop running by itself because an absent conditional expression is considered to be true. To interrupt the loop for example from the terminal press `Ctrl-C`.

Use for loop when number of iterations is known beforehand, i.e. the number of times the loop body is needed to be executed is known.

Use while loops where exact number of iterations is not known but the loop termination condition is known.

Use do while loop if the code needs to be executed at least once like in Menu driven programs.
