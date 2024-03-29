# Chapter 18 Solutions and Guidelines

1. Use `Dictionary<TKey, TValue>` counts and though a single scan through the input numbers count the occurrences of each one. When you pass through a number `p`, if it is missing in the dictionary `counts[p] = 1`. If the number is already stored in the dictionary, increase its count: `counts[p] = counts[p] + 1`. Finally scan through the element of the dictionary (with `foreach`-loop) and **print its key-value pairs.**
2. Use `Dictionary<K, T>` to count how many times each element occurs (like in the previous problem) and `List<T>` where you can add all elements occurring even number of times.
3. Use `Dictionary<string, int>` with word as a key and number of occurrences as a value. After **counting all the words, sort the dictionary by value** using something like this:
    
    ```cs
    var sorted = dictionary.OrderBy(p => p.Value);
    ```
    
    To use the `OrderBy(<keySelector>)` extension method you need to include the `System.Linq` namespace.

4. Use the element of the set as **key and value at the same time.**
5. Use **hash-table of hash-tables:** `Dictionary<key, Dictionary<key, value>>`. Think about how to add and search elements in this structure.
6. Use `Dictionary<K, List<V>>`.
7. You can use `GetHashCode() % size` as the first hash-function, `(GetHashCode() * 83 + 7) % size` as the second, `(GetHashCode () * GetHashCode() + 19) % size)` as the third.
8. **Follow the example from the section "Implementation of a Dictionary with Hash-Table and Chaining".** Read about quadratic probing in Wikipedia: http://en.wikipedia.org/wiki/Quadratic_probing. In order to expand the hash table (double its size), you can allocate an array with double size, transfer all the elements from the old one to the new one and at the end redirect the reference from the old array to the new one. To have `foreach` on your collection, implement the interface `IEnumerable` and inside your `GetEnumerator()` method you must return `GetEnumerator()` to the array of lists. You can use `yield` operator.
9. One way to solve the task is to use as key for the hash-table the element of the set and **as a value always `true`.** The union and intersection will be done by looping all the elements of the first set and checking if there is (respectively there is not) element of the second one.
10. Find all the members of the three sequences inside the given range and using `HashSet<int>` implement union and intersection of sets after that. At the end do the calculations requested.
11. `TreeMultiSet<T>` class you can implement by using the .NET system class `SortedDictionary<K, List<T>>`. It is not so easy, so take enough time to write the code and test it.
12. The obvious solution is to check for all the buses whether they arrive or depart in the given range. But according to the task terms we have to use `HashSet<T>`. Let’s think how.
    
    With a linear scan (a `for`-loop) we can find **all buses arriving after the beginning** of the range and find **all buses departing before the end** of the range. These are **two separate sets,** right? The intersection of these sets should give us the set of buses we need.
    
    If `TimeInterval` is a class, keeping the schedule of a bus (`arriveHour`, `arriveMinute`, `departureHour`, `departureMinute`), the intersection could be efficiently found by `HashSet<TimeInterval>` with correctly defined `GetHashCode()` and `Equals()`.
    
    Another, **efficient solution** is to use `SortedSet<T>` and its method `GetViewBetween(<start>, <end>)`, but this contradicts to the problem description (recall that we are assigned to use `HashSet<T>`).

13. The first idea for a solution is simple: Using **two nested loops we find all lucky sub-sequences** of the sequence `P`. After that we **sort them** by their length (and by their elements as second criteria) and at the end we print the first 10. However, this algorithm will not work well if we have millions of sub-sequences. It may cause **"out of memory".**
    
    We would describe an idea for a **much efficient solution:** we will first define a class `Sequence<T>` to hold a sequence of elements. We will implement `IComparable<Sequence<T>>` to compare sequences by length in decreasing order (and by elements in decreasing order when the length is the same).
    
    Later we will use our `TreeMultiSet<T>` class. Inside we will **keep the first 10 sub-sequences of S,** i.e. multi-set of the lucky sub-sequences of P, kept in decreasing order by length (and in decreasing order of their content when the length is the same). When we have 10 sub-sequences inside the multi-set and we add 11th sequence, it would **take its correct place** in the order, because of the `IComparable<Sequence<T>>` defined. After that we can delete the 11th subsequence, because it is not amongst the first 10. In that way we would **always keep the first 10 elements,** discarding the others in any given moment, consuming **much less memory** and with no need of sorting at the end. The implementation is not so easy, so spare enough time for it.
