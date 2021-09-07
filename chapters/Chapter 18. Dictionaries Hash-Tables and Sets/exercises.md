# Chapter 18 Exercises

1. Write a program that counts, in a given array of integers, the number of occurrences of each integer.
    - Example: array = {3, 4, 4, 2, 3, 3, 4, 3, 2}  
      2 ? 2 times		3 ? 4 times		4 ? 3 times
1. Write a program to remove from a sequence all the integers, which appear odd number of times. For instance, for the sequence {4, 2, 2, 5, 2, 3, 2, 3, 1, 5, 2, 6, 6, 6} the output would be {5, 3, 3, 5}.
1. Write a program that counts how many times each word from a given text file words.txt appears in it. The result words should be ordered by their number of occurrences in the text.
    - Example: "This is the TEXT. Text, text, text – THIS TEXT! Is this the text?"
    - Result: is ? 2, the ? 2, this ? 3, text ? 6.
1. Implement a DictHashSet<T> class, based on HashDictionary<K, V> class, we discussed in the text above.
1. Implement a hash-table, maintaining triples (key1, key2, value) and allowing quick search by the pair of keys and adding of triples.
1. Implement a hash-table, allowing the maintenance of more than one value for a specific key.
1. Implement a hash-table, using "cuckoo hashing" with 3 hash-functions.
1. Implement the data structure hash-table in a class HashTable<K,T>. Keep the data in an array of key-value pairs (KeyValuePair<K,T>[]) with initial capacity of 16. Resole the collisions with quadratic probing. When the hash table load runs over 75%, perform resizing to 2 times larger capacity. Implement the following methods and properties: Add(key, value), Find(key) ? value, Remove(key), Count, Clear(), this[] and Keys. Try to make the hash-table to support iterating over its elements with foreach.
1. Implement the data structure "Set" in a class HashedSet<T>, using your class HashTable<K, T> to hold the elements. Implement all standard set operations like Add(T), Find(T), Remove(T), Count, Clear(), union and intersect.
1. We are given three sequences of numbers, defined by the formulas:
    - f1(0) = 1; f1(k) = 2*f1(k-1) + 3; f1 = {1, 5, 13, 29, …}
    - f2(0) = 2; f2(k) = 3*f2(k-1) + 1; f2 = {2, 7, 22, 67, …}
    - f3(0) = 2; f3(k) = 2*f3(k-1) - 1; f3 = {2, 3, 5, 9, …}
    1. Write a program to find the intersection and union of sets of sequences’ elements within the range [0; 100000]: f1 * f2; f1 * f3; f2 * f3; f1 * f2 * f3; f1 + f2; f1 + f3; f2 + f3; f1 + f2 + f3. Here + and * mean respectively union and intersection of sets.
1. * Define TreeMultiSet<T> class, which allows to keep a set of elements, in increasing order and to have duplicates of the elements. Implement operations adding of element, finding the number of occurrences, deletion, iterator, min / max element finding, min / max deletion. Implement the possibility to pass an external Comparer<T> for elements comparison.
1. * We are given a list of arriving and departing schedule at a bus station. Write a program, using the HashSet<T> class, which by given interval (start, end) returns the number of buses, which have arrived and departed during that time. Example:
    - We have the data of the following buses: [08:24-08:33], [08:20-09:00], [08:32-08:37], [09:00-09:15]. We are given the range [08:22-09:05]. The number of buses, arriving and departing during that time is 2.
1. * We are given a sequence P containing L integers L (1 < L < 50,000) and a number N. We call a "lucky sub-sequence within P" every sub-sequence of integers from P with a sum equal to N.
Imagine we have a sequence S, holding all the lucky sub-sequences of P, kept in decreasing order by their length. When the length is the same, the sequences are ordered in decreasing order by their elements: from the leftmost to the rightmost. Write a program to return the first 10 elements of S.
Example: We are given N = 5 and the sequence P = {1, 1, 2, 1, -1, 2, 3, -1, 1, 2, 3, 5, 1, -1, 2, 3}. The sequence S consists of the following 13 sub-sequences of P:
    1. [1, -1, 2, 3, -1, 1]
    1. [1, 2, 1, -1, 2]
    1. [3, -1, 1, 2]
    1. [2, 3, -1, 1]
    1. [1, 1, 2, 1]
    1. [1, -1, 2, 3]
    1. [1, -1, 2, 3]
    1. [-1, 1, 2, 3]
    1. [5, 1, -1]
    1. [2, 3]
    1. [2, 3]
    1. [2, 3]
    1. [5]
    - The last 10 elements of P are given in bold.