# C++ Journey: Part 1 - Introduction to Series

<!--more-->

## Introduction to Series

### Why am I learning C++?
So, the main thing is "Why am even bothering with this?". As you may or may not know, I want to become a computational particle physicist, as my young mind inspires, and even though I hate programming, I have decided to study C++, Python, MATLAB, Mathematica, etc. But why C++? Well... Geant4 and ROOT are written especially for C++, so I must study C++.

Then, what will be these category's purpose? My main purpose for creating this category is to create an archive for learning C++ from a newbie physics major point of view, so that if I need to refresh my memory or just check something I can come back here and check it.

### Starting Notes: What are our resources?

The main resources of these notes are mentioned below: 

1. [Programming -- Principles and Practice Using C++](https://www.stroustrup.com/programming.html)
2. [Murach’s C++ Programming](https://www.murach.com/shop/murach-s-c-programming-382-detail)

I will mostly use the first book mentioned because it seemed more comprehensive for the time being. It may seem like I am copy-pasting but I will try to elaborate more on most of the topics and try to create more examples.

## Actual C++ Part of This Article

### How does C++ work?

It was really fun to use the power of GitHub Copilot and create a mermaid diagram to show how a C++ program works or is created.

1. We write the C++ source code, for example below code
```cpp
    #include<iostream>
    int main()
    {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
```
2. Run compiler, for example, `g++ -E hello-world.cpp -o hello-world`
   1. The compiler first runs the preprocessor, which evaluates header files, header files are not getting compiled.
   2. Second, the compiler takes the output from the preprocessor and makes an object file.

{{< mermaid >}}
graph LR
A[C++ Source File] --> B[Preprocessor]
B --> C[Translation Unit]
C --> D[Compiler]
D --> E[Object File]
{{< /mermaid >}}

### An example code

In the above explanation, we have used a code you might remember

```cpp
    #include<iostream>
    int main()
    {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
```

1. Here first line includes our header file `iostream`. We need this line for `std::cout` and 'std::endl' to run. 
2. In the second line, we see a `main` function definition. Every C++ program has a main function, it is the first function that runs. 
3. In the fourth line, we see `std::cout << "Hello world!" << std::endl;`. This line of code prints out `Hello world!` sentence to the console and then gets to a new line.
4. In the last line, we see `return 0;`. In this function, we must return an integer in order code to work. In C++, as a convention, returning 0 from the `main` function indicates that it ran successfully.
