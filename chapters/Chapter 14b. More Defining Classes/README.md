# Chapter 14b. More Defining Classes

## In This Chapter

In this chapter, we will expand on the different types and more advanced concepts when defining classes. We will explain what the **static elements** of a class are – fields (including **constants**), properties, and methods and how to use them properly. In this chapter we will also introduce generic types (**generics**), enumerated types (**enumerations**) and **nested classes.**

## Static Classes and Static Members

We call an element static when it is declared with the modifier `static`. In C# we can declare fields, methods, properties, constructors, and classes as static.

We will first consider the **static elements** of a class or in other words, we will look at the fields, methods, properties, and constructors of a class, and then we will study the concept of the static class.

### What the Static Elements Are Used For?

Before we study the working principle of the static elements, let’s see the reasons why we need to use them.

#### Method to Sum Two Numbers

Let’s imagine that we have a class with a single method that always works in the same manner. For example, its task is to get two numbers and return their sum as a result. In this scenario, there is no matter exactly which object of that class is going to implement that method since it will always do the same thing – adding two numbers together, independent of the calling object.

In practice **the behavior of the method does not depend on the object state** (the values in the object field). So why the need to create an object to accomplish that method provided that the method does not depend on any of the objects of that class? Why not just get the class to implement that method?

#### Instance Counter for Given Class

Consider a different scenario. Let’s say we want to keep in our program the current number of objects, which have been created by a given class. How will we keep that variable, which stores **the number of created objects?**

As we know, we will not be able to store the variable as a class field because for each created object there will be created a copy of that field, initialized with the default value. Every single object will store its field for indication of the number of objects and the objects will not be able to **share information.**

It looks like the counter should be outside a class field rather than inside it. In the following subsections, we will find out how to deal with such a problem.

### What Is a Static Member?

Formally speaking, a **static member** of the class is every field, property, method, or other members, which has a **static** modifier in its declaration. That means that fields, methods, and properties, marked as static, belong to the particular class rather than to any particular object of the given class.

Therefore, when we mark a field, method, or property as `static`, we can use them without creating any object of the given class. All we need is to have access (visibility) to the class so that we can call the object’s static methods or its static fields and properties.

| :warning: | Static elements of the class can be used without creating an object of the given class. |
|:--:|:--|

On the other hand, if we have created objects of the given class then its **static fields and properties will be shared** and there will be only one copy of the static field or property which will be shared among all objects of the given class. Because of that reason in the VB.NET language we have the keyword **shared** instead of the **static** keyword.

### Static Fields

When we create objects from a given class, each of them holds different values in its fields. For example, consider again the class `Dog`:

```cs
public class Dog
{
    // Instance variables
    private string name;
    private int age;
}
```

There are two fields in the class, one for the name – `name` and another one for the age – `age`. Every object, each of these fields, has its own value, which is stored in a different place in the memory for every object.

Sometimes, however, we want to have **common fields** for all objects of a given class. To achieve that, we have to use the `static` modifier in the field declarations. As we already said, such fields are called **static fields.** In the literature they are also called **class variables.**

We say that the static fields are **class associated,** rather than associated with any object from the particular class. That means that all objects, created by the description of a class **share** the static fields of the class.

| :warning: | All objects, created by the description of a given class (that is, instances of a given class), share the static fields of the class. |
|:--:|:--|

### Declaration of Static Fields

The static fields are declared the same way as the class fields. If there is an access modifier, the keyword **static** should be added after it.

```cs
[<access_modifier>] static <field_type> <field_name>
```

Here is how a field named `dogCount` would look like. The field stores information about the count of the created objects from the class `Dog`:

| Dog.cs |
|---|

```cs
public class Dog
{
    // Static (class) variable
    static int dogCount;

    // Instance variables
    private string name;
    private int age;
}
```

The static fields are created when we try to access them for the first time (read/modify). After their creation, they are initialized with the default values of their types.

### Initialization during Declaration

If during the static field declaration we set an initialization value, it will be assigned to the particular static field. The **initialization executes only once** when the field is accessed for the first time right after the assignment has finished. The next time when the field is accessed that field initialization will not execute.

We can append the **static field initialization** in the example above:

```cs
// Static variable – declaration and initialization
static int dogCount = 0;
```

This initialization will complete during the first invocation to the static field. When we access some static field, an amount of memory will be reserved for it and it will be initialized with its default values. If the field has initialization during declaration (like it is in our case with the `dogCount` field) this initialization will execute. If we try later to access the field from another part of our program this process will not repeat, because the static field already exists and is initialized.

### Accessing Static Fields

In contrast to the common (non-static) class fields, the static fields that are associated with the particular class can be accessed through an external class. To do that we need to put a **"dot" notation** this way:

```cs
<class_name>.<static_field_name>
```

For example, if we want to print the value of the static field that holds the number of created objects of our class `Dog` we should do that:

```cs
static void Main()
{
    // Access to the static variable through class name
    Console.WriteLine("Dog count is now " + Dog.dogCount);
}
```

The result of the `Main()` method is:

```console
Dog count is now 0
```

If we have a method in the class, which is defined as a static field, we can access it directly without the class name, because it is known by default.

```cs
<static_field_name>
```

### Modification of the Static Field Values

As we said before, the static variables are **shared between all objects** of the class and do not belong to any object of the particular class. That way any object can access and modify the static field values and at the same time, other objects can "see" the modified values.

That’s why if we want to count the number of created objects of the class `Dog`, we should use a **static field** and increment it by one every time the constructor is invoked, i.e. every time we create an object of our class.

```cs
public Dog(string name, int age)
{
    this.name = name;
    this.age = age;

    // Modifying the static counter in the constructor
    Dog.dogCount += 1;
}
```

We access the static field from the class `Dog` so we can use the following code to access the field `dogCount`:

```cs
public Dog(string name, int age)
{
    this.name = name;
    this.age = age;

    // Modifying the static counter in the constructor
    dogCount += 1;
}
```

The first way is preferable, it is clear that the field in the class `Dog` is static. The code is more readable.

Let’s create some objects of the class `Dog` and print out their number to check if we are right:

```cs
static void Main()
{
    Dog dog1 = new Dog("Jackie", 1);
    Dog dog2 = new Dog("Lassy", 2);
    Dog dog3 = new Dog("Rex", 3);

    // Access to the static variable
    Console.WriteLine("Dog count is now " + Dog.dogCount);
}
```

The output of the example is:

```console
Dog count is now 3
```

### Constants

Before we finish with the static fields we should get familiar with one more specific type of static field.

Like the constants of mathematics, in C# special fields of a class called **constants** can be created. Once declared and initialized **constants always have the same value** for all objects of a particular type.

In C# constants are of two types:

1. Constants, the values of which are extracted during the compilation of the program (**compile-time constants**).
2. Constants, the values of which are extracted during the execution of the program (**run-time constants**).

### Compile-Time Constants (const)

Constants, which are calculated at compile time (compile-time constants), are declared as follows, using modifier `const`:

```cs
[<access_modifiers>] const <type> <name>;
```

Constants, which are declared with the special word `const`, are static fields. Nevertheless, the use of modifier `static` is not required (nor allowed by the compiler) in their declaration.

| :warning: | Although the constants declared with a modifier const are static fields, they must not and cannot use the static modifier in their declaration. |
|:--:|:--|

For example, if we want to declare as a constant the number "PI", which is known to us from mathematics, this can be done as follows:

```cs
public const double PI = 3.141592653589793;
```

The value we assign to a particular constant can be an expression, which has to be calculated by the compiler at compile time. For example, as we know from mathematics, the constant "PI" can be represented as the approximate result of the division of numbers 22 and 7:

```cs
public const double PI = 22d / 7;
```

When we try to print the value of the constant:

```cs
static void Main()
{
    Console.WriteLine("The value of PI is: " + PI);
}
```

The command line will display:

```console
The value of PI is: 3.14285714285714
```

If we do not give a value to a constant at its declaration, but later, we will get a compilation error. For example, if we take the example of the constant PI, we first declare the constant and later try to give it a value:

```cs
public const double PI;

// ... Some code ...

public void SetPiValue()
{
    // Attempting to initialize the constant PI
    PI = 3.141592653589793;
}
```

The compiler will issue an error like this one, indicating the line, where the constant is declared:

```console
A const field requires a value to be provided
```

Let’s pay attention, again:

| :warning: | Constants declared with modifier const must be initialized at the moment of their declaration. |
|:--:|:--|

### Assigning Constant Values at Runtime

