# Chapter 09 Solutions and Guidelines

1. Use a method that takes the name as parameter of type `string`.
2. Use the expression `Max(a, b, c) = Max(Max(a, b), c)`.

    To **test the code** check whether the results from the invoked methods is correct for a set of examples that cover the most interesting cases, e.g. Max(1,2)=2; Max(3,-1)=3; Max(-1,-1)=-1; Max(1,2,444444)=444444; Max(5,2,1)=5; Max(-1,6,5)=6; Max(0,0,0)=0; Max(-10,-10,-10)=-10; Max(2000000000,-2000000001,2000000002)=2000000002; etc.
    
    You may write a **generic method** that works not just for int but for any other type T using the following declaration:

    ```cs
    static T Max<T>(T a, T b) where T : IComparable<T> { … }
    ```

    Read more about the concept of **generic methods** in the section "Generic Methods" of chapter "Defining Classes".

    Instead of creating a program that checks whether the method works correctly, you can search in Internet for information about "**unit testing**" and **write unit tests** for your methods. You may also read about unit testing in the section "Unit Testing" of chapter "High-Quality Code".
3. Use the **reminder of division by 10** and then a `switch` statement.
4. The method must take as parameter an array of integer numbers (`int[]`) and the number that has to be counted (`int`). Test it with few examples like this: `CountOccurences(new int[]{3,2,2,5,1,-8,7,2}, 2)` -> 3.
5. Just **perform a check.** The elements of the first and the last position in the array will be compared only with their left and right neighbor. Test examples like `GreaterThanNeighbours(new int[]{1,3,2}, 1)` -> `true` and `GreaterThanNeighbours(new int[]{1}, 0)` -> `true`.
6. Invoke the method from the **previous problem** in a `for`-loop.
7. There are two solutions:

    **First solution:** Let the number is `num`. So while `num` ≠ 0 we print its last digit (`num % 10`) and then divide `num` by 10.

    **Second solution:** Convert the number into a string `string` and print it in a reverse order with a `for`-loop. This is a bit cheater’s approach.
8. The reader must implement own method **that calculates the sum of very big numbers.** The digits on position zero will keep the ones; the digit on the first position will keep the tenths and so on. When two very big numbers are about to be calculated, the ones of their sum will be equal to `(firstNumber[0] + secondNumber[0]) % 10`, the tenths on other side will be equal to `(firstNumber[1] + secondNumber[1]) % 10 + (firstNumber[0] + secondNumber[0])/10` and so on.
9. First write a method that finds **the biggest element in array** and then modify it to find the biggest element in given range of the array, e.g. in the elements at indexes [3...10]. Finally find the **biggest number in the range [1...n-1]** and **swap it with the first element,** then find the biggest element in the range [2...n-1] and swap it with the second element of the array and so on. Think when the algorithm should finish.
10. The reader must implement own method that calculates the **product of very big numbers,** because the value of `100!` does not fit in variable of type `ulong` or `decimal`. The numbers can be represented in an array of reversed digits (one digit in each element). For example, the number 512 can be represented as `{2, 1, 5}`. Then the multiplication can be implemented in the way done in the elementary school (multiply digit by digit and then calculate the sum).
    
    Another easier way to work with extremely large numbers such as 100! is by using the library `System.Numerics.dll` (you have to add a reference to it in your project). Look for Information in internet about how to use the class `System.Numerics.BigInteger`.
    
    Finally calculate in a loop `k!` for k = 1, 2, ..., n.
    
11. Firstly, create the necessary **methods.** To **create the menu** display a list in which the actions are represented as numbers (1 – reverse, 2 – average, 3 – equation). Ask the user to choose from 1 to 3.
12. **Use arrays to represent the polynomial** and the arithmetic rules that you know from math. For example the polynomial (3x<sup>2</sup> + x - 5) can be represented as an array of the numbers {-5, 1, 3}. Bear in mind that it is useful at the zero position to put the coefficient for x<sup>0</sup> (in our case -5), at the first position – the coefficient for x<sup>1</sup> (in our case 1) and so on.
1. Use the instructions from the **previous task** and the rules for polynomial multiplication that you know from math. How to **multiple polynomials** can be read here: <http://www.purplemath.com/modules/polymult.htm>.