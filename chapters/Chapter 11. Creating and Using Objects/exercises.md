# Chapter 11 Exercises

1. Write a program, which reads from the console a year and **checks if it is a leap year.**
2. Write a program, which generates and prints on the console **10 random numbers** in the range [100, 200].
3. Write a program, which prints, on the console **which day of the week is today.**
4. Write a program, which prints on the standard output the **count of days, hours, and minutes, which have passes since the computer is started** until the moment of the program execution. For the implementation use the class `Environment`.
5. Write a program which by given two sides **finds the hypotenuse of a right triangle.** Implement entering of the lengths of the sides from the standard input, and for the calculation of the hypotenuse use methods of the class `Math`.
6. Write a program which **calculates the area of a triangle** with the following given:
   - three sides;
   - side and the altitude to it;
   - two sides and the angle between them in degrees.
7. Define your own namespace `CreatingAndUsingObjects` and place in it two classes `Cat` and `Sequence`, which we used in the examples of the current chapter. Define one more namespace and make a class, which calls the classes `Cat` and `Sequence`, in it.
8. Write a program which creates 10 objects of type `Cat`, gives them names `CatN`, where N is a unique serial number of the object, and in the end call the method `SayMiau()` for each of them. For the implementation use the namespace `CreatingAndUsingObjects`.
9. Write a program, which **calculates the count of workdays between the current date and another given date** after the current (inclusive). Consider that workdays are all days from Monday to Friday, which are not public holidays, except when Saturday is a working day. The program should keep a list of predefined public holidays, as well as a list of predefined working Saturdays.
10. You are given a **sequence of positive integer numbers** given as string of numbers separated by a space. Write a program, which **calculates their sum.** Example: "43 68 9 23 318" -> 461.
11. Write a program, which **generates a random advertising message** for some product. The message has to consist of laudatory phrase, followed by a laudatory story, followed by author (first and last name) and city, which are selected from predefined lists. For example, let’s have the following lists:
    - **Laudatory phrases:** {"The product is excellent.", "This is a great product.", "I use this product constantly.", "This is the best product from this category."}.
    - **Laudatory stories:** {"Now I feel better.", "I managed to change.", "It made some miracle.", "I can’t believe it, but now I am feeling great.", "You should try it, too. I am very satisfied."}.
    - **First name** of the author: {"Dayan", "Stella", "Hellen", "Kate"}.
    - **Last name** of the author: {"Johnson", "Peterson", "Charls"}.
    - **Cities:** {"London", "Paris", "Berlin", "New York", "Madrid"}.

    Then the program would print randomly generated advertising message like the following:
    
    ```console
    I use this product constantly. You should try it, too. I am very satisfied. -- Hellen Peterson, Berlin
    ```

12. Write a program, which calculates the value of a given numeral expression given as a string. The numeral expression consists of:
    - real numbers, for example 5, 18.33, 3.14159, 12.6;
    - arithmetic operations: +, -, *, / (with their standard priorities);
    - mathematical functions: ln(x), sqrt(x), pow(x, y);
    - brackets for changing the priorities of the operations: ( and ).

    Note that the numeral expressions have priorities, for example the expression -1 + 2 + 3 * 4 - 0.5 = (-1) + 2 + (3 * 4) - 0.5 = 12.5.
