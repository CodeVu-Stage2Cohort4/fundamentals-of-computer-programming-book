# Chapter 04 Solutions and Guidelines

1. Use the methods Console.ReadLine() and Int32.Parse().
1. Use Math.PI constant and the well-known geometric formulas.
1. Format the text with Write(…) or WriteLine(…) similar to the example with the letter that we looked at.
1. Use the format strings explained in the "Composite Formatting" section and the method Console.WriteLine(). Below is a piece of the code:

    ```cs
    int hexNum = 2013;
    Console.WriteLine("|0x{0,-8:X}|", hexNum);
    double fractNum = -1.856;
    Console.WriteLine("|{0,-10:f2}|", fractNum);
    ```

1. There are two approaches for solving the problem:
    - First approach: Use mathematical tricks for optimized calculation based on the fact that every fifth number is divisible by 5. Think how to implement this correctly and about the borderline cases.
    - The second approach is easier but it works slower. With a for-loop each number within the given range can be checked. You should read in Internet or in the chapter "Loops" how to use for-loops.
1. Since the problem requires a solution, which does not use conditional statements, you should use a different approach. Two possible solutions of the problem include the use of functions of class Math. The greater of the two numbers you can find with the function `Math.Max(a, b)` and the smaller with `Math.Min(a, b)`.

    Another solution to the problem includes usage of the function for taking the absolute value of a number Math.Abs(a):

    ```cs
    int a = 2011;
    int b = 1990;
    Console.WriteLine("Greater: {0}", (a + b + Math.Abs(a-b)) / 2);
    Console.WriteLine("Smaller: {0}", (a + b - Math.Abs(a-b)) / 2);
    ```

    The third solution uses bitwise operations:

    ```cs
    int a = 1990;
    int b = 2011;
    int max = a - ((a - b) & ((a - b) >> 31));
    Console.WriteLine(max);
    ```

    There is another solution which is partially correct because it uses a hidden conditional statement (the ternary ?: operator):

    ```cs
    int a = 1990;
    int b = 2013;
    int max = a > b ? a : b;
    Console.WriteLine(max);
    ```

1. You can read the numbers in five different variables and finally sum them and print the obtained sum. Note that the sum of 5 int values may not fit in the int type so you should use long.
    - Another approach is using loops. When parsing the consecutive numbers use conditional parsing with TryParse(…). When an invalid number is entered, repeat reading of the number. You can do this through while loop with an appropriate exit condition. To avoid repetitive code you can explore the for-loops from the chapter "Loops".
1. You can use the comparison statement "if" (you can read about it on the Internet or from the chapter "Conditional Statements"). To avoid repeating code you can use the looping construct "for" (you could read about it online or in the chapter "Loops").
1. You should use a for-loop (see the chapter "Loops"). Read the numbers one after another and accumulate their sum in a variable, which then display on the console at the end.
1. Use a combination of loops (see the chapter "Loops") and the methods Console.ReadLine(), Console.WriteLine() and Int32.Parse().
1. More about the Fibonacci sequence can be found in Wikipedia at: http://en.wikipedia.org/wiki/Fibonacci_sequence. For the solution of the problem use 2 temporary variables in which store the last 2 calculated values and with a loop calculate the rest (each subsequent number in the sequence is a sum of the last two). Use a for-loop to implement the repeating logic (see the chapter "Loops").
1. Accumulate the sum of the sequence in a variable inside a while-loop (see the chapter "Loops"). At each step compare the old sum with the new sum. If the difference between the two sums Math.Abs(current_sum – old_sum) is less than the required precision (0.001), the calculation should finish because the difference is constantly decreasing and the precision is constantly increasing at each step of the loop. The expected result is 1.307.