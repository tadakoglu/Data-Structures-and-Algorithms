<!-- section start -->
<!-- attr: { class:'slide-title', showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Sorting Algorithms
<div class="signature">
    <p class="signature-course">Data Structures and Algorithms</p>
    <p class="signature-initiative">Telerik Software Academy</p>
    <a href = "http://academy.telerik.com " class="signature-link">http://academy.telerik.com </a>
</div>


<!-- section start -->
<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Table of Contents
* Sorting
  * Sorting and classification
  * Review of the most popular sorting algorithms


<!-- section start -->
<!-- attr: { class:'slide-section', showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Sorting


<!-- attr: { showInPresentation:true, style:'' } -->
# What is a Sorting Algorithm?
* Sorting algorithm
  * An algorithm that puts elements of a list in a certain order (most common lexicographically)
* More formally:
  * The output is in some (non-decreasing) order
  * The output is a permutation of the input
* Efficient sorting is important for
  * Producing human-readable output
  * Canonicalizing data
  * Optimizing the use of other algorithms
* Sorting presents many important techniques

<!-- attr: { showInPresentation:true, style:'' } -->
# Classification
* Sorting algorithms are often classified by
  * Computational complexity
    * worst, average and best behavior
  * Memory usage
  * Recursive or non-recursive
  * Stability
  * Whether or not they are a comparison sort
  * General method
    * insertion, exchange (bubble sort and quicksort), selection (heapsort), merging, serial or parallel…

<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Stability of Sorting
* Stable sorting algorithms <!-- .element: style="width:70%" -->
  * Maintain the relative order of records with equal values
* If two items compare as equal, then their relative order will be preserved <!-- .element: style="width:70%" -->
  * When sorting only part of the data is examined when determining the sort order

<img class="slide-image" src="imgs/stability.png" style="width:25%; top:15%; right:0%" />


<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Selection sort


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'font-size:0.95em' } -->
# Selection sort
* Very simple and very inefficient algorithm
  * Best, worst and average case: `n`<sup>`2`</sup>
  * Memory: `1` (constant, only for the min element)
  * Stable: No
  * Method: Selection
  ```cs
  for (j = 0; j < n-1; j++) {
      // find the min element in the unsorted a[j .. n-1]
      iMin = j;
      for ( i = j+1; i < n; i++) {
          if (a[i] < a[iMin]) iMin = i;
      }
      if (iMin != j) swap(a[j], a[iMin]);
  }
  ```
  * http://en.wikipedia.org/wiki/Selection_sort


<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Bubble sort


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'font-size:0.8em' } -->
# Bubble sort
* Repeatedly stepping through the list, comparing each pair of adjacent items and swap them if they are in the wrong order
  * Best case: `n`, worst and average case: `n`<sup>`2`</sup>
  * Memory: `1`, Stable: Yes, Method: Exchanging
<img class="slide-image" src="imgs/bubble.png" style="position:initial; width:80%; margin:-10px 0;" />
  * http://en.wikipedia.org/wiki/Bubble_sort



<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Insertion sort


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'font-size:0.9em' } -->
# Insertion sort
* Builds the final sorted array one item at a time
  * Best case: `n`, worst and average case: `n`<sup>`2`</sup>
  * Memory: `1`, Stable: Yes, Method: Insertion

```cs
for i ← 1 to i ← length(A)-1
{
  valueToInsert ← A[i]
  holePos ← i
  while holePos > 0 and valueToInsert < A[holePos - 1]
  { 
    A[holePos] ← A[holePos - 1] // shift the larger value up
    holePos ← holePos - 1       // move the hole position down
  }
  A[holePos] ← valueToInsert
}
```
  * http://en.wikipedia.org/wiki/Insertion_sort



<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Quicksort


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'font-size:0.95em' } -->
# Quicksort
* First divides a large list into two smaller sub-lists then recursively sort the sub-lists
  * Best and average case: `n*log(n)`, worst: `n`<sup>`2`</sup>
  * Memory: `log(n)` stack space
  * Stable: Depends
  * Method: Partitioning
<img class="slide-image" src="imgs/quicksort.png" style="position:initial; width:80%; " />
  * http://en.wikipedia.org/wiki/Quicksort
<div class="fragments balloon" style="width:250px; top:57%; left:50%">Stable implementation</div>



<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Merge sort


