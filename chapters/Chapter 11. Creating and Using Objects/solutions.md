# Chapter 11 Solutions and Guidelines

1. Use DateTime.IsLeapYear(year).
1. Use the class Random. You may generate random numbers in the range [100, 200] by calling Random.Next(100, 201).
1. Use DateTime.Today.DayOfWeek.
1. Use the property Environment.TickCount, in order to get the count of passed milliseconds. Use the fact that one second has 1,000 milliseconds; one minute has 60 seconds; one hour has 60 minutes and one day has 24 hours.
1. The hypotenuse of a rectangular triangle could be found with the Pythagorean Theorem a2 + b2 = c2, where a and b are the two sides, and c is the hypotenuse. Take square root of the two sides of the equation in order to get the length of the hypotenuse. Use the Sqrt(…) methods of the Math class.
1. For the first sub-problem of the task use the Heron’s Formula S= v(p(p-a)(p-b)(p-c)), where p=(a+b+c)/2. For the second sub-problem use the formula: S=  (a*h_a)/2. For the third sub-problem use the formula: S =  (a * b * sin(?))/2. For the sine use the System.Math class.
1. Make a new project in Visual Studio, right click on the folder and choose the menu Add ? New Folder. Then enter the name of the folder and press [Enter], right click on the newly made folder and choose Add ? New Item… from the list choose Class, for the name of the new class enter Cat and press [Add]. Change the definition of the newly created class with the definition, which we gave to this chapter, to put the classes in a namespace. Make the same to the class Sequence.
1. Create an array with 10 elements of type Cat. Create 10 objects of type Cat in a loop (use a constructor with parameters) and assign them to the corresponding element of the array. For the serial number of the objects use the method NextValue() of the Sequence class. In the end again in an array use the method SayMiau() for each of the array elements.
1. Use the class System.DateTime and the methods in it. You can execute a loop from the current date (DateTime.Now.Date) to the end date, consecutively incrementing the day by the method AddDays(1) and count the working days according to your country (e.g. all days except Saturday and Sunday and a few fixed non-working official holidays).
    - Another approach that might work is to subtract the dates to find the TimeSpan between them (DateTime values can be subtracted, just like a numbers). This will give you the count of days between the dates. You will need to perform some additional calculations to find how much weekends are included in this count and discard them.
1. Use String.Split(' ') to split the string by spaces. Then use Int32.Parse(…) to extract the separate numbers from the obtained string array as int values and sum them.
1. Use the class System.Random and its method Next(…) to select a random laudatory phrase, laudatory story, first name, last name and city and combine them.
1. Calculating a numeral expression is quite hard and is unlikely a beginner programmer to solve it correctly without external help. As a start check out the article in Wikipedia about the "Shunting-yard algorithm" (en.wikipedia.org/wiki/Shunting-yard_algorithm) describing how to convert an expression from to postfix notation (reversed Polish notation), and the article about calculating a postfix expression (en.wikipedia.org/wiki/Reverse_Polish notation). There are really much special cases, so be sure to test your solution carefully.