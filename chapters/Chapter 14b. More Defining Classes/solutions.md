# Chapter 14b Solutions and Guidelines

3. Use the constructor of the class as a place where the number of objects of class `Student` is increasing.
<!--  -->
7. You can use the **static constructor** to create instances in the first access to the class.
   
---

10. Define a `private` field and initialize it at the time of its declaration.
11. Use `enum` for the **type of battery.** Search in Internet for other types of batteries for phones, except these in the requirements and add them as value of the enumeration.
<!--  -->

---

20. Define classes `Book` and `Library`. For a list of books use `List<Book>`.
21. Follow the instructions directly from the requirements of the task.
22. Create classes `School`, `SchoolClass`, `Student`, `Teacher`, `Discipline` and define into them their respective fields, as described in the instructions of the task. Do not use the word "`Class`" as a class name, because in C# it has special meaning. Add methods for printing all the fields from each of the classes.
23. Use your knowledge concerning **generic classes.** Check out all input parameters of the methods, just to make sure that no element can access an invalid position.
24. When you reach the capacity of the array, **create a new array with a double size** and copy all old elements in the new one.
25. Write a class with two `private decimal` fields, which hold information relevant to the **numerator** and **denominator** of the fraction. Among other requirements in the task, redefine in appropriate standard the features for each object: `Equals(...)`, `GetHashCode()`, `ToString()`.
26. Figure out appropriate **tests,** for which your function may give incorrect results. Good practice is **first to write the tests,** then to implement their specific functionality.
27. Search for information in Internet for the **"greatest common divisor (GCD)"** and the **Euclidean algorithm** for its calculation. Divide the numerator and denominator of their greatest common divisor and you will get the cancelled fraction.