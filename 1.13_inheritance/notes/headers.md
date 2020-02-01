# Organizing your code
* classes are usually forward declared in a .h file maintaining the same name as the class (.cpp)
  * class.cpp & class.h
* this means .h will have a delcartion of each function or class and .cpp will provide the definition

## Why bother with this?
* mutiple source files can then include the header file without having to 
* then you dont need to know all the dependencies of the library
    * for example, when you include **iostream** you automatically get std::cout,
    becasue **iostream** has foward declared std::cout.
    * thus, the preproccessor will copy all of the content (including forward delcarations into the file doing the #include)

## What belongs in a .h file?   
* object & function declarations
* Const, constexpr, and symbolic constants).

### What doesn't belong?
* function definitions and object definitions

# header guard
* recall that you cannot declare some thing twice

<pre>
    #include &ltstring&gt
    #include &ltstring&gt
</pre>
* obviously these is an error
* but here is a more subtle exmample of double declaration of string

[see example here](https://www.learncpp.com/cpp-tutorial/header-guards/)

# Example of including
<pre>
<code>
#include <iostream>
int add(int x, int y); //forward declaration 
 
int main(){
    std::cout << add(3,4);
}
</code>
</pre>

Problem with forward declaration of add here is that other files who want to
use add can't really include this file because of main. so its better to but
all code we want to use in multiple files in a .h file. Techincally they could
include main.cpp, but if the other file who is including the add forward
declaration happens to have a main function then there will be an error.
## better example
### add.h
<pre>
#ifndef ADD_H
#define ADD_H
int add(int x, int y); 
#endif
</pre>

### main.cpp
<pre>
#include "add.h"

int main(){
    add(2,2);
}
</pre>
