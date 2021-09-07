# Chapter 14 Solutions and Guidelines

1. Use enum for subjects and universities.
1. To avoid repetition of source code call constructors from each other with keyword this(<parameters>).
1. Use the constructor of the class as a place where the number of objects of class Student is increasing.
1. Display on the console in all fields of the class Student, followed by a blank line.
1. Define as private all members of the class Student and then using Visual Studio (Refactor -> Encapsulate Field) define automatically the public get / set methods to access these fields.
1. Create a few students and display the whole information for each one of them.
1. You can use the static constructor to create instances in the first access to the class.
1. Declare three separate classes: GSM, Battery and Display.
1. Define the described constructors and create a test program to check if classes are working properly.
1. Define a private field and initialize it at the time of its declaration.
1. Use enum for the type of battery. Search in Internet for other types of batteries for phones, except these in the requirements and add them as value of the enumeration.
1. Override the method ToString().
1. In classes GSM, Battery and Display define suitable private fields and generate get / set. You can use automatic generation in Visual Studio.
1. Add a method PrintInfo() in class GSM.
1. Read about the class List<T> in Internet. The class GSM has to store its conversations in a list of type List<Call>.
1. Return as a result the list of conversations.
1. Use the built-in methods of the class List<T>.
1. Because the tariff is fixed, you can easily calculate the total price of all calls.
1. Follow the instructions directly from the requirements of the task.
1. Define classes Book and Library. For a list of books use List<Book>.
1. Follow the instructions directly from the requirements of the task.
1. Create classes School, SchoolClass, Student, Teacher, Discipline and define into them their respective fields, as described in the instructions of the task. Do not use the word "Class" as a class name, because in C# it has special meaning. Add methods for printing all the fields from each of the classes.
1. Use your knowledge concerning generic classes. Check out all input parameters of the methods, just to make sure that no element can access an invalid position.
1. When you reach the capacity of the array, create a new array with a double size and copy all old elements in the new one.
1. Write a class with two private decimal fields, which hold information relevant to the numerator and denominator of the fraction. Among other requirements in the task, redefine in appropriate standard the features for each object: Equals(…), GetHashCode(), ToString().
1. Figure out appropriate tests, for which your function may give incorrect results. Good practice is first to write the tests, then to implement their specific functionality.
1. Search for information in Internet for the "greatest common divisor (GCD)" and the Euclidean algorithm for its calculation. Divide the numerator and denominator of their greatest common divisor and you will get the cancelled fraction.