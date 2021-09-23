# Chapter 12 Solutions and Guidelines

1. Search in MSDN. The easiest way to do this is to search in Google for **"IOException MSDN"** (without the quotes).
2. Look at the instructions for the **previous task.**
3. Look at the instructions for the **previous task.**
4. Use the information from the **section "What Is an Exception?"** earlier in this chapter.
5. When having difficulties use the information from the **section "try-finally Construct".**
6. When having difficulties use the information from the **section "Exceptions Advantages".**
7. Create `try-catch-finally` statement.
8. When invalid number is used we can throw `Exception` because there is no other exception that can better describe the problem. As an alternative we can define our own exception class called in a way that better describes the problem, e.g. `InvalidNumberException`.
9. First read the chapter "Text Files". Read the file line by line with `System.IO.StreamReader` class and add the rows in `System.Text.StringBuilder`. Throw all exceptions from the method without catching them. You may cheat and solve the problem in one line of code by using the static method `System.IO.File.ReadAllText()`.
10. It is not too likely to write this method correctly without external help. Search in Internet to learn more about **binary streams.** After that follow the instructions below for reading a file:
    - For reading use `FileStream` and write the data in a `MemoryStream`. You have to read the file in parts, for example on portions with 64 KB each, the last one can be smaller.
    - Be careful with the method for reading the bytes `FileStream.Read(byte[] buffer, int offset, int count)`. This method can read less bytes than requested. You have to write as many bytes as you read from the input stream. Create a loop that ends when zero bytes are read.
    - Use `using` to correctly closing the streams.

    Saving an array of bytes in a file is a simpler task. Open `FileStream` and start writing the bytes inside from the `MemoryStream`. Use `using` to correctly close the streams.
    
    Use a **big ZIP archive** to test (for example 300 MB). If the program is not working correctly it will break the structure of the archive and an error will occur when trying to open it.

    You can cheat by using the system methods `System.IO.File.ReadAllBytes()` and `System.IO.File.WriteAllBytes(byte[])`.

11. Inherit from `Exception` class and add a constructor to it. For example `FileParseException(string message, string filename, int line)`. Use this exception the same way as using any other exception. The number can be read with `StreamReader` class.
12. Search for all possible exceptions that the method could throw and for all of them define a `catch` block and print user-friendly message.
13. Search for articles in Internet for **"downloading a file with C#"** or search for information and examples about using the `WebClient` class. Make sure you catch and process all **exceptions** that can be thrown.