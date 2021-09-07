# Chapter 10 Exercises

1. Write a program to simulate n nested loops from 1 to n.
1. Write a program to generate all variations with duplicates of n elements class k. Sample input:
    n = 3  
    k = 2  
    Sample output:  
    (1 1), (1 2), (1 3), (2 1), (2 2), (2 3), (3 1), (3 2), (3 3)  
    - Think about and implement an iterative algorithm for the same task.
1. Write a program to generate and print all combinations with duplicates of k elements from a set with n elements. Sample input:
    n = 3  
    k = 2  
    Sample output:  
    (1 1), (1 2), (1 3), (2 2), (2 3), (3 3)
    - Think about and implement an iterative algorithm for the same task.
1. You are given a set of strings. Write a recursive program, which generates all subsets, consisting exactly k strings chosen among the elements of this set. Sample input:
    strings = {'test', 'rock', 'fun'}  
    k = 2  
    Sample output:  
    (test rock), (test fun), (rock fun)  
    - Think about and implement an iterative algorithm as well.
1. Write a recursive program, which prints all subsets of a given set of N words. Example input:
    words = {'test', 'rock', 'fun'}  
    Example output:  
    (), (test), (rock), (fun), (test rock), (test fun),  
    (rock fun), (test rock fun)  
    - Think about and implement an iterative algorithm for the same task.
1. Implement the merge-sort algorithm recursively. In it the initial array is divided into two equal in size parts, which are sorted (recursively via merge-sort) and after that the two sorted parts are merged in order to get the whole sorted array.
1. Write a recursive program, which generates and prints all permutations of the numbers 1, 2, …, n, for a given integer n. Example input:
    n = 3  
    Example output:  
    (1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)  
    - Try to find an iterative solution for generating permutations.
1. You are given an array of integers and a number N. Write a recursive program that finds all subsets of numbers in the array, which have a sum N. For example, if we have the array {2, 3, 1, -1} and N=4, we can obtain N=4 as a sum in the following two ways: 4=2+3-1; 4=3+1.
1. You are given an array of positive integers. Write a program that checks whether there is one or more numbers in the array (subset), whose sum is equal to S. Can you solve the task efficiently for large arrays?
1. You are given a matrix with passable and impassable cells. Write a recursive program that finds all paths between two cells in the matrix.
1. Implement the algorithm BFS (breadth-first search) for finding the shortest path in a labyrinth.
1. Modify the previous program to check whether a path exists between two cells without finding all possible paths. Test the program with a matrix 100x100 filled only with passable cells.
1. You are given a matrix with passable and impassable cells. Write a program that finds the largest area of neighboring passable cells.
1. Write a recursive program that traverses the whole hard disk C:\ recursively and prints all folders and files.
