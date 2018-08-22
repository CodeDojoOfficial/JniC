<h1 align="center">
  <a href="https://github.com/CodeDojoOfficial/JniC"><img src="https://codedojoofficial.github.io/image/jnic-logo.png"></a>
  <br>
</h1>

<p align="center">
  <a href="https://github.com/CodeDojoOfficial/JniC/releases/tag/1.0.0"><img src="https://img.shields.io/badge/version-1.0.0-green.svg?longCache=true&style=for-the-badge"></a>
  <a href="#a-java-native-method-tool"><img src="https://img.shields.io/badge/java%20native%20interface-compiler-blue.svg?longCache=true&style=for-the-badge"></a>
</p>

<h3 align="center" style="font-size: 25px;">
  <font>JniC - The Java Native Interface Compiler Tool</font>
</h3>

## A Java Native Method Tool

Never heard of a native method in Java? A native method is a method that is implemented later in the compilation process. However, if this just seems strange, I mean, why would you want a method that you have to implement later? But it is much better than that. A native method's source code, is written in the **C**/**C++** programming language!

If you don't know how to program in at least C, then you might want to learn that before you do anything with this.

You can do lot's of things that you wouldn't normally be able to do in java, with a native method. But doing this takes time. JniC is an interactive command line tool that lets you create your programs in as little as 15 seconds, not including the time it takes to write and compile the C source code.

Download it now for free on [Linux](https://github.com/CodeDojoOfficial/JniC/blob/master/src/jnic-linux.sh 'jnic-linux.sh Source File'), [DOS](https://github.com/CodeDojoOfficial/JniC/blob/master/src/jnic-dos.sh 'jnic-dos.sh Source File'), or [Darwin (Mac OS X)](https://github.com/CodeDojoOfficial/JniC/blob/master/src/jnic-darwin.sh 'jnic-darwin.sh Source File')! Or you can download the most recent official release [here](https://github.com/CodeDojoOfficial/JniC/releases/latest 'Latest Release')!

## Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
  - [How to Use](#how-to-use)
- [Frequently Asked Questions](#frequently-asked-questions)
  - [Can you create these libraries with multiple packages in mind?](#q-can-you-create-these-libraries-with-multiple-packages-in-mind)

## Installation

Click one of the links below to *download* the most updated stable version of JniC for your OS

| OS | Latest Version | Download Link |
|:---|:--------------:|:-------------:|
| Linux | 1.0.0 | [jnic-linux-1.0.0.sh](https://github.com/CodeDojoOfficial/JniC/releases/download/1.0.0/jnic-linux-1.0.0.sh) |
| DOS | 1.0.0 | [jnic-dos-1.0.0.sh](https://github.com/CodeDojoOfficial/JniC/releases/download/1.0.0/jnic-dos-1.0.0.sh) |
| Darwin (Mac OS X) | 1.0.0 | [jnic-darwin-1.0.0.sh](https://github.com/CodeDojoOfficial/JniC/releases/download/1.0.0/jnic-darwin-1.0.0.sh) |

## Quick Start

This section assumes you are ready to go, and the software for your specific OS is currently running in the terminal. (Use `source my-jnic-file.sh` to load) All you need now is to have a basic understanding of how the software works.

## How to Use

In this section you will learn how to create a native method in java, call it, and have the source code in C run.

To start, launch open your favorite editor to work with java. We'd prefer this test project to be in a main folder by itself. Write the following program:

**File: Program.java**

```java
public class Program {
  
  public static native void printText(); // The native method we call
  static { // This block will be called as the class is being loaded into memory.
    System.loadLibrary("program"); // Load the soon to be created libprogram.so, or program.dll on DOS.
  }
  
  public static void main(String[] args) {
    printText(); // Executing the C code.
  }
  
}
```

Alright! Your're done with the Java source code. Now to write the source code for the native method "`printText()`".

Open your command line and navigate to the directory with your source code in it. Enter `jnic Program`, and you should see this:

```
$ jnic Program
Input: Program
What would you like the name of this library to be? Don't include the lib prefix or .so suffix.
```

Here, we will enter the name that we had in the loadLibrary method, "program".

```
program
Ok. The resulting file name will be libprogram.so and your static block should contain `System.loadLibrary("program");'.
Starting initialization progress...
Compiling code...
Code compilation successful.
Generating header files...
Header code generation successful.
Generating implementation C++ files...
C++ implementation file generation successful.
Launching VI Improved editor for each file. Write and quit using :wq in normal mode (Get to normal mode by using ESC), and the writing will continue to the last file.
```

Now, if you have followed through so far, you are probably in the Vim text editor. If you are new to it, open a shell and type `vimtutor` to learn.

Add this to the bottom of the file that pops up:

```c
JNIEXPORT void JNICALL Java_Program_printText(JNIEnv *env, jclass self) { // Naming convention: Java_<package_and_class_name>_<method_name>
  printf("Hello, world!\n"); // Comes from <stdio.h> header
  return;
}
```

Save and Quit, and the program will finish.

```
Editing complete.
Compiling C++ code...
C++ compilation successful!
Be careful. The LD_LIBRARY_PATH environment variable is now loaded. If you wish to add on, just enter the following:
export LD_LIBRARY_PATH="yourdir:$LD_LIBRARY_PATH"
Ok! You're done! Just enter `java <MyClass>', and you will run the native code along side your java code!
$ 
```

As the last line says, all we have to do is call `java Program`. So let's do just that!

```
$ java Program
Hello, world!
$
```

Yay! It works! You just wrote your first Java program using native methods!

## Frequently Asked Questions

We know you probably have many questions by now, and we would love to answer them, but to avoid repeat questions, here are some of our most commonly asked questions.

## Q: Can you create these libraries with multiple classes in mind?

**A:** Yes! Yes you can. All you have to do is run the command at the root of all packages. Not a directory lower. Thanks for asking!
