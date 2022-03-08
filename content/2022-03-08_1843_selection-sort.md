# Selection Sort

A commonly used algorithm for [[sorting a list|2022-03-08_1816_sorting-a-list]].

> selection sort is an in-place comparison sorting algorithm. It has an O(n2) time complexity, which makes it inefficient on large lists, and generally performs worse than the similar insertion sort. Selection sort is noted for its simplicity and has performance advantages over more complicated algorithms in certain situations, particularly where auxiliary memory is limited.
>
> The algorithm divides the input list into two parts: a sorted sublist of items which is built up from left to right at the front (left) of the list and a sublist of the remaining unsorted items that occupy the rest of the list. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list. The algorithm proceeds by finding the smallest (or largest, depending on sorting order) element in the unsorted sublist, exchanging (swapping) it with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the right.
>
>The time efficiency of selection sort is quadratic, so there are a number of sorting techniques which have better time complexity than selection sort. One thing which distinguishes selection sort from other sorting algorithms is that it makes the minimum possible number of swaps, n − 1 in the worst case.

[From wiki](https://en.wikipedia.org/wiki/Selection_sort)

It's `O(n**2)` because the worst case is when all the elements are ordered in reverse. E.g. if you want to sort the list from smallest to maximum, worst is something like `[5,4,3,2,1]`. This is because algorithm must travel the length of the list for every iteration, and it must iterate the length of the list times.

Though because the sorted prefix is growing by 1 and the unsorted suffix is shrinking by 1 each time, it's `0.5(n**2)` but we ignore multiplicative constants in BigO analysis.

A good diagram of the algorithm:

![[2022-03-08_Selection-Sort-Animation.gif]]

[From wiki](https://en.wikipedia.org/wiki/Selection_sort#/media/File:Selection-Sort-Animation.gif)

In python

```python
def select_sort(L:list) -> list:
    for i in range(len(L) - 1):
        #Invariant: the list L[:i] is sorted
        minIndx = i
        minVal= L[i]
        j = i + 1
        while j < len(L):
            if minVal > L[j]:
                minIndx = j
                minVal= L[j]
            j += 1
        temp = L[i]
        L[i] = L[minIndx]
        L[minIndx] = temp
    return L
```

Code from [MIT Opencourseware](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-00sc-introduction-to-computer-science-and-programming-spring-2011/unit-1/lecture-9-memory-and-search-methods/)

#complexity
#algorithms
#list
#sort