<!-- attr: { showInPresentation:true, style:'font-size:0.9em' } -->
# Merge Sort
* Conceptually, a merge sort works as follows
  * Divide the unsorted list into `n` sublists, each containing `1` element (list of 1 element is sorted)
  * Repeatedly merge sublists to produce new sublists until there is only 1 sublist remaining
* Best, average and worst case: `n*log(n)`
* Memory: Depends; worst case is `n`
* Stable: Yes; Method: Merging
* Highly parallelizable (up to `O(log(n)`) using the Three Hungarian's Algorithm
* http://en.wikipedia.org/wiki/Merge_sort

<!-- attr: { showInPresentation:true, style:'font-size:0.9em' } -->
# Merge Sort Pseudocode

```cs
function merge_sort(list m)
    // if list size is 0 (empty) or 1, consider it sorted
    // (using less than or equal prevents infinite recursion
    // for a zero length m)
  if length(m) <= 1
      return m
    // else list size is > 1, so split the list into two sublists
  var list left, right
  var integer middle = length(m) / 2
  for each x in m before middle
       add x to left
  for each x in m after or equal middle
       add x to right
    // recursively call merge_sort() to further split each sublist
    // until sublist size is 1
  left = merge_sort(left)
  right = merge_sort(right)
    // merge the sublists returned from prior calls to merge_sort()
    // and return the resulting merged sublist
  return merge(left, right)
```

<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'' } -->
<!-- # Merge Sort Pseudocode -->

```cs
function merge(left, right)
    var list result
    while length(left) > 0 or length(right) > 0
        if length(left) > 0 and length(right) > 0
            if first(left) <= first(right)
                append first(left) to result
                left = rest(left)
            else
                append first(right) to result
                right = rest(right)
        else if length(left) > 0
            append first(left) to result
            left = rest(left)
        else if length(right) > 0
            append first(right) to result
            right = rest(right)
    end while
    return result
```

<img class="slide-image" src="imgs/mergesort.png" style="width:40%; top:45%; left:70%" />



<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Heap


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Heap
* Specialized tree-based data structure that satisfies the heap property:
  * Parent nodes are always greater (less) than or equal to the children
    * No implied orderingbetween siblings or cousins

<img class="slide-image" src="imgs/heap.png" style="position:initial; width:60%; margin:-10px 0;" />
* https://en.wikipedia.org/wiki/Heap_data_structure
<img class="slide-image" src="imgs/heap-tree.png" style="width:30%; top:52%; left:67%" />


<!-- attr: { showInPresentation:true, style:'' } -->
# Heapsort
* Can be divided into two parts
  * In the first step, a heap is built out of the data
  * A sorted array is created by repeatedly removing the largest element from the heap
* Best, average and worst case: `n*log(n)`
* Memory: Constant - `O(1)`
* Stable: No
* Method: Selection
* http://en.wikipedia.org/wiki/Heapsort


<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Counting sort


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Counting sort
* Algorithm for sorting a collection of objects according to keys that are small integers
* Not a comparison sort
* Average case: `n + r`
* Worst case: `n + r` 
  * `r` is the range of numbers to be sorted
* Stable: Yes
* Memory: `n + r`
* http://en.wikipedia.org/wiki/Counting_sort

<img class="slide-image" src="imgs/counting-sort.png" style="width:35%; top:27%; right:0%" />


<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Bucket sort


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'' } -->
# Bucket sort
* Partitioning an array into a number of buckets
  * Each bucket is then sorted individually
* Not a comparison sort
* Average case: `n + k`
  * `k` = the number of buckets
* Worst case: `n2 * k`
* Stable: Yes
* Memory: `n * k`
* http://en.wikipedia.org/wiki/Bucket_sort

<img class="slide-image" src="imgs/bucket-sort.png" style="width:40%; top:26%; right:0" />


<!-- section start -->
<!-- attr: { class:'slide-section' } -->
# Comparison of Sorting Algorithms


<!-- attr: { showInPresentation:true, hasScriptWrapper:true, style:'font-size:0.9em' } -->
# Comparison of Sorting Algorithms
* There are hundreds of sorting algorithms

<img class="slide-image" src="imgs/comparison.png" style="position:initial" />

<!-- section start -->
<!-- attr: { id:'questions', class:'slide-section', showInPresentation:true, style:'' } -->
# Questions
## Sorting and Searching Algorithms
[link to Telerik Academy Forum](http://telerikacademy.com/Forum/Category/15/data-structures-algorithms)