Having learned how to declare constants that are being initialized at compile-time, let’s consider the following example: we want to create a class for color (`Color`). We will use the so-called **Red-Green-Blue (RGB) color model,** according to which, each color is represented by mixing the three primary colors – red, green, and blue. These three primary colors are represented as three integers in the range from 0 to 255. For example, black is represented as (0, 0, 0), white as (255, 255, 255), blue – (0, 0, 255) etc.

In our class we declare three integer fields for red, green, and blue light and a constructor that accepts values for each of them:

| Color.cs |
|---|

```cs
class Color
{
    private int red;
    private int green;
    private int blue;

    public Color(int red, int green, int blue)
    {
        this.red = red;
        this.green = green;
        this.blue = blue;
    }
}
```

As some colors are used more frequently than others (for example, black and white) we can **declare constants for them,** with the idea that the users of our class will take them for granted, instead of creating their own objects for these particular colors every time. To do this, we modify the code of our class as follows, adding the declaration of the following color constants:

| Color.cs |
|---|

```cs
class Color
{
    public const Color Black = new Color(0, 0, 0);
    public const Color White = new Color(255, 255, 255);

    private int red;
    private int green;
    private int blue;

    public Color(int red, int green, int blue)
    {
        this.red = red;
        this.green = green;
        this.blue = blue;
    }
}
```

Strangely, when we try to compile, we **get the following error:**

```console
'Color.Black' is of type 'Color'. A const field of a reference type other than string can only be initialized with null.
'Color.White' is of type 'Color'. A const field of a reference type other than string can only be initialized with null.
```

This is so because in C#, constants, declared with the modifier `const`, can be only of the following types:

1. Primitive types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`.
2. **Enumerated types** (discussed in section "Enumerations" at the end of this chapter).
3. **Reference types** (mostly the type string).

The problem with the compilation of the class in our example is connected with the reference types and the restriction on the compiler not to allow simultaneous use of the operator `new` when declaring a constant when this constant is declared with the modifier `const` unless the reference type can be calculated at compile time.

As we can guess, the only reference type, which can be calculated at compile time while using the operator `new` is `string`.

Therefore, the only possibilities for reference type constants that are declared with modifier `const` are, as follows:

1. The constants must be of type `string`.
2. The value, which we assign to the constant of reference type, other than `string`, is `null`.

We can formulate the following definition:

| :warning: | Constants declared with modifier `const` must be of primitive, enumeration or reference type, and if they are of reference type, this type must be either a `string` or the value, that we assign to the constant, must be `null`. |
|:--:|:--|

Thus, using the modifier `const`, we will not be able to declare the constants `Black` and `White` of type `Color` in our color class because they aren’t `null`. The next section will show us how to deal with this problem.

### Runtime Constants (readonly)

When we want to declare reference type constants, which cannot be calculated during the compilation of the program, we must use a combination of `static readonly` modifiers, instead of the `const` modifier.

```cs
[<access_modifiers>] static readonly <reference-type> <name>;
```

Accordingly, `<reference-type>` is a type the value of which cannot be calculated at compilation time.

The compilation is successful if we replace `const` by `static readonly` in the last example of the previous section:

```cs
public static readonly Color Black = new Color(0, 0, 0);
public static readonly Color White = new Color(255, 255, 255);
```

### Naming the Constants

The constant's names in C# follow the **PascalCase** rule according to Microsoft’s official C# coding convention. If the constant is composed of several words, each new word after the first one begins with a capital letter. Here are some examples of correctly named constants:

```cs
// The base of the natural logarithms (approximate value)
public const double E = 2.718281828459045;
public const double PI = 3.141592653589793;
public const char PathSeparator = '/';
public const string BigCoffee = "big coffee";
public const int MaxValue = 2147483647;
public static readonly Color DeepSkyBlue = new Color(0,104,139);
```

Sometimes naming in style **ALL-CAPS** is used but it is not officially supported by the Microsoft code conventions, even though it is widely distributed in programming:

```cs
public const double FONT_SIZE_IN_POINTS = 14; // 14pt font size
```

The examples made it clear that the difference between `const` and `static readonly` fields is in the moment of their value assignments. The compile-time constants (`const`) must be initialized at the moment of declaration, while the run-time constants (`static readonly`) can be initialized at a later stage, for example in one of the constructors of the class in which they are defined.

### Using Constants

Constants are used in programming to **avoid repetition of numbers, strings, or other common values** (literals) in the program and to enable them to change easily. The use of constants instead of brutally hardcoded repeating values facilitates readability and maintenance of the code and is a highly recommended practice. According to some authors, all literals other than `0`, `1`, `-1`, empty string, `true`, `false` and `null` must be declared as constants, but this can make it difficult to read and maintain the code instead of making it simple. Therefore, it is believed that **values, which occur more than once in the program or are likely to change over time, must be declared as constants.**

In the chapter "High-Quality Programming Code" will we learn in detail when and how to use constants efficiently.

### Static Methods

Like static fields, we declare a method as static if we want it to be associated only with the class and not with a particular class object.

### Declaration of Static Methods

To declare a **static method** syntactically means that we must add the keyword `static` in the method’s declaration:

```cs
[<access_modifier>] static <return_type> <method_name>()
```

Let’s for example declare the method of summing two numbers, which we discussed at the beginning of this section:

```cs
public static int Add(int number1, int number2)
{
    return (number1 + number2);
}
```

### Accessing Static Methods

Like static fields, static methods can be **accessed with the "dot" notation** (the dot operator) applied to the name of the class and the class name can be skipped if the calling is performed by the same class, in which the static method is declared. Here is an example of calling the static method `Add(...)`:

```cs
static void Main()
{
    // Call the static method through its class
    int sum = MyMathClass.Add(3, 5);

    Console.WriteLine(sum);
}
```

### Access between Static and Non-Static Members

In most cases **static methods are used to access static fields** in the class they have been defined. For example, if we want to declare a method, which returns the number of the created objects of the `Dog` class, it must be static, because our counter will be static too:

```cs
public static int GetDogCount()
{
    return dogCount;
}
```

But when we examine how static and non-static methods and fields can be accessed, not all combinations are allowed.

### Accessing Non-Static Members from Non-Static Method

Non-static methods can access non-static fields and other non-static methods of the class. For example, in the `Dog` class we can declare method `PrintInfo()`, which displays information about our dog:

| Dog.cs |
|---|

```cs
public class Dog
{
    // Static variable
    static int dogCount;

    // Instance variables
    private string name;
    private int age;

    public Dog(string name, int age)
    {
        this.name = name;
        this.age = age;

        dogCount += 1;
    }

    public void Bark()
    {
        Console.Write("wow-wow");
    }

    // Non-static (instance) method
    public void PrintInfo()
    {
        // Accessing instance variables – name and age
        Console.Write("Dog's name: " + this.name + "; age: "
            + this.age + "; often says: ");

        // Calling instance method
        this.Bark();
    }
}
```

Of course, if we create an object of the `Dog` class and call its `PrintInfo()` method:

```cs
static void Main()
{
    Dog dog = new Dog("Doggy", 1);
    dog.PrintInfo();
}
```

The result will be the following:

```console
Dog's name: Doggy; age: 1; often says: wow-wow
```

### Accessing Static Elements from Non-Static Method

We can access static fields and static methods of the class from non-static methods. As we learned earlier, this is because static methods and variables are bound by class, rather than a specific method and the static elements can be accessed from any object of the class, even of external classes (as long as they are visible to them).

For example:

| Circle.cs |
|---|

```cs
public class Circle
{
    public static double PI = 3.141592653589793;

    private double radius;

    public Circle(double radius)
    {
        this.radius = radius;
    }

    public static double CalculateSurface(double radius)
    {
        return (PI * radius * radius);
    }

    public void PrintSurface()
    {
        double surface = CalculateSurface(radius);
        Console.WriteLine("Circle's surface is: " + surface);
    }
}
```

In the example, we provide access to the value of the static field `PI` of the non-static method `PrintSurface()`, by calling the static method `CalculateSurface()`. Let’s try to call this non-static method:

```cs
static void Main()
{
    Circle circle = new Circle(3);
    circle.PrintSurface();
}
```

After the compilation and the execution, the following result will be printed on the console:

```console
Circle's surface is: 28.2743338823081
```

### Accessing Static Elements of the Class from Static Method

We can call a static method or static field of the class from another static method without any problems.

For example, let’s consider our class for mathematical calculations. We have declared the constant `PI`, in it. We can declare a static method for finding the length of the circle (the formula for finding the perimeter of a circle is **2πr,** where **r** is the radius of the circle), that uses the constant `PI` for calculating the perimeter of a circle. Then, to show that the static method can call another static method, we can call the static method for finding the perimeter of a circle from the static method `Main()`:

| MyMathClass.cs |
|---|

```cs
public class MyMathClass
{
    public const double PI = 3.141592653589793;

