# Chapter 03 Solutions and Guidelines

1. Take the **remainder of dividing the number by 2** and check if it is 0 or 1 (respectively the number is odd or even). **Use `%` operator** to calculate the remainder of integer division.
2. Use a logical "AND" `(&&` operator) and the remainder operation `%` in division. You can also solve the problem by only one test: the division of 35 (think why).
3. Divide the number by 100 and save it in a new variable, which then divide by 10 and take the remainder. The remainder of the division by 10 is the third digit of the original number. Check if it is equal to 7.
4. Use **bitwise "AND"** on the current number and the number that has 1 only in the third bit (i.e. number 8, if bits start counting from 0). If the returned result is different from 0 the third bit is 1:

    ```cs
    int num = 25;
    bool bit3 = (num & 8) != 0;
    ```

5. The formula for **trapezoid surface** is: S = (a + b) * h / 2.
6. Search the Internet for **how to read integers** from the console and use the formula for rectangle area calculation. If you have difficulties see instructions on the next problem.
7. Use the following code to **read the number from the console**:

    ```cs
    Console.Write("Enter number: ");
    int number = Convert.ToInt32(Console.ReadLine());
    ```

    Then **multiply by 0.17** and print it.
8. Use the **Pythagorean Theorem** `a2 + b2 = c2`. The point is inside the circle when `(x*x) + (y*y) ? 5*5`.
9. Use the code from the previous task and **add a check for the rectangle**. A point is inside a rectangle with walls parallel to the axes, when in the same time it is right of the left wall, left of the right wall, down from the top wall and above the bottom wall.
10. To get the individual **digits of the number** you can divide by 10 and take the remainder of the division by 10:

    ```cs
    int a = num % 10;
    int b = (num / 10) % 10;
    int c = (num / 100) % 10;
    int d = (num / 1000) % 10;
    ```

11. Use bitwise operations:

    ```cs
    int n = 35; // 00100011
    int p = 6;
    int i = 1; // 00000001
    int mask = i << p; // Move the 1-st bit left by p positions

    // If i & mask are positive then the p-th bit of n is 1
    Console.WriteLine((n & mask) != 0 ? 1 : 0);
    ```

12. The task is similar to the previous one.
13. Use bitwise operations by analogy with the previous two problems. You can reset the bit at position `p` in the number `n` as follows:

    ```plain
    n = n & (~(1 << p));
    ```

    You can set bits in the unit at position `p` in the number `n` as follows:

    ```plain
    n = n | (1 << p);
    ```

    Think how you can combine the above two hints.
14. Read about **loops** in the Internet or in the chapter "Loops". Use a loop and check the number for divisibility by all integers from 1 to the square root of the number. Since **n < 100**, you can find in advance all prime numbers from 1 to 100 and checks the input over them. The **prime numbers** in the range [1...100] are: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89 and 97.
15. Use 3 times a combination of **getting and setting a bit at a given position**. The first exchange is given below:

    ```cs
    int bit3 = (num >> 3) & 1;
    int bit24 = (num >> 24) & 1;
    num = num & (~(1 << 24)) | (bit3 << 24);
    num = num & (~(1 << 3)) | (bit24 << 3);
    ```

16. Extend the solution of the previous problem to perform a **sequence of bit exchanges in a loop**. Read about loops in the chapter "Loops".
