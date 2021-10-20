# Chapter 14b Exercises

Apply the following exercises to the code you wrote for Chapter 14a, exercises 1 through 6

3. Add a **static field** for the class `Student`, which holds the number of created objects of this class.
7. Add a **static method** in class `StudentTest`, which creates several objects of type `Student` and store them in static fields. Create a **static property** of the class to access them. Write a test program, which displays the information about them in the console.

---

Apply the following exercises to the code you wrote for Chapter 14a, exercises 8 through 19.

10. To the `Phone` class, add a **static field** `nokiaN95`, which stores information about mobile phone model Nokia N95. Add a method to the same class, which displays information about this static field.
11. Add an **enumeration** `BatteryType`, which contains the values for type of the battery (Li-Ion, NiMH, NiCd, …) and use it as a new field for the class `Battery`. Update any test classes to accurately test the new `BatteryType` enumeration.

---

The following exercises do not reference previous exercises.

20. There is a **book library.** Define classes respectively for a **book** and a **library.** The library must contain a name and a list of books. The books must contain the title, author, publisher, release date and ISBN-number. In the class, which describes the library, create methods to add a book to the library, to search for a book by a predefined author, to display information about a book and to delete a book from the library.
21. Write a **test class,** which creates an object of type library, adds several books to it and displays information about each of them. Implement a test functionality, which finds all books authored by Stephen King and deletes them. Finally, display information for each of the remaining books.
22. We have a **school.** In school we have **classes** and **students.** Each class has a number of **teachers.** Each teacher has a variety of disciplines taught. Students have a name and a unique number in the class. Classes have a unique text identifier. Disciplines have a name, number of lessons and number of exercises. The task is to shape a school with C# classes. You have to define classes with their fields, properties, methods and constructors. Also define a **test class,** which demonstrates, that the other classes work correctly.
23. Write a **generic class** `GenericList<T>`, which holds a list of elements of type `T`. Store the list of elements into an array with a limited capacity that is passed as a parameter of the constructor of the class. Add methods to add an item, to access an item by index, to remove an item by index, to insert an item at given position, to clear the list, to search for an item by value, and to override the method `ToString()`.
24. Implement **auto-resizing functionality** of the array from the previous task, when by adding an element, it reaches the capacity of the array.
25. Define a class `Fraction`, which contains information about the **rational fraction** (e.g. ¼ or ½). Define a static method `Parse()` to create a fraction from a sting (for example **-3/4**). Define the appropriate properties and constructors of the class. Also write property of type `Decimal` to return the decimal value of the fraction (e.g. 0.25).
26. Write a class `FractionTest`, which tests the functionality of the class `Fraction` from previous task. Pay close attention on testing the function Parse with different input data.
27. Write a function to **cancel a fraction**, also known as simplifying a fraction (e.g. if numerator and denominator are respectively 10 and 15, fraction to be cancelled to 2/3).