    // The method applies the formula: P = 2 * PI * r
    static double CalculateCirclePerimeter(double r)
    {
        // Accessing the static variable PI from a static method
        return (2 * PI * r);
    }

    static void Main()
    {
        double radius = 5;

        // Accessing static method from other static method
        double circlePerimeter = CalculateCirclePerimeter(radius);

        Console.WriteLine("Circle with radius " + radius +
            " has perimeter: " + circlePerimeter);
    }
}
```

The code is compiled without errors and displays the following output:

```console
Circle with radius 5.0 has perimeter: 31.4159265358979
```

### Accessing Non-Static Elements from Static Method

Let’s look at the most interesting case of a combination of accessing non-static and static elements of the class – **accessing non-static elements from a static method.**

We should know that from the static method we can neither access non-static fields nor call non-static methods. This is because static methods are bound to the class and do not "know" any object of the class. Therefore, the keyword `this` cannot be used in static methods – it is bound to a specific instance of the class. When we try to access non-static elements of the class (fields or methods) from the static method, we will always get a compilation error.

#### Unauthorized Access to Non-Static Field – Example

If in our class `Dog` we try to declare a static method `PrintName()`, which returns, as a result, the value of the non-static field name declared in the class:

```cs
public static void PrintName()
{
    // Trying to access non-static variable from static method
    Console.WriteLine(name); // INVALID
}
```

Accordingly, the compiler will respond with an **error message:**

```console
An object reference is required for the non-static field, method, or property 'Dog.name'
```

If we try to access the field in the method, via the **keyword** `this`:

```cs
public void string PrintName()
{
    // Trying to access non-static variable from static method
    Console.WriteLine(this.name); // INVALID
}
```

The compiler will still not be satisfied and this time will **fail to compile** the class and will display the following message:

```console
Keyword 'this' is not valid in a static property, static method, or static field initializer
```

#### Illegal Call of Non-Static Method from Static Method – Example

Now we will try to call the non-static method from the static method. Let declare in our class `Dog`, the non-static method `PrintAge()`, which prints the value of the field `age`:

```cs
public void PrintAge()
{
    Console.WriteLine(this.age);
}
```

Accordingly, let’s try from the method `Main()`, which we declare in the class `Dog`, to call this method without creating an object of our class:

```cs
static void Main()
{
    // Attempt to invoke non-static method from a static context
    PrintAge(); // INVALID
}
```

When we try to compile we will **get the following error:**

```console
An object reference is required for the non-static field, method, or property 'Dog.PrintAge()'
```

The result is similar if we try to cheat the compiler, trying to call the method via the keyword `this`:

```cs
static void Main()
{
    // Attempt to invoke non-static method from a static context
    this.PrintAge(); // INVALID
}
```

Accordingly, as with the attempt to access the non-static field of a static method using the keyword this, the compiler displays the following error message and **fails to compile our class:**

```console
Keyword 'this' is not valid in a static property, static method, or static field initializer
```

From the examples, we can make the following conclusion:

| :warning: | Non-static elements of the class may NOT be used in a static context. |
|:--:|:--|

The problem with the access to non-static elements of the class of static method has a single solution – these non-static elements are accessed by reference to an object:

```cs
static void Main()
{
    Dog myDog = new Dog("Lassie", 2);
    string myDogName = myDog.name;
    Console.WriteLine("My dog \"" + myDogName +"\" has age of ");
    myDog.PrintAge();
    Console.WriteLine("years");
}
```

Accordingly, this code is compiled and the result is:

```console
My dog "Lassie" has age of 2 years
```

### Static Properties of the Class

Although rare, it is sometimes convenient to use and declare not the object characteristics, but the ones of the class. They possess the same characteristics as the properties related to the particular object of a particular class, which we discussed above, but with the difference that the **static properties refer to the class** (not its objects).

As we can guess, all we need to do to turn a simple property into a static one is to **add the `static` keyword in its declaration.**

The static properties are declared as follows:

```cs
[<modifiers>] static <property_type> <property_name>
{
    // ... Property's accessors methods go here
}
```

Let’s consider an example. We have a class that describes a system. We can create many objects from it, but the model of the system has a version and a vendor, which are common to all instances created from this class. We can make the version and the vendors as static properties of the class:

| SystemInfo.cs |
|---|

```cs
public class SystemInfo
{
    private static double version = 0.1;
    private static string vendor = "Microsoft";

    // The "version" static property
    public static double Version
    {
        get { return version; }
        set { version = value; }
    }

    // The "vendor" static property
    public static string Vendor
    {
        get { return vendor; }
        set { vendor = value; }
    }

    // ... More (non)static code here ...
}
```

In this example, we have chosen to keep the value of static properties in static variables (which are logical, since they are bound only to the class). The properties that we consider are `Version` and `Vendor`, respectively. For each of them, we have created static methods for reading and modification. Thus, all objects of this class will be able to retrieve the current version and vendor of the system, which describes the class. Accordingly, if one day an upgrade of the system version is done and the value becomes `0.2`, as a result, each object will receive the new version by accessing the class property.

### Static Properties and the Keyword "this"

Like static methods, the keyword `this` cannot be used in the static properties, as the static property is associated only with the class and does not "recognize" objects of a class.

| :warning: | The keyword `this` cannot be used in static properties. |
|:--:|:--|

### Accessing Static Properties

Like the static fields and methods, static properties can be accessed by **"dot" notation,** applied only to the name of the class in which they are declared.

To be sure, let’s try to access the property `Version` through a variable of the class `SystemInfo`:

```cs
static void Main()
{
    SystemInfo sysInfoInstance = new SystemInfo();
    Console.WriteLine("System version: " +
        sysInfoInstance.Version);
}
```

When we try to compile the above code, we get the following error message:

```console
Member 'SystemInfo.Version.get' cannot be accessed with an instance reference; qualify it with a type name instead
```

Accordingly, if we try to access the static properties through class name, the code compiles and works correctly:

```cs
static void Main()
{
    // Invocation of static property setter
    SystemInfo.Vendor = "Microsoft Corporation";

    // Invocation of static property getters
    Console.WriteLine("System version: " + SystemInfo.Version);
    Console.WriteLine("System vendor: " + SystemInfo.Vendor);
}
```

The code is compiled and the result of its execution is:

```console
System version: 0.1
System vendor: Microsoft Corporation
```

Before proceeding to the next section, let’s look at the printed value of the property `Vendor`. It is "`Microsoft Corporation`", although we have initialized it with the value "`Microsoft`" in the `SystemInfo` class. This is because we changed the value of the property `Vendor` of the first line of the `Main()` method, by calling its method of modification.

| :warning: | Static properties can be accessed only through dot notation, applied to the name of the class in which they are declared. |
|:--:|:--|

### Static Classes

For complete understanding, we have to explain that we can also declare classes as static. Similar to static members, a class is static, when the keyword `static` is used in its declaration.

```cs
[<modifiers>] static class <class_name>
{
    // ... Class body goes here
}
```

When a class is declared as static, it is an indication that **this class contains only static members** (i.e. static fields, methods, properties) and cannot be instantiated.

The use of static classes is rare and most often associated with the **use of static methods and constants,** which do not belong to any particular object. For this reason, the details of static classes go beyond the scope of this book. The curious reader can find more information on the site of the Microsoft Developer Network (MSDN): http://msdn.microsoft.com/en-us/library/79b3xss3.aspx.

### Static Constructors

To finish the section on static class members, we should mention that classes may also have **static constructor** (i.e. constructor that has the static keyword in its declaration):

```cs
[<modifiers>] static <class_name>([<parameters_list>])
{
}
```

Static constructors can be declared both in static and non-static classes. They are **executed only once** when the first of the following two events occurs for the first time:

1. An object of the class is created.
2. A static element of the class is accessed (field, method, property).

Most often static constructors are used for the initialization of static fields.

#### Static Constructor – Example

Consider an example for the **use of a static constructor.** We want to make a class that quickly calculates the square root of an integer and returns the whole part of the result, which is also an integer. Since calculating the square root is a time-consuming mathematical operation involving calculations with real numbers and calculating convergent series, it is a good idea for these calculations to be done once at program startup and then to use the already calculated values. Of course, to make such **pre-computing of all square roots** in a given range, we must first define this range and it should not be too wide (e.g. from 1 to 1000). Then we need, at first request for a square root of a number, to recalculate all the square roots in this range and then to return the already calculated value. Upon the following request for a square root, all values in this range will have already been calculated and returned directly. If the program is never required to calculate the square root, preliminary calculations should not be fulfilled at all.

Through the described process initially, some CPU time is invested for preliminary calculations, but then the extraction of the square root later is done very quickly. If we have multiple calculations of the square root, the pre-calculation will significantly increase the performance.

All this can be implemented in one **static class with a static constructor,** in which the square roots will be recalculated. The results, which have already been calculated, can be **stored in a static array.** A **static method** can be used to extract the already pre-calculated value. Since the preliminary calculations are being performed in the static constructor, if the class for pre-calculated square roots is not used, they will not be executed and CPU time and memory will be saved.

This is how the implementation might look like:

```cs
static class SqrtPrecalculated
{
    public const int MaxValue = 1000;

