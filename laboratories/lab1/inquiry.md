## Laboration 1

### Building and Compilation

#### Where can you find the manual to g++?

There many ways to find the manual for g++ compiler.  
The manual can be find locally by typing on the terminal the following commands : 
```
> man g++
```

```
> man gcc | col -b > gcc.txt
```

Furthemore, the manual can also be find online for example at  https://linux.die.net/man/1/g++


####What is the purpose of -Wall and -g, when passed as arguments to g++?

The purpose of  -Wall is to set all the warnings and print all warning messages.
On the other hand, -g is used for  generating additional symbolic debuggging information for the  gdb debugger.

```
> gdb ./<executable>
```

####How can you store the previous mentioned flags in a variable in the makefile?

The previous flags can be stored in two variables CXX  for g++
and CXXFLAGS  for  -Wall -g as show at the code snipet below :

```
# *****************************************************
# Variables to control Makefile operation
# CPPFLAGS: params for the C preprocessor (e.g. -I <path>,-D <symbol>, etc.)
# CFLAGS: params for the C compiler (e.g. -Wall,-g, etc)
# CXXFLAGS: params for the C++ compiler (e.g. -Wall,-g, etc)
# LDFLAGS: params for the  linker (e.g. -L<path>, etc)
# LDLIBS: the libraries for linking into the executable (e.g.-lm, etc)
CXX = g++
CXXFLAGS = -Wall -g

%.out: %.cpp
	$(CXX) -std=c++11 $(CXXFLAGS) $*.cpp -o $*.out

```
#### Find and write down 4 other arguments tp g++ that you think might be useful and write a short motivation why you selected these specific 4 arguments.
```
CXX = g++
CXXFLAGS = -Wall -g -pedantic

%.out: %.cpp
		$(CXX) -I -pthread -std=c++11 $(CXXFLAGS) -O $*.cpp -o $*.out

```

- -I (include) :
- Pedantic : 
- pthread (multithreading) :
- O (optimization) :
- lm ()



#### What is the difference between an object file, and an executable?

When a source file (.cpp) is compiled, first the precessor directives are translated with an appropriate content; thereafter,  an object file is created. The object file is the machine language code of the source file.

The object file can not be executed due to its lack of pre-defined programming elements such as library functions (not present in headers). The pre-defined programming elements  and object file are linked by the linker and an executable (.exe ,.out) is created. An executable is a linked object fiel with standard librarbies ready to be exectuted. 

#### What is a forward declaration?

Forward declaration is a declaration of an identifier for which the complete definition is not yet given. A signature of a function is given before its complet definition :

```
boolean match(int u, int v)

boolean match(int u, int v)
{
 	return u == v;
}
```

#### Why is it not possible to have class A containing a B object and B containing an A object?

`class A { B b; };`
`class B { A a; };`

Because the class B is declared on the stack, and we do need the complete structure of class B in order to allaocate an sufficient size of memory; however, in this case the size of the class is not known beforehand.

#### Why are include guards needed?

Guards are   particular constructs used for avoiding multiple inclusion wiht the include directive when programming in  C/C++. An alternative is to use pragma once. 


### GIT

