## Laboration 1

### 1. Building and Compilation

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


### 2. GIT


#### What does git show HEAD~:01/makefile show?

Git log useful information in the background. One of the things Git does in the background is to keep a“reflog”— a log of where  HEAD
and branch references have been for the last few months. 
```
> git reflog
0efe11a (HEAD -> master) HEAD@{0}: commit: changed makefile 222l
af125b9 HEAD@{1}: commit: changed makefile
0b7ef9c (origin/master, origin/HEAD) HEAD@{2}: commit: changed stuffs
4ddf68d HEAD@{3}: commit: changed makefile
52a8634 HEAD@{4}: commit: changed makefile
3030f9d HEAD@{5}: clone: from https://gits-15.sys.kth.se/cprog20/benedith-labbar.git
```
The general rule is : 

```
git show [REVISION]:[FILENAME]
```
HEAD~ shows the first parent or ancestror of the current file. 

```
CXX = g++
CXXFLAGS = -Wall -g -pedantic

%.out: %.cpp
        $(CXX) -I -pthread -std=c++11 $(CXXFLAGS) -O $*.cpp -o $*.out
```

#### What does git show HEAD:01/makefile show?

HEAD shows the current modified version of the file makefile. 

```
CXX = g++
CXXFLAGS = -std=c++11 -g -Wall -pedantic

main.out: main.cpp hello.o
	$(CXX) $(CXXFLAGS) main.cpp hello.o -o main.out
	
hello.o: hello.cpp
	$(CXX) $(CXXFLAGS) -c hello.cpp
	
clean:
	rm -f *.o *.out
```

#### What would git show HEAD~~:01/makefile show?

HEAD~ shows the first parent or ancestror of the first parent of the current file - grand-parent. 

```
%.out: %.cpp
       g++ -std=c++11 -g -Wall $*.cpp -o $*.out
```

#### What does the ~ in the previous git show commands mean?

In bref, the sign ~ means ancestor relation. The first parent. 

#### Why can you not ommit 01 in the previous commands (i.e. git show HEAD~:makefile instead of git show HEAD~:01/makefile)

Because we need the realtive path to the file, not just the name of the file. 

#### Sometimes you may need to do a git pull before you can do a git push how can that be?

Sometimes there is conflicts that need to be resolved and merged with the current version of the work, if there are possibly multiple coontributors to the project. Therefore, it is required to pull first in order to have an updated version (merging possibly required) and then pull up the new version. 

#### What is the purpose of the .git_ignore file and why should *.o *.out *.exe be in this file when developing C++?

.gitignore contains the list of file extension that the system must ignore by avoiding their presentation, add and tracking. For example the file with extension *.o *.out *.exe  are filed rpduced by the build systems; therefore, there is no need to track them as they are dependent of the build system and can be produced by the makefile. 


### 3.  How make works

#### If you invoke touch hello.cpp prior to invoking make, how many files were rebuilt?

![](https://github.com/benedictmulongo/Cplusplus_experiments/blob/master/laboratories/lab1/IMG_20200216_175006.jpg)

Two files are rebuilded such as hello.o and main.out.

#### Why?

The reason is due to the dependency shown in the figure above.  hello.o and main.out are dependent of hello.cpp; therefore, they do need a rebuild. 

#### Why do you think make checks the modification timestamp of the relevant files as part of deciding what to do?

the last time the file was modified (content has been modified) is a good indication of whether or not the file has have its content modified. 

#### What is the difference between an implicit rule and an explicit rule in a makefile?

Explicit rules tell make which files depend on the compilation of other files, and the commands required to compile a particular file. They take the following form:

targetfile : sourcefiles
	commands 
	

Implicit rules are just like explicit rules, except listed without commands. make uses the suffixes on the files to determine what command to perform. For example, the implicit rule:

test.o: test.c io.h

 will cause the following command to be executed:

$(CC) $(CFLAGS) -c test.c io.h

http://pages.cs.wisc.edu/~beechung/ref/Makefiles-short.html

#### What does $* mean inside a makefile?

%.o: %.c
  $*   # the 'stem' with which an implicit rule matches ("foo" in "foo.c")

https://devhints.io/makefile

### 4.  clang compiler

The new makefile is defined as follow :

``` 
CXX = clang++
CXXFLAGS = -std=c++11 -g 

main.out: main.cpp hello.o
	$(CXX) $(CXXFLAGS) main.cpp hello.o -o main.out
	
hello.o: hello.cpp
	$(CXX) $(CXXFLAGS) -c hello.cpp
	
clean:
	rm -f *.o *.out
```

### 5.  Assignment an improved world of hello

#### What is the purpose of std::cout, std::cerr, and std::clog, respectively?
#### How does #include work?

### 6.  Train Spotting (debugging)

#### Why does not powerof return the expected value (16), when invoked with 2 and 4?
Because the for loop is guarded and conversely do not behaves as it was intendend. 
we need to change :

from 
```c++
  for (int i = 0; i < y; ++i);
    res = res * x;
```
to 
```c++
  for (int i = 0; i < y; ++i)
  {
    res = res * x;
  }
```

#### Why does not adding_a_decimal output 100000?

We convert float to double. As show in the code listing below.
``` c++
void adding_a_decimal(float step) {
  double sum = step;
  for (int i = 0; i < 1000*1000; ++i) {
    sum += step;
  }
  std::cout << std::setw(4) << sum << std::endl;
}
```

![](https://github.com/benedictmulongo/Cplusplus_experiments/blob/master/laboratories/lab1/float_double_sizes.png)
>Float and double size 
	
As shown in the figure above, float has sufficient memory size to hold a number with 5 zeros. However, after multiple sucessive addition of float number the precision becomes inaccurate; therefore, the precision must be hold by converting float to double. 


#### Describe how weird.out is invoked by echo '3.1415' | ./weird.out

The pipe operator is used for sending data from one program to another. 
(|) Send the output from one program as input to another program.

in bref, the output '3.1415' to the standard in of the ./weird.out program. 

#### Why does not y compare equal to 3.1415?

The floating-poit are imprecise; therefore, the direct equality between two float-point may be incorrect although they both numbers are strictly equal. 


#### Is there any difference in behavior if we compare y to 3.1415f, if so; why?

There is a difference, because in this case the comparison is performed between two numbers of same type. Therefore, the comparison is more stable and precise given two numbers of same type - float.  


#### Describe and motivate the recommended method to use when trying to determine if two floating-point values are equal.

The recommended method to compare two float-points is to check the magnitude of the difference of the two numbers. If the difference is significantly small, then it may be concluded that the numbers are equal. 

```
if (|x -y| < 0.00001 ) # x - y can be considered equal
```

### 7. unit testing


### 8.  Will It Float? (temporaries, resource management, valgrind)

### 9.  valgrind a memory management analyzer