    // Static field
    private static int[] sqrtValues;

    // Static constructor
    static SqrtPrecalculated()
    {
        sqrtValues = new int[MaxValue + 1];
        for (int i = 0; i < sqrtValues.Length; i++)
        {
            sqrtValues[i] = (int)Math.Sqrt(i);
        }
    }

    // Static method
    public static int GetSqrt(int value)
    {
        if ((value < 0) || (value > MaxValue))
        {
            throw new ArgumentOutOfRangeException(String.Format(
                "The argument should be in range [0...{0}].",
                MaxValue));
        }
        return sqrtValues[value];
    }
}

class SqrtTest
{
    static void Main()
    {
        Console.WriteLine(SqrtPrecalculated.GetSqrt(254));
        // Result: 15
    }
}
```

## Structures

In C# and .NET Framework, there are two implementations of the concept of "class" from object-oriented programming: **classes** and **structures.** Classes are defined through the keyword `class` while the structures are defined through the keyword `struct`. The main difference between a structure and a class is that:

- Classes are reference types (references to some address in the heap that holds their members).
- Structures (structs) are value types (they directly hold their members in the program execution stack).

#### Structure (struct) – Example

Let’s define a **structure** to hold a point in the 2D space, similar to the class Point defined in the section "Example of Encapsulation":

| Point2D.cs |

```cs
struct Point2D
{
    private double x;
    private double y;

    public Point2D(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    public double X
    {
        get { return this.x; }
        set { this.x = value; }
    }

    public double Y
    {
        get { return this.y; }
        set { this.y = value; }
    }
}
```

The only difference is that now we defined `Point2D` as `struct`, not as `class`. `Point2D` is a structure, a value type, so its instances behave like `int` and `double`. They are value types (not objects), which means they cannot be `null` and they are **passed by value** when taken as method parameters.

### Structures are Value Types

Unlike classes, the **structures are value types.** To illustrate this we will play a bit with the `Point2D` structure:

```cs
class PlayWithPoints
{
    static void PrintPoint(Point2D p)
    {
        Console.WriteLine("({0},{1})", p.X, p.Y);
    }

    static void TryToChangePoint(Point2D p)
    {
        p.X++;
        p.Y++;
    }

