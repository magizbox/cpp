# Data Structure


# Number

C++ offer the programmer a rich assortment of built-in as well as user defined data types. Following table lists down seven basic C++ data types:

* *Boolean*	- bool
* *Character* - char
* *Integer*	- int
* *Floating point* - float
* *Double floating point* - double
* *Valueless* - void
* *Wide character* - wchar_t

Several of the basic types can be modified using one or more of these type modifiers: *signed*, *unsigned*, *short*, *long*

Following is the example, which will produce correct size of various data types on your computer.

```
#include <iostream>
using namespace std;

int main() {
   cout << "Size of char : " << sizeof(char) << endl;
   cout << "Size of int : " << sizeof(int) << endl;
   cout << "Size of short int : " << sizeof(short int) << endl;
   cout << "Size of long int : " << sizeof(long int) << endl;
   cout << "Size of float : " << sizeof(float) << endl;
   cout << "Size of double : " << sizeof(double) << endl;
   cout << "Size of wchar_t : " << sizeof(wchar_t) << endl;
   return 0;
}
```

# String

**String Basic**

```cpp
#include <iostream>
#include <string>
using namespace std ;

// assign a string
string s1 = "www.java2s.com\n";
cout << s1;

// input a string
string s2;
cin >> s2;

// concatenate two strings
string s_c = s1 + s2;

// compare strings
s1 == s2;
```

# Collection

## Pointer

A pointer is a variable whose value is the address of another variable. Like any variable or constant, you must declare a pointer before you can work with it.

The general form of a pointer variable declaration is:

```cpp
type *variable_name;
// example
int    *ip;    // pointer to an integer
double *dp;    // pointer to a double
float  *fp;    // pointer to a float
char   *ch;    // pointer to character
```

**Pointer Lab**

![](https://lh3.googleusercontent.com/MUzBdLRGuwilV16MBABqQtCHj71elA305jtDHBy8wSIMMYkIcqds=w213-h219-no)

```cpp
#include <iostream>
using namespace std;

/*
 * Look at these lines
 */
int* a;
a = new int[3];
a[0] = 10;
a[1] = 2;
cout << "Address of pointer a: &a = " << &a << endl;
cout << "Value   of pointer a:  a = " << a << endl << endl;
cout << "Address of a[0]: &a[0] = " << &a[0] << endl;
cout << "Value   of a[0]: a[0]  = " << a[0]  << endl;
cout << "Value   of a[0]: *a    = " << *a    << endl << endl;
cout << "Address of a[1]: &a[1] = " << &a[1] << endl;
cout << "Value   of a[1]: a[1]  = " << a[1]  << endl;
cout << "Value   of a[1]: *(a+1)= " << *(a+1)<< endl << endl;
cout << "Address of a[2]: &a[2] = " << &a[2] << endl;
cout << "Value   of a[2]: a[2]  = " << a[2]  << endl;
cout << "Value   of a[2]: *(a+2)= " << *(a+2)<< endl << endl;
```

Result:

```
Address of pointer a: &a = 008FF770
Value   of pointer a:  a = 00C66ED0

Address of a[0]: &a[0] = 00C66ED0
Value   of a[0]: a[0]  = 10
Value   of a[0]: *a    = 10

Address of a[1]: &a[1] = 00C66ED4
Value   of a[1]: a[1]  = 2
Value   of a[1]: *(a+1)= 2

Address of a[2]: &a[2] = 00C66ED8
Value   of a[2]: a[2]  = -842150451
Value   of a[2]: *(a+2)= -842150451
```

**Stack**, **Queue**, **Linked List**, **Array**, **Deque**, **List**, **Map**, **Set**

# Datetime

The C++ standard library does not provide a proper date type. C++ inherits the structs and functions for date and time manipulation from C. To access date and time related functions and structures, you would need to include <ctime> header file in your C++ program.

There are four time-related types: clock_t, time_t, size_t, and tm. The types clock_t, size_t and time_t are capable of representing the system time and date as some sort of integer.

The structure type tm holds the date and time in the form of a C structure having the following elements:

```
struct tm {
   int tm_sec;   // seconds of minutes from 0 to 61
   int tm_min;   // minutes of hour from 0 to 59
   int tm_hour;  // hours of day from 0 to 24
   int tm_mday;  // day of month from 1 to 31
   int tm_mon;   // month of year from 0 to 11
   int tm_year;  // year since 1900
   int tm_wday;  // days since sunday
   int tm_yday;  // days since January 1st
   int tm_isdst; // hours of daylight savings time
}
```

**Current date and time**

Consider you want to retrieve the current system date and time, either as a local time or as a Coordinated Universal Time (UTC). Following is the example to achieve the same:

```
#include <iostream>
#include <ctime>

using namespace std;

int main( ) {
   // current date/time based on current system
   time_t now = time(0);
   
   // convert now to string form
   char* dt = ctime(&now);

   cout << "The local date and time is: " << dt << endl;

   // convert now to tm struct for UTC
   tm *gmtm = gmtime(&now);
   dt = asctime(gmtm);
   cout << "The UTC date and time is:"<< dt << endl;
}
```

When the above code is compiled and executed, it produces the following result:

```
The local date and time is: Sat Jan  8 20:07:41 2011

The UTC date and time is:Sun Jan  9 03:07:41 2011
```