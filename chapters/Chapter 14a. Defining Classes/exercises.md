# Chapter 14a Exercises

The exercises in Chapter 14b will reference the exercises you complete here. It would be a good idea to commit the results of these exercises to GitHub!

1. Define a class `Student`, which contains the following **information about students:** full name, course, subject, university, e-mail and phone number.
2. Declare several **constructors** for the class `Student`, which have different lists of parameters (for complete information about a student or part of it). Data, which has no initial value to be initialized with `null`. Use nullable types for all non-mandatory data.
<!--  -->
4. Add a **method** in the class `Student`, which displays complete information about the student.
5. Modify the current source code of `Student` class so as to **encapsulate** the data in the class using **properties.**
6. Write a class `StudentTest`, which has to test the functionality of the class `Student`.
<!--  -->

---

8. Define a class, which contains information about a **mobile phone:** model, manufacturer, price, owner, features of the battery (model, idle time and hours talk) and features of the screen (size and colors).
9. Declare several **constructors** for each of the classes created by the previous task, which have different lists of parameters (for complete information about a phone or part of it). Data fields that are unknown have to be initialized respectively with `null` or 0.
<!--  -->
12. Add a method to the class `Phone`, which returns information about the object as a `string`.
13. Define properties to encapsulate the data in classes `Phone`, `Battery` and `Display`.
14. Write a class `PhoneTest`, which has to **test the functionality** of class `Phone`. Create few objects of the class and store them into an array. Display information about the created objects.
15. Create a class `Call`, which contains information about a call made via mobile phone. It should contain information about date, time of start and duration of the call.
16. Add a property for keeping a **call history** – `CallHistory`, on the `Phone` class, which holds a list of call records.
17. In `Phone` class add methods for adding and deleting calls (`Call`) in the archive of mobile phone calls. Add method, which deletes all calls from the archive.
18. In `Phone` class, add a method that calculates the total amount of calls (`Call`) from the archive of phone calls (`CallHistory`), as the price of a phone call is passed as a parameter to the method.
19. Create a class `PhoneCallHistoryTest`, with which to test the functionality of the class `Phone`, from task 12, as an object of type `Phone`. Then add to it a few phone calls (`Call`). Display information about each phone call. Assuming that the price per minute is 0.37, calculate and display the total cost of all calls. Remove the longest conversation from archive with phone calls and calculate the total price for all calls again. Finally, clear the archive.