    static void Main()
    {
        Point2D point = new Point2D(3, -2);
        PrintPoint(point);
        TryToChangePoint(point);
        PrintPoint(point);
    }
}
```

If we run the above example, the result will be as follows:

```console
(3,-2)
(3,-2)
```

The **structures are value types** and when passed as parameters to a method **their fields are copied** (just like `int` parameters) and when changed inside the method, the change affects only the copy, not the original. This can be illustrated by the next few figures.

First, the `point` variable is created which holds a value of (3, -2):

![](assets/structure-point-1.png)
 
Next, the method `TryToChangePoint(Point2D p)` is called and it copies the value of the variable `point` into **another place in the stack,** allocated for the parameter `p` of the method. When the parameter `p` is changed in the method’s body, it is modified in the stack and this **does not affect the original variable** `point` which was previously passed as an argument when calling the method:

![](assets/structure-point-2.png)
  
If we change `Point2D` from `struct` to `class`, the result will be very different:

```console
(3,-2)
(4,-1)
```

This is because the variable `point` will be now passed by reference (not by value) and its value will be shared between `point` and `p` in the heap. The figure below illustrates what happens in the memory at the end of the method `TryToChangePoint(Point2D p)` when `Point2D` is a class:

![](assets/structure-point-3.png)
 
### Class or Structure?

How to decide **when to use a class and when a structure?** We will give you some general guidelines.

**Use structures** to hold simple data structures consisting of a few fields that come together. Examples are coordinates, sizes, locations, colors, etc. Structures are not supposed to have functionality inside (no methods except simple ones like `ToString()` and comparators). Use structures for **small data structures consisting of a set of fields** that should be passed by value.

**Use classes** for more complex scenarios where you combine data and programming logic into a class. If you have logic, use a class. If you have more than a few simple fields, use a class. If you need to pass variables by reference, use a class. If you need to assign a `null` value, prefer using a class. If you prefer working with a reference type, use a class.

Classes are used more often than structures. Use structs as the exception, and **only if you know well what are you doing!**

There are a few other **differences between class and structure** in that classes are reference types and structures are values types, but we will not going to discuss them. For more details refer to the following article in MSDN: http://msdn.microsoft.com/en-us/library/ms173109.aspx.

## Enumerations

Earlier in this chapter, we discussed what constants are, how to declare and use them. In this connection, we will now consider a part of the C# language, in which a variety of logically connected constants can be linked through language. These language constructs are the so-called **enumerated types.**

### Declaration of Enumerations

**Enumeration** is a structure, which resembles a class but differs from it in that in the class body we can **declare only constants.** Enumerations can take values only from the constants listed in the type. An enumerated variable can have as a value one of the listed in the type constants but cannot have value `null`.

Formally speaking, the enumerations can be declared using the reserved word `enum` instead of `class`:

```cs
[<modifiers>] enum <enum_name>
{
    constant1 [, constant2 [, [, ... [, constantN]]
}
```

Under `<modifiers>` we understand the access modifiers `public`, `internal`, and `private`. The identifier `<enum_name>` follows the rules for class names in C#. Constants separated by commas are declared in the enumeration block.

Consider an example. Let’s define an enumeration for the days of the week (we will call it `Days`). As we can guess, the constants that will appear in this particular enumeration are the **names of the weekdays:**

| Days.cs |
|---|

```cs
enum Days
{
    Mon, Tue, Wed, Thu, Fri, Sat, Sun
}
```

The naming of constants in one particular enumeration follows the same principles of naming which we already explained in the "Naming Constants" section.

Note that each of the constants listed in the enumeration is of type this enumeration, i.e. in our case `Mon` belongs to type `Days`, as well as each of the other constants.

In other words, if we execute the following line:

```cs
Console.WriteLine(Days.Mon is Days);
```

This will be printed as a result:

```console
True
```

Let’s repeat again:

| :warning: | The enumerations are a set of constants of type – this listed type. |
|:--:|:--|

### Nature of Enumerations

Each constant, which is declared in one enumeration, is being associated with a certain integer. By default, for this hidden integer representation of constants in one enumeration `int` is being used.

To show **"the integer nature" of constants** in the listed types let’s try to figure out what’s the numerical representation of the constant, which corresponds to "Monday" from the example of the previous subsection:

```cs
int mondayValue = (int)Days.Mon;
Console.WriteLine(mondayValue);
```

After we execute it, the result will be:

```console
0
```

The values, associated with constants of a particular enumerated type by default are the indices in the list of constants of this type, i.e. numbers from 0 to the number of constants in the type less 1. In this way, if we consider the example with the enumeration type for the weekdays, used in the previous subsection, the constant `Mon` is associated with the numerical value 0, the constant `Tue` with the integer value 1, `Wed` – with 2, etc.

| :warning: | Each constant in one enumeration is actually a textual representation of an integer. By default, this number is the constant’s index in the list of constants of a particular enumeration type. |
|:--:|:--|

Despite the integer nature of constants in a particular enumeration, when we try to print a particular constant, its textual representation at the time of the constant’s declaration will be printed:

```cs
Console.WriteLine(Days.Mon);
```

After we execute the code above we will get the following result:

```console
Mon
```

### Hidden Numerical Value of Constants in Enumeration

As we can guess it is possible to change the **numerical value of constants in an enumeration.** This is done when we assign the values we prefer to each of the constants at the time of declaration.

```cs
[<modifiers>] enum <enum_name>
{
    constant1[=value1] [, constant2[=value2] [, ... ]]
}
```

Accordingly `value1`, `value2`, etc. must be integers.

To get a clearer idea of the given definition, consider the following example: let’s have a class `Coffee`, which represents a cup of coffee that customers order in a coffee shop:

| Coffee.cs |
|---|

```cs
public class Coffee
{
    public Coffee()
    {
    }
}
```

In this facility customers can order different amounts of coffee, as the coffee machine has predefined values "small" – 100 ml, "normal" – 150 ml, and "double" – 300 ml. Therefore, we can declare one enumeration `CoffeeSize`, which has respectively three constants – `Small`, `Normal` and `Double`, the correspondent qualities of which will be assigned:

| CoffeeSize.cs |
|---|

```cs
public enum CoffeeSize
{
    Small=100, Normal=150, Double=300
}
```

Now we can add a field and property to the class `Coffee`, which reflect the type of coffee the customer has ordered:

| Coffee.cs |
|---|

```cs
public class Coffee
{
    public CoffeeSize size;

    public Coffee(CoffeeSize size)
    {
        this.size = size;
    }

    public CoffeeSize Size
    {
        get { return size; }
    }
}
```

Let’s try to print the values of the coffee quantity for a normal and for one double coffee:

```cs
static void Main()
{
    Coffee normalCoffee = new Coffee(CoffeeSize.Normal);
    Coffee doubleCoffee = new Coffee(CoffeeSize.Double);

    Console.WriteLine("The {0} coffee is {1} ml.",
        normalCoffee.Size, (int)normalCoffee.Size);
    Console.WriteLine("The {0} coffee is {1} ml.",
        doubleCoffee.Size, (int)doubleCoffee.Size);
}
```

As we compile and execute this method, the following will be printed:

```console
The Normal coffee is 150 ml.
The Double coffee is 300 ml.
```

### Use of Enumerations

The main purpose of the enumerations is to **replace the numeric values,** which we would use if there were no enumeration types. In this way, the code becomes simpler and easier to read.

Another very important application of the enumerations is the pressure exercised by the compiler to use constants from the enumerations and not just numbers. Thus we minimize future errors in the code. For example, if we use an int variable instead of a variable from enumerations and a set of constants for the valid values, nothing prevents us from assigning the variable any value, e.g. -6723.

To make this clearer, consider the following example: create a class **"coffee price calculator",** which is calculating the price of each type of coffee, offered in the coffee shop:

| PriceCalculator.cs |
|---|

```cs
public class PriceCalculator
{
    public const int SmallCoffeeQuantity = 100;
    public const int NormalCoffeeQuantity = 150;
    public const int DoubleCoffeeQuantity = 300;

    public CashMachine() { }

    public double CalcPrice(int quantity)
    {
        switch (quantity)
        {
            case SmallCoffeeQuantity:
                return 0.20;
            case NormalCoffeeQuantity:
                return 0.30;
            case DoubleCoffeeQuantity:
                return 0.60;
            default:
                throw new InvalidOperationException(
                    "Unsupported coffee quantity: " + quantity);
        }
    }
}
```

We have three constants for the capacity of the coffee cups in the coffee shop, respectively 100, 150, and 300 ml. Furthermore, **we expect** that users of our class will diligently use the defined constants, instead of numbers – `SmallCoffeeQuantity`, `NormalCoffeeQuantity` and `DoubleCoffeeQuantity`. The method `CalcPrice(int)` returns the respective price, calculating it by the submitted amount.

The problem lies in the fact that someone may decide not to use the constants defined by us and may submit an invalid number as a parameter of our method, for example -1 or 101. In this case, if the method does not check for invalid quantity, it will likely return a wrong price, which is incorrect behavior.

To avoid this problem we will use one feature of these enumerations, namely constants in the enumeration type that can be used in `switch-case` structures. They can be submitted as values of the operator `switch` and accordingly – as operands of the operator `case`.

| :warning: | The constants of enumerations can be used in switch-case structures. |
|:--:|:--|

Let’s rework the method, which calculates the price for a cup of coffee, depending on the capacity of the cup. This time we will use the enumeration type `CoffeeSize`, which we declared in previous examples:

```cs
public double CalcPrice(CoffeeSize coffeeSize)
{
    switch (coffeeSize)
    {
        case CoffeeSize.Small:
            return 0.20;
        case CoffeeSize.Normal:
            return 0.40;
        case CoffeeSize.Double:
            return 0.60;
        default:
            throw new InvalidOperationException(
                "Unsupported coffee quantity: " + (int)coffeeSize);
    }
}
```

As we can see in this example, the possibility for the users of our method to provoke unexpected behavior of the method is negligible, because we force them to use specific values which to be used as arguments, namely constants of enumerated `CoffeeSize` type. This is one of the advantages of constants, which are declared in enumeration types to constants declared in any class.

| :warning: | Whenever possible, use enumerations instead of a set of constants declared in a class. |
|:--:|:--|

Before we finish with the enumeration section we should mention that the enumerations are to be used with caution when working with the `switch-case` construct. For example, if one day the owner of the coffee shop buys many big cups (mugs) for coffee, we will need to add a new constant in the constant list of the enumeration `CoffeeSize`, which may be called, for example, `Overwhelming`:

| CoffeeSize.cs |
|---|

```cs
public enum CoffeeSize
{
    Small=100, Normal=150, Double=300, Overwhelming=600
}
```

When we try to calculate the coffee price with the new quantity, the method, which calculates the price, will throw an exception, informing the user that such an amount of coffee is not available in the coffee shop.

What we should do to solve this problem is to add a new `case`-condition, which reflects the new constant in the enumerated `CoffeeSize` type.

| :warning: | When we modify the list of constants in an existing enumeration, we should be careful not to break the logic of the code that already exists and uses the constants, declared so far. |
|:--:|:--|

## Inner Classes (Nested Classes)

In C# an inner (nested) class is called a **class that is declared inside the body of another class.** Accordingly, the class that encloses the inner class is called an **outer class.**

The main reason to declare one class into another are:

1. To **better organize the code** when working with objects in the real world, among which have a special relationship and one cannot exist without the other.
2. To **hide a class in another class,** so that the inner class cannot be used outside the class wrapped it.

In general, inner classes are used rarely, because they complicate the structure of the code and increase the nested levels.

### Declaration of Inner Classes

The inner classes are declared in the same way as normal classes but are **located within another class.** Allowed modifiers in the declaration of the class are:

1. `public` – an inner class is accessible from any assembly.
2. `internal` – an inner class is available in the current assembly, in which is located the outer class.
3. `private` – access is restricted only to the class holding the inner class.
4. `static` – an inner class that contains only static members.

There are four more permitted modifiers – `abstract`, `protected`, `protected internal`, `sealed`, and `unsafe`, which are outside the scope and subject of this chapter and will not be considered here.

The keyword `this` to an inner class has relation only to the internal class, but not to the outside. Fields of the outside class **cannot be accessed** using the reference `this`. If necessary fields of the outer class can be accessed by the internal, it needs in creating the internal class to submit a reference to an outer class.

**Static members** (fields, methods, properties) of the outer class **are accessible from the inner class** regardless of their level of access.

#### Inner Classes – Example

Consider the following example:

| OuterClass.cs |
|---|

```cs
public class OuterClass
{
    private string name;

    private OuterClass(string name)
    {
        this.name = name;
    }

    private class NestedClass
    {
        private string name;
        private OuterClass parent;

        public NestedClass(OuterClass parent, string name)
        {
            this.parent = parent;
            this.name = name;
        }

        public void PrintNames()
        {
            Console.WriteLine("Nested name: " + this.name);
            Console.WriteLine("Outer name: " + this.parent.name);
        }
    }

    static void Main()
    {
        OuterClass outerClass = new OuterClass("outer");
        NestedClass nestedClass = new
            OuterClass.NestedClass(outerClass, "nested");
        nestedClass.PrintNames();
    }
}
```

In the example, the outer class `OuterClass` defines a member of the class `InnerClass`. Non-static inner class methods have access to their own body `this` as well as the instance of outside class `parent` (through syntax `this.parent`, if the `parent` reference is added by the developer). In the example, while creating the inner class, `parent` reference is set to the constructor of the outer class.

If we run the above example, we will obtain the following result:

```console
Nested name: nested
Outer name: outer
```

### Usage of Inner Classes

Consider an example. Let’s have a class for a car – `Car`. Each car has an engine and doors. Unlike the car’s door, however, the engine makes no sense regarded as being outside the car, because without it, the car cannot run, i.e. we have composition (see the section "Class Diagrams: Composition" in the chapter "Principles of Object-Oriented Programming").

| :warning: | When the connection between the two classes is a composition, the class, which consequently is a part of another class, is convenient to be declared as an inner class. |
|:--:|:--|

Therefore, if you declare the class for a car: `Car` would be appropriate to create an inner class `Engine`, which will reflect the appropriate concept for the car engine:

| Car.cs |
|---|

```cs
class Car
{
    Door FrontRightDoor;
    Door FrontLeftDoor;
    Door RearRightDoor;
    Door RearLeftDoor;
    Engine engine;

    public Car()
    {
        engine = new Engine();
        engine.horsePower = 2000;
    }

    public class Engine
    {
        public int horsePower;
    }
}
```

### Declare Enumeration in a Class

Before proceeding to the next section that refers to generic types, it should be noticed, that sometimes **enumeration should and can be declared within a class** in order of better encapsulation of the class.

For example, the enumeration of type `CoffeeSize`, we have created in the previous section, can be declared inside the body of the class `Coffee`, thereby it improves its encapsulation:

| Coffee.cs |
|---|

```cs
class Coffee
{
    // Enumeration declared inside a class
    public static enum CoffeeSize
    {
         Small = 100, Normal = 150, Double = 300
    }

    // Instance variable of enumerated type
    private CoffeeSize size;

    public Coffee(CoffeeSize size)
    {
        this.size = size;
    }

    public CoffeeSize Size
    {
        get { return size; }
    }
}
```

Respectively, the method for calculation of the price of coffee will be slightly modified:

```cs
public double CalcPrice(Coffee.CoffeeSize coffeeSize)
{
    switch (coffeeSize)
    {
        case Coffee.CoffeeSize.Small:
            return 0.20;
        case Coffee.CoffeeSize.Normal:
            return 0.40;
        case Coffee.CoffeeSize.Double:
            return 0.60;
        default:
            throw new InvalidOperationException(
                "Unsupported coffee quantity: " + ((int)coffeeSize));
    }
}
```

## Generics

In this section, we will explain the concept of **generic classes** (generic data types, generics). Before we begin, however, let’s look through an example that will help us understand more easily the idea.

#### Shelter for Homeless Animals – Example

Let’s assume that we have two classes. A class `Dog`, which describes a dog:

| Dog.cs |
|---|

```cs
public class Dog
{
}
```

And let a class `Cat`, which describes a cat:

| Cat.cs |
|---|

```cs
public class Cat
{
}
```

Then we want to create a class that describes a **shelter for homeless animals** – `AnimalShelter`. This class has a specific number of free cells, which determines the number of animals, which could find refuge in the shelter. The special feature of the class, that we want to create, is that it needs to accommodate animals of the same kind, in our case, dogs or cats only, because the coexistence of different species is not always a good idea.

If we think about how to solve the task with the knowledge that we have until here, we will come to the following conclusion – to ensure that our class will contain elements only from the same type we need to use an array of identical objects. These objects may be dogs, cats, or simply instances of the universal type `object`.

For instance, if we want to make a shelter for dogs, here is how our class would look like:

| AnimalsShelter.cs |
|---|

```cs
public class AnimalShelter
{
    private const int DefaultPlacesCount = 20;

    private Dog[] animalList;
    private int usedPlaces;

    public AnimalShelter() : this(DefaultPlacesCount)
    {
    }

    public AnimalShelter(int placesCount)
    {
        this.animalList = new Dog[placesCount];
        this.usedPlaces = 0;
    }

    public void Shelter(Dog newAnimal)
    {
        if (this.usedPlaces >= this.animalList.Length)
        {
            throw new InvalidOperationException("Shelter is full.");
        }
        this.animalList[this.usedPlaces] = newAnimal;
        this.usedPlaces++;
    }

    public Dog Release(int index)
    {
        if (index < 0 || index >= this.usedPlaces)
        {
            throw new ArgumentOutOfRangeException(
                "Invalid cell index: " + index);
        }
        Dog releasedAnimal = this.animalList[index];
        for (int i = index; i < this.usedPlaces - 1; i++)
        {
            this.animalList[i] = this.animalList[i + 1];
        }
        this.animalList[this.usedPlaces - 1] = null;
        this.usedPlaces--;

        return releasedAnimal;
    }
}
```

Shelter capacity (number of animals, which it is capable to accommodate) is set when the object is created. By default, it is the value of the constant `DefaultPlacesCount`. We use the field `usedPlaces` to monitor the occupied cells (at the same time we use it to index into the array for "pointing" to the first space from left to right in the array).

![](assets/animal-shelter-1.png)
 
We have created a method for adding a new dog into the shelter –
`Shelter()` and respectively for releasing from the shelter – `Release(int)`.

The method `Shelter()` adds each new animal in the first free cell on the right side of the array (if there is any free).

The method `Release(int)` accepts the number of the cell from which the dog will be released (i.e. the index number in the array, where it is stored a link to the object of type `Dog`).

![](assets/animal-shelter-2.png)
 
Then it moves all animals which are having a bigger cell number than the current cell, from which we will release a dog, with a position to the left (steps 2 and 3 are shown in the diagram below).

![](assets/animal-shelter-3.png)
 
The released cell at position `usedPlaces - 1` is marked as free, and a value `null` is assigned to it. This provides release of the reference to it and respectively allows the system to clean memory (garbage collector), to release the object if it is not used anywhere else in the program at this moment. This prevents indirect loss of memory (memory leak).

Finally, it assigns the number of the last free cell to a `usedPlaces` field (steps 4 and 5 of the scheme above).

![](assets/animal-shelter-4.png)
 
It is visible that the "removal" of an animal from a cell **could be a slow operation,** because it requires the transfer of all animals from the next cells with one position left. In the chapter "Linear Data Structures" we will discuss also more efficient ways of presenting the animal shelter, but for now, let’s focus on the topic of generic types.

So far we succeed implementing the functionality of the shelter – the class `AnimalShelter`. When we work with objects of type `Dog`, everything compiles and executes smoothly:

```cs
static void Main()
{
    AnimalShelter dogsShelter = new AnimalShelter(10);
    Dog dog1 = new Dog();
    Dog dog2 = new Dog();
    Dog dog3 = new Dog();

    dogsShelter.Shelter(dog1);
    dogsShelter.Shelter(dog2);
    dogsShelter.Shelter(dog3);

    dogsShelter.Release(1); // Releasing dog2
}
```

What happens, however, if we attempt to use an `AnimalShelter` class for objects of type `Cat`:

```cs
static void Main()
{
    AnimalShelter dogsShelter = new AnimalShelter(10);

    Cat cat1 = new Cat();

    dogsShelter.Shelter(cat1);
}
```

As expected, the compiler displays an error:

```console
The best overloaded method match for 'AnimalShelter.Shelter(
Dog)' has some invalid arguments. Argument 1: cannot convert from 'Cat' to 'Dog'
```

Consequently, if we want to create a shelter for cats, we will not be able to reuse the class that we already created, although the operations of adding and removing animals from the shelter will be identical. Therefore, we have to copy `AnimalShelter` class and change only the type of objects, which are handled – `Cat`.

Yes, but if we decide to make a shelter for other species? How many classes of shelters for the particular type of animals we shall create?

We can see that this solution of the problem **is not sufficiently comprehensive** and does not fully meets the terms, which we were set – to exist a **single class** that describes our shelter **for any kind of animal** (i.e. for all objects) and by working with it, **it should contain only one kind of animals** (i.e. only objects of the same type).

We could use instead of the type `Dog`, the universal type object, which can take values as `Dog`, `Cat` and all other data types, but this will create some inconvenience, associated with the need to convert back from the object to the `Dog`, when creating a shelter for dogs and it contains cells of type `object`, instead of type `Dog`.

To solve the task efficiently, we have to use a feature of the C# language that allows us to satisfy all required conditions simultaneously. It is called **generics** (template classes).

### What Is a Generic Class?

As we know if a method needs additional information to operate properly, this information is passed to the method using parameters. During the execution of the program, when calling this particular method, we pass arguments to the method, which are assigned to its parameters and then used in the method’s body.

Like the methods, when we know, that the functionality (actions) encapsulated into a class, can be applied not only to objects of one, but to many (heterogeneous) types, and these types are not known at the time of declaring the class, we can use a functionality of the language C# called **generics** (generic types).

It allows us to **declare parameters of this class, by indicating an unknown type** that the class will work eventually with. Then, when we instantiate our generic class, we replace the unknown with a particular. Accordingly, the newly created object will only work with objects of this type that we have assigned at its initialization. The specific type can be any data type that the compiler recognizes, including class, structure, enumeration, or another generic class.

To get a clearer picture of the nature of the generic types, let’s return to our task from the previous section. As you might guess, the class that describes the animal shelter (`AnimalShelter`) **can operate with different types of animals.** Consequently, if we want to create a general solution of the task, during the declaration of class `AnimalShelter`, we cannot know what type of animals will be sheltered to shelter. This is sufficient indication, that we can typify our class, adding to the declaration of the class as a parameter, the unknown type of animals.

Later, when we want to create a dog’s shelter, for example, this parameter of the class will pass the name of our type – class `Dog`. Accordingly, if you create a shelter for cats, we will pass the type `Cat`, etc.

| :warning: | Typifying a class (creating a generic class) means to add to the declaration of a class a parameter (replacement) of unknown type, which the class will use during its operation. Subsequently, when the class is instantiated, this parameter is replaced with the name of some specific type. |
|:--:|:--|

In the following sections, we will introduce the syntax of generic classes and we will modify our previous example to use generics.

### Declaration of Generic Class

Formally, the **parameterizing of a class** is done by adding `<T>` to the declaration of the class, after its name, where `T` is the substitute (parameter) of the type, which will be used later:

```cs
[<modifiers>] class <class_name><T>
{
}
```

It should be noticed that the characters '`<`' and '`>`', which surround the substitution `T` are an obligatory part of the syntax of language C# and must participate in the declaration of a generic class.

The **declaration of a generic class,** which describes a shelter for homeless animals, should look like as follows:

```cs
class AnimalShelter<T>
{
    // Class body here ...
}
```

Let’s can imagine that we are creating a **template of our class** `AnimalShelter`, which we will specify later, replacing `T` with a specific type, for instance, a `Dog`.

A particular class may have more than one substitute (to be parameterized by more than one type), depending on its needs:

```cs
[<modifiers>] class <class_name><T1 [, T2, [... [, Tn]]]>
{
}
```

If the class needs **several different unknown types,** these types should be listed by a comma between the characters '`<`' and '`>`' in the declaration of the class, as each of the substitutes used must be a different identifier (e.g. a different letter) – in the definition they are indicated as `T1`, `T2`, ..., `Tn`.

In case, we should create a shelter for animals of a mixed type, one that accommodates both – dogs and cats, we should declare the class as follows:

```cs
class AnimalShelter<T, U>
{
    // Class body here ...
}
```

If this were our case, we would use the first parameter `T`, to indicate objects of type `Dog`, which our class would operate with, and with `U` – to indicate objects of type `Cat`.

### Specifying Generic Classes

Before we present more details about generics, we should look at **how to use generic classes.** The using of generic classes should be done as follows:

```cs
<class_name><concrete_type> <variable_name> =
    new <class_name><concrete_type>();
```

Again, similar to `T` substitution in the declaration of our class, the characters '`<`' and '`>`' surrounding a particular class `concrete_type`, are required.

If we want to create two shelters, one for dogs and one for cats, we should use the following code:

```cs
AnimalShelter<Dog> dogsShelter = new AnimalShelter<Dog>();
AnimalShelter<Cat> catsShelter = new AnimalShelter<Cat>();
```

In this way, we ensure that the shelter `dogsShelter` will always contain objects of a type `Dog` and the variable `catsShelter` will always operate with objects of type `Cat`.

### Using Unknown Types by Declaring Fields

Once used during the class declaration, the parameters that are used to indicate the unknown types are visible in the whole body of the class, therefore they can be used to declare the field as each other type:

```cs
[<modifiers>] T <field_name>;
```

As we can guess, in our example with shelter for homeless animals, we can use this feature provided by language C#, to declare the type of field `animalsList`, which holds references to objects for the housed animals, instead of a specific type of `Dog`, with parameter `T`:

```cs
private T[] animalList;
```

Let’s assume when we create an object of our class, setting a specific type (e.g. Dog) during the execution of the program, **the unknown type `T` will be replaced** with the above type. If we choose to create a shelter for dogs, we can consider that our field is declared as follows:

```cs
private Dog[] animalList;
```

Accordingly, when we want to initialize a particular field in the constructor of our class, we should do it as usual – creating an array, using substitution of the unknown type – `T`:

```cs
public AnimalShelter(int placesNumber)
{
    animalList = new T[placesNumber]; // Initialization
    usedPlaces = 0;
}
```

### Using Unknown Types in a Method’s Declaration

As an **unknown type** used in the declaration of a generic class is visible from opening to closing brace of the class body, except for field’s declaration, it **can be used in a method declaration,** namely:

- As a parameter in the list of parameters of the method:

    ```cs
    <return_type> MethodWithParamsOfT(T param)
    ```

- As a result of implementation of the method:

    ```cs
    T MethodWithReturnTypeOfT(<params>)
    ```

As we already guessed, using our example, we can adapt the methods `Shelter(...)` and `Release(...)`, respectively:

- As a method of unknown type parameter `T`:

    ```cs
    public void Shelter(T newAnimal)
    {
        // Method's body goes here ...
    }
    ```
- And a method, which returns a result of unknown type `T`:

    ```cs
    public T Release(int i)
    {
        // Method's body goes here ...
    }
    ```

As we already know when we create an object from our class shelter and replace the unknown type with a specific one (e.g. `Cat`), during the execution of the program, the above methods will have the following form:

- The parameter of method `Shelter` will be of type `Cat`:

    ```cs
    public void Shelter(Cat newAnimal)
    {
        // Method's body goes here ...
    }
    ```
- The method `Release` will return a result of type `Cat`:

    ```cs
    public Cat Release(int i)
    {
        // Method's body goes here ...
    }
    ```

### Typifying (Generics) – Behind the Scenes

Before we continue, let’s explain what happens in the memory of the computer, when we work with generic classes.

![](assets/typifying-generics.png)
 
First, we declare our generic class `MyClass<T>` (generic class description in the scheme above). Then the compiler translates our code to an intermediate language (MSIL), as translated code contains information that the class is generic, i.e. it works with undefined types until now. At runtime, when someone tries to work with our generic class and tries to use it with a specific type, a **new description of the class** is created (specific type class description in the diagram above), which is identical to the generic class, with the difference that where it has been used `T`, now is replaced by a specific type. For example, if you try to use `MyClass<int>`, everywhere in your code, where the unknown parameter T is used, it will be replaced with `int`. Only then we can create an object of a generic class with a specific type `int`. The interesting thing here is that to create this object, the description of the class, which was created in the meantime (specific type class description), will be used. Instantiating a generic class by given specific types of its parameters is called **"specialization of the type"** or **"extension of generic class".**

Using our example, if we create an object of type `AnimalShelter<T>`, which works only with objects of type `Dog`, if we try to add an object of type `Cat`, this will cause a compile error almost identical to the errors, that were derived by an attempt to add an object of type `Cat`, into an object of type `AnimalShelter`, which we have created in section "Shelter for Homeless Animals – Example":

```cs
static void Main()
{
    AnimalShelter<Dog> dogsShelter = new AnimalShelter<Dog>(10);

    Cat cat1 = new Cat();

    dogsShelter.Shelter(cat1);
}
```

As expected, we get the following **compilation error messages:**

```console
The best overloaded method match for 'AnimalShelter< Dog>.Shelter(Dog)' has some invalid arguments

Argument 1: cannot convert from 'Cat' to 'Dog'
```

### Generic Methods

Like classes, when the type of method’s parameters cannot be specified, we can **parameterize (typify) the method.** Accordingly, the indication of a specific type will happen during the invocation of the method, replacing the unknown type with a specific one, as we did in the classes.

Typifying of a method is done, when after the name and before the opening bracket of the method, we add `<K>`, where `K` is the replacement of the type that will be used later:

```cs
<return_type> <methods_name><K>(<params>)
```

Accordingly, we can use unknown type `K` for parameters in the parameter’s list of method `<params>`, whose type is unknown, and also for the return value, or declare variables of type substitute `K` in the body of the method.

For example, consider a **method that swaps the values of two variables:**

```cs
public void Swap<K>(ref K a, ref K b)
{
    K oldA = a;
    a = b;
    b = oldA;
}
```

This is a method that swaps the values of two variables, **without caring about their types.** That is why we define it as a generic, so we can use it for all types of variables.

Accordingly, if we want to swap the values of two integers and then two string variables, we should use our method:

```cs
int num1 = 3;
int num2 = 5;
Console.WriteLine("Before swap: {0} {1}", num1, num2);
// Invoking the method with concrete type (int)
Swap<int>(ref num1, ref num2);
Console.WriteLine("After swap: {0} {1}\n", num1, num2);

string str1 = "Hello";
string str2 = "There";
Console.WriteLine("Before swap: {0} {1}!", str1, str2);
// Invoking the method with concrete type (string)
Swap<string>(ref str1, ref str2);
Console.WriteLine("After swap: {0} {1}!", str1, str2);
```

When you run this code, the result is as expected:

```console
Before swap: 3 5
After swap: 5 3

Before swap: Hello There!
After swap: There Hello!
```

We notice that in the list of parameters we have used also the keyword `ref`. This concerns the specification of the method – namely, to exchange the values of two references. By using the keyword `ref`, the method will use the same reference that was given by the calling method. This way, all changes on this variable made by our method, will remain after the method exits.

We should know that by **calling a generic method,** we can miss the explicit declaration of a specific type (in our example `<int>`), because the compiler will detect it automatically, recognizing the type of the given parameters. In other words, our code can be simplified using the following calls:

```cs
Swap(ref num1, ref num2); // Invoking the method Swap<int>
Swap(ref str1, ref str2); // Invoking the method Swap<string>
```

We should know that the **compiler will be able to recognize what is the specific type,** only if this type is involved in the parameter’s list. The compiler cannot recognize what is the specific type of a generic method only by the type of its return value or if it does not have parameters. In both cases, this specific type will have to be given explicitly. In our example, it will be similar to the original method call, or by adding `<int>` or `<string>`.

It should be noticed that static methods can also be typified, unlike the properties and constructors of the class.

| :warning: | Static methods can also be typified, but properties and constructors of the class cannot. |
|:--:|:--|

### Features by Declaration of Generic Methods in Generic Classes

As we have already seen in the section "Using Unknown Types in a Declaration of Methods", non-generic methods can use unknown types, described in the generic class declaration (e.g. methods `Shelter()` and `Release()` from the example "Shelter for Homeless Animals"):

| AnimalShelter.cs |
|---|

```cs
public class AnimalShelter<T>
{
    // ... The rest of the code ...

    public void Shelter(T newAnimal)
    {
        // Method body here
    }

    public T Release(int i)
    {
        // Method body here
    }
}
```

If we try to reuse the variable, which is used to mark the unknown type of the generic class, for example as `T`, in the declaration of a generic method, then when we try to compile the class, we will get a warning **CS0693.** This is happening because the scope of action of the unknown type `T`, defined in the declaration of the method, overlaps the scope of action of the unknown type `T`, in the class declaration:

| CommonOperations.cs |
|---|

```cs
public class CommonOperations<T>
{
    // CS0693
    public void Swap<T>(ref T a, ref T b)
    {
        T oldA = a;
        a = b;
        b = oldA;
    }
}
```

When you try to compile this class, you receive the following **message:**

```console
Type parameter 'T' has the same name as the type parameter from outer type 'CommonOperations<T>'
```

So if we want our code to be flexible, and our generic method safely to be called with a specific type, different from that in the generic class by instantiating it, we just have to declare the replacement of the unknown type in the declaration of the generic method **to be different than the parameter for the unknown type** in the class declaration, as shown below:

| CommonOperations.cs |
|---|

```cs
public class CommonOperations<T>
{
    // No warning
    public void Swap<K>(ref K a, ref K b)
    {
        K oldA = a;
        a = b;
        b = oldA;
    }
}
```

Thus, always make sure that there will be no overlapping of substitutes of the unknown types of method and class.

### Using a Keyword "default" in a Generic Source Code

Once we have introduced the basics of generic types, let’s try to **redesign our first example** in this section (Shelter for Homeless Animals). The only thing we need to do is to replace the type `Dog` with some parameter `T`:

| AnimalsShelter.cs |
|---|

```cs
public class AnimalShelter<T>
{
    private const int DefaultPlacesCount = 20;

    private T[] animalList;
    private int usedPlaces;

    public AnimalShelter() : this(DefaultPlacesCount)
    {
    }

    public AnimalShelter(int placesCount)
    {
        this.animalList = new T[placesCount];
        this.usedPlaces = 0;
    }

    public void Shelter(T newAnimal)
    {
        if (this.usedPlaces >= this.animalList.Length)
        {
            throw new InvalidOperationException("Shelter is full.");
        }
        this.animalList[this.usedPlaces] = newAnimal;
        this.usedPlaces++;
    }

    public T Release(int index)
    {
        if (index < 0 || index >= this.usedPlaces)
        {
            throw new ArgumentOutOfRangeException(
                "Invalid cell index: " + index);
        }
        T releasedAnimal = this.animalList[index];
        for (int i = index; i <this.usedPlaces - 1; i++)
        {
            this.animalList[i] = this.animalList[i + 1];
        }
        this.animalList[this.usedPlaces - 1] = null;
        this.usedPlaces--;

        return releasedAnimal;
    }
}
```

Everything looks to work properly until we try to compile the class. Then we **get the following error:**

```console
Cannot convert null to type parameter 'T' because it could be a non-nullable value type. Consider using 'default(T)' instead.
```

The error is inside the method `Release()` and it is related to recording a null value in the last released (rightmost) cell in the shelter. The problem is that we are trying to use the default value for a reference type, but **we are not sure whether this type is a reference type or a primitive.** Therefore the compiler displays the errors above. If the type `AnimalShelter` is instantiated by a structure and not by a class, then the null value is not valid.

To handle this problem, in our code we have to use the construct `default(T)` instead of `null`, which returns the default value for the particular type that will be used instead of `T`. As we know, the default value for reference type is `null`, and for numeric types – zero. We can make the following change:

```cs
// this.animalList[this.usedPlaces - 1] = null;
this.animalList[this.usedPlaces - 1] = default(T);
```

Finally, the compilation runs smoothly and the class `AnimalShelter<T>` operates correctly. We can test it as follows:

```cs
static void Main()
{
    AnimalShelter<Dog> shelter = new AnimalShelter<Dog>();
    shelter.Shelter(new Dog());
    shelter.Shelter(new Dog());
    shelter.Shelter(new Dog());
    Dog d = shelter.Release(1); // Release the second dog
    Console.WriteLine(d);
    d = shelter.Release(0); // Release the first dog
    Console.WriteLine(d);
    d = shelter.Release(0); // Release the third dog
    Console.WriteLine(d);
    d = shelter.Release(0); // Exception: invalid cell index
}
```

### Advantages and Disadvantages of Generics

Generic classes and methods **increase the reusability of the code,** the security and the performance compared to other non-generic alternatives.

As a general rule, the **programmer should strive to create and use generic classes, whenever it is possible.** The more generic types are used, the higher level of abstraction there is in the program and the source code becomes more flexible and reusable. However we should keep in mind, that overuse of generics can lead to over-generalization and the code may become unreadable and difficult to understand by other programmers.

### Naming the Parameters of the Generic Types

Before we finish generics as a topic, let’s give you some guidance on working with the substitutes (parameters) of unknown types in a generic class:

1. If there is just one unknown type in the generic, it is common to use the letter `T`, as a substitute for that unknown type. As an example, we can give our class declaration `AnimalShelter<T>`, which we used until now.
2. To the substitutes should be given the most descriptive names, unless a letter is not a sufficiently descriptive and well-chosen name, this will not improve the readability of the source code. For instance, we can modify our example, replacing the letter `T`, with the more descriptive substitute for `Animal`:

| AnimalShelter.cs |
|---|

```cs
public class AnimalShelter<Animal>
{
    // ... The rest of the code ...

    public void Shelter(Animal newAnimal)
    {
        // Method body here
    }

    public Animal Release(int i)
    {
        // Method body here
    }
}
```

When we use descriptive names of substitutes instead of a letter, it is better to add `T` at the beginning of the name, to distinguish it more easily from the class names in our application. In other words, instead of using a substitute `Animal` in the previous example, we should use `TAnimal` (`T` comes from the word "template" which means a parameterized / generic type).
