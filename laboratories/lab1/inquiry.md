## Laboration 1

- Support Standard Markdown / CommonMark and GFM(GitHub Flavored Markdown);
- Full-featured: Real-time Preview, Image (cross-domain) upload, Preformatted text/Code blocks/Tables insert, Code fold, Search replace, Read only, Themes, Multi-languages, L18n, HTML entities, Code syntax highlighting...;

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


#### What is the purpose of -Wall and -g, when passed as arguments to g++?

The purpose of  -Wall is to set all the warnings and print all warning messages.
On the other hand, -g is used for  generating additional symbolic debuggging information for the  gdb debugger.

```
> gdb ./<executable>
```

#### How can you store the previous mentioned flags in a variable in the makefile?

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
