# Chapter 16 Solutions and Guidelines

1. See the section "`List<T>`".
2. Use `Stack<int>`.
3. Keep the numbers in `List<T>` and finally use its `Sort()` method.
4. Use `List<int>`. Scan the list with a for-loop (1 ... n-1) while keeping two variables: **start** and **length.** Initially start=0, length=1. At each loop iteration if the number at the left is the same as the current number, increase length. Otherwise restart from the current cell (start=current, length=1). Remember the current start and length every time when the current length becomes better than the **current maximal length.** Finally create a new list and copy the found sequence to it.

    **Testing** could be done through a sequence of examples and comparisons, e.g. {1} -> {1}; {1, 2} -> {1}; {1, 1} -> {1, 1}; {1, 2, 2, 3} -> {2, 2}; {1, 2, 2} -> {2, 2}; {1, 1, 2} -> {1, 1}; {1, 2, 2, 1, 1, 1, 2, 2, 2, 3, 3, 3} -> {1, 1, 1}; {1, 2, 2, 1, 1, 1, 2, 2, 2, 2, 3, 3, 3} -> {2, 2, 2, 2}; ...

5. **Use list.** Perform a left-to-right scan through all elements. If the current number is positive, add it to the result, otherwise, skip it.
6. **Slow solution:** pass through the elements with a `for`-loop. For each element `p` count how many times `p` appears in the list (with a nested `for`-loop). If it is even number of times, append `p` to the result list (which is initially empty). Finally print the result list.

    **Fast solution:** use a **hash-table** (`Dictionary<int, int>`). With a single scan calculate `count[p]` (the number of occurrences of `p` in the input sequence) for each number `p` from the input sequence. With another single scan pass though all numbers `p` and append `p` to the result only when `count[p]` is even. Read about hash tables from the chapter "Dictionaries, Hash-Tables and Sets".

7. Make a **new array "occurrences" with size 1001.** After that scan through the list and for each number `p` increment the corresponding value of its occurrences (`occurrences[p]++`). Thus, at each index, where the value is not 0, we have an occurring number, so we print it.
8. **Use list.** **Sort the list** and you are going to get the equal numbers next to one another. Scan the array by counting the number of occurrences of each number. If up to a certain moment a number has occurred N/2+1 times, this is the **majorant** and there is no need to check further. If after position N/2+1 there is a new number (a majorant is not found until this moment), there is no need to search further – even in the case when the list is filled with the current number to the end, it will not occur N/2+1 times.

    **Another solution:** Use a **stack.** Scan through the elements. At each step if the element at the top of the stack is different from the next element form the input sequence, remove the element from the stack. Otherwise append the element to the stack. Finally the majorant will be in stack (if it exists). **Why?** Each time when we find any two different elements, we discard both of them. And this operation keeps the majorant the same and decreases the length of the sequence, right? If we repeat this as much times as possible, finally the stack will hold only elements with the same value – **the majorant.**

9. **Use queue.** In the beginning add N to the queue. After that take the current element M and add to the queue M+1, then 2*M + 1 and then M+2. Repeat the same for the next element in a loop. At each step in the loop print M and if at certain point the queue size reaches 50, break the loop and finish the calculation.
10. Use the data structure **queue.** Firstly, add to the queue N. Repeat the following in a loop until M is reached: remove a number X from the queue and add 3 new elements: X * 2, X + 2 and X + 1. Do not add numbers greater than M. As optimization of the solution, **try to avoid repeating numbers** in the queue.
11. Implement `DoubleLinkedListNode<T>` class, which has fields `Previous`, `Next` and `Value`. It will hold to hold a single list node. Implement also `DoubleLinkedList<T>` class to hold the whole list.
12. Use **singly linked list** (similar to the list from the previous task, but only with a field `Previous`, without a field `Next`).
13. Just modify your implementation of **doubly-linked list** to enable adding and removing from both its head and tail. **Another solution** is to use **circular buffer** (see http://en.wikipedia.org/wiki/Circular_buffer). When the buffer is full, create a new buffer of double size and move all existing elements to it.
14. **Use array.** When you reach the last index, you need to add the next element at the beginning of the array. For the correct calculation of the indices use the **remainder from the division with the array length.** When you need to resize the array, implement it the same way like we implemented the resizing in the "Static List" section. 
15. Use the simple **Bubble sort.** We start with the leftmost element by checking whether it is smaller than the next one. If it is not, we **swap their places.** Then we compare with the next element and so on and so forth, until we reach a larger element or the end of the array. We return to the start of the array and repeat the same procedure many times until we reach a moment, when we have taken sequentially all elements and no one had to be moved.
16. The **algorithm** is very easy: we start with an **empty queue,** in which we put the **root directory** (from which we start traversing). After that, until the queue is empty, we **remove the current directory** from the queue, print it on the console and **add all its subdirectories** to the queue. This way we are going to traverse the entire file system in breadth. If there are no cycles in the file system (as in Windows), the process will be finite.
17. If in the solution of the previous problem we **substitute the queue with a stack,** we are going to get **traversal in depth (DFS).**
18. Use **Breath-First Search (BFS)** by starting from the position, marked with "*". Each unvisited adjacent to the current cell we fill with the current number + 1. We assume that the value at "*" is 0. After the queue is empty, we traverse the whole matrix and if in some of the cells we have 0, we fill it with "u".