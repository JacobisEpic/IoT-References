# Design Pattern – Multiple Files in C

Most of the example code in the ESP distro consists of a main file
(.c) and a header file (.h). Necessary modules are linked to the main
program via #include statements.

Many programs are created by starting with one
example code unit and then adding many, many units that contribute to
the whole. This can become cumbersome to manage and creates barriers
to breaking down a solution to units that can be developed by
individual contributors. Better: create a set of files that are all
brought together by the main program. For example:

Main program (main.c)

(sub_program_1.c)

(sub_program_2.c)




## References
- [Modular Programming in C])https://www.embedded.com/modular-programming-in-c/)




