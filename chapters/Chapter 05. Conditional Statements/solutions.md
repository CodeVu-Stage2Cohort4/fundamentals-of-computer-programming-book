# Chapter 05 Solutions and Guidelines

1. Look at the section about `if`-statements.
2. A multiple of non-zero numbers has a positive product, if the **negative multiples are even number.** If the count of the negative numbers is odd, the product is negative. If at least one of the numbers is zero, the product is also zero. Use a counter `negativeNumbersCount` to keep the **number of negative numbers.** Check each number whether it is negative and change the counter accordingly. If some of the numbers is 0, print "0" as result (the zero has no sign). Otherwise print "+" or "-" depending on the condition (`negativeNumbersCount % 2 == 0`).
3. Use **nested `if`-statements,** first checking the first two numbers then checking the bigger of them with the third.
4. First **find the smallest** of the three numbers, and then **swap it with the first one.** Then check if the second is greater than the third number and if yes, swap them too.

    Another approach is to check all possible orders of the numbers with a series of `if-else` checks: `a≤b≤c`, `a≤c≤b`, `b≤a≤c`, `b≤c≤a`, `c≤a≤b` and `c≤b≤a`.

    A **more complicated** and more general solution of this problem is to put the numbers in an array and use the `Array.Sort(...)` method. You may read about arrays in the chapter "Arrays".
5. Use a `switch` statement to check for all possible digits.
6. From math it is known, that a **quadratic equation** may have one or two real roots or no real roots at all. In order to calculate the real roots of a given quadratic equation, we first calculate the **discriminant** (D) by the formula: D = b<sup>2</sup> - 4ac. If the discriminant is **zero,** then the quadratic equation has one double real root and it is calculated by the formula: <!-- $x_{1,2}=\frac{-b}{2a}$ --> <img style="transform: translateY(0.1em); background: white;" src=".\assets\svg\UwU433lH7J.svg">. If the value of the discriminant is **positive,** then the equation has **two distinct real roots,** which are calculated by the formula: <!-- $x_{1,2}=\frac{-b\pm\sqrt{b^{2}-4ac}}{2a}$ --> <img style="transform: translateY(0.1em); background: white;" src=".\assets\svg\1VricIGaLF.svg">. If the discriminant is **negative,** the quadratic equation has **no real roots.**
7. Use nested `if` statements. You could use the loop structure `for`, which you could read about in the "Loops" chapter of the book or on the Internet.
8. First input a variable, which indicates **what type will be the input,** i.e. by entering 0 the type is `int`, by 1 is `double` and by 2 is `string`.
9. Use nested `if` statements or series of **31 comparisons,** in order to check all the sums of the 31 subsets of the given numbers (without the empty one). Note that the problem in general (with N numbers) is complex and using loops will not be enough to solve it.
10. Use `switch` statement or a sequence of `if-else` constructs and at the end print at the console the calculated points.
11. Use nested `switch` statements. Pay special attention to the numbers from 0 to 19 and those that end with 0. There are **many special cases!**
    
    You might benefit from using **methods** to reuse the code you write, because printing a single digit is part of printing a 2-digit number which is part of printing 3-digit number. You may read about methods in the chapter "Methods".