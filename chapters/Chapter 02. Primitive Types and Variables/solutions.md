# Chapter 02 Solutions and Guidelines

1. Look at the ranges of the numerical types in C# described in this chapter.
1. Consider the number of digits after the decimal point. Refer to the table that describes the sizes of the types `float`, `double` and `decimal`.
1. Two floating-point variables are considered equal if their difference is less than some predefined precision (e.g. `0.000001`):

    ```cs
    bool equal = Math.Abs(a - b) < 0.000001;
    ```

1. Look at the section about Integer Literals. To easily convert numbers to a different numeral system use the built-in Windows calculator. For a **hexadecimal** representation of the literal **use prefix** ``0x``.
1. Look at the section about Character Literals.
1. Look at the section about Boolean Literals.
1. Look at the sections about Strings and Object Data Type.
1. Look at the sections about Strings and Object Data Type. To cast from object to string use **typecasting**:

    ````cs
    string str = (string)obj;
    ````

1. Look at the section about Character Literals. It is necessary to use the **escaping character** `\"` or **verbatim strings**.
1. Use `Console.WriteLine(...)`, the character '`o`' and spaces.
1. Use `Console.WriteLine(...)`, the character © and spaces. Use Windows Character Map in order to find the Unicode code of the sign "©".
    - Note that the console may display "`c`" instead of "©" if it does not support Unicode. If this happens, you might be unable to do anything to fix it. Some versions of Windows just do not support Unicode in the console even when you explicitly set the character encoding to UTF-8:

    ```cs
    Console.OutputEncoding = System.Text.Encoding.UTF8;
    ```

    You may need to change the font of your console to some font that supports the "©" symbol, e.g. "Consolas" or "Lucida Console".
1. For the names use type `string`, for the manager use type `bool`, and for the unique number and age use some integer type.
1. Use **third temporary variable** for exchanging the variables:

    ```cs
    int a = 5;
    int b = 10;

    int oldA = a;
    a = b;
    b = oldA;
    ```

    To swap integer variables **other solutions** exist which do not use a third variable. For example, if we have two integer variables `a` and `b`:

    ```cs
    int a = 5;
    int b = 10;

    a = a + b;
    b = a - b;
    a = a - b;
    ```

    You might also use the **XOR swap algorithm** for exchanging integer values: <http://en.wikipedia.org/wiki/XOR_swap_algorithm>.
