# Chapter 12 Exercises

1. Find out all exceptions in the `System.IO.IOException` **hierarchy.**
2. Find out all standard exceptions that are part of the **hierarchy** holding the class `System.IO.FileNotFoundException`.
3. Find out all standard exceptions from `System.ApplicationException` **hierarchy.**
4. Explain the concept of **exceptions** and **exception handling,** when they are used and how to **catch** exceptions.
5. Explain when the statement `try-finally` is used. Explain the relationship between the statements `try-finally` and `using`.
6. Explain the **advantages** when using exceptions.
7. Write a program that takes a positive integer from the console and prints the **square root** of this integer. If the input is **negative or invalid** print "Invalid Number" in the console. In all cases print "Good Bye".
8. Write a method `ReadNumber(int start, int end)` that reads an integer from the console in the range `[start...end]`. In case the input integer is not valid or it is not in the required range throw appropriate exception. Using this method, write a program that takes 10 integers a<sub>1</sub>, a<sub>2</sub>, …, a<sub>10</sub> such that 1 < a<sub>1</sub> < ... < a<sub>10</sub> < 100.
9. Write a method that takes as a parameter the name of a **text file,** **reads the file and returns its content as `string`.** What should the method do if and **exception is thrown?**
10. Write a method that takes as a parameter the name of a binary file, **reads the content** of the file and returns it as an array of bytes. Write a method that **writes the file content** to another file. Compare both files.
11. Search for information in Internet and define your own class for exception `FileParseException`. The exception has to contain the name of the processed file and the number of the row where the problem is occurred. Add appropriate constructors in the exception. Write a program that reads integers from a text file. If the during reading a row does not contain an integer throw `FileParseException` and pass it to the calling method.
12. Write a program that gets from the user the full path to a file (for example `C:\Windows\win.ini`), reads the content of the file and prints it to the console. Find in MSDN how to us the `System.IO.File.ReadAllText(...)` method. Make sure all possible exceptions will be caught and a user-friendly message will be printed on the console.
13. Write a program to download a file from Internet by given URL, e.g. <http://introprogramming.info/wp-content/themes/introprograming_en/images/Intro-Csharp-Book-front-cover-big_en.png>.