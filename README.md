# ADT-Algorithm-Notes

## Set

- **MaxIntSet**
    - Integer Set that only includes integers value up to given maximum

- **IntSet**
    - Integer set that stores value inside buckets(array) by moding given number by the total number of buckets
- **ResizingIntSet**
    - Integer Set that resizes whenever that number of elements insize the integer set is greater than the number of buckets in it
    - Resizes usually by create a new array twiced it's size(num_buckets) and re-inserting all values into resized Integer set


## Priority Queues
- **Binary Heap**
    - Great for finding min/max in constant time
    - Peek - find min/max which is always the first value (O(1))
    - Insert - insert into end and if it does not follow the rule, swap with parent until in correct place (log(n)) [heapify]
    - extract - get min/max and remove it (log(n))
        - swap min/max with bottom-most right
        - remove bottom-most right
        - heapify (swap until heap follows rule) 
        - at most (depth-level) swaps occur 
    - addition should occur from left to right (should be a complete tree ()
    - min-heap (parent <= child) or max-heap (parent >=  child)
    - In an array, children = 2i + 1 / 2i+ 2 and parent = (i - 1)/2 [Ensure value received is an integer]
- **Heap Sort**
    - normal without in-place, you push all values into a heap sort and then extract it all
        - push basically creates a heapified array (everytime you push into heap arr you heapify_up)
        - extract (which takes out highest value and heapifies down) values from heapified array and insert into an array normally
    - in place array sort (using boundary for length)
        - heapify up moving following given rule)
        - heapify_up each value from left to right (have a length boundary (i + 1) [right most])
        - after heapified_up, "extract" and heapify_dowmn
            - "extract" - swap first and last values
            - heapify down with right-most boundary going from right to left (make length limit smaller to avoid swapping already swapped ("extracted) values)

## Quicksort
-   **quicksort(not in place)**
    - base case: return array if less than or equal to 1
    - choose pivot point
    - partition array around pivot
        - left everything  smaller than or equal to pivot point
        - right everything bigger than pivot point
    - recurse on left and right (Repeating step 1 and 2)
- **quicksort(in place)**
    -recursive call takes (log(n)?) -space complexity
    - base case: return array if length less than or equal to 1
    - choose pivot point
        -random pick a pivot point
        -swap first value with randomly chosen pivot point
    - partition array around pivot (by swapping elements inside the array)
        - separate arrays left side has everything <= pivot
        - right side everything > pivot
        - everytime you find value <= pivot
            - swap value after boundary index with it
            - add 1 to boundary index
        - swap pivot value with boundary index
    - recurse on left and right with start and end index
        - left side - start index to boundary index
        - right-side - boundary index + 1 to end

## Time Complexities

|function | **Array**       | **Sorted**          | **Min Heap** | **BST**|
| ------------- | ------------- |:-------------:| -----:|-----:|
| `find` |  O(n)  | O(log(n) [BS]| O(n) | O(log n)|
|`insert` | O(1)    | O(n)     |  O(log n) | O(log n)|
|`delete` | O(n) | O(n)     |    O(log n)| O(log n)

## Binary Search Tree
- **rules**
    - all left nodes < root
    - all right nodes > root
- **find (recursively check) -time is dependent on # of depth in tree**
    - if val != node
        - if val < node check left-child
            - return false if no left-child
        - if val > node check right-child
            - return false if no right-child
- **insert**
    - if val > node, go to right-side and check
        - if right-side is empty, insert into it
        - if not, compare with node and decide side to keep going left/right through comparison
    - if val < node, go to left-side
        - if left-side is empty, insert into it
        - if not, compare with ndoe and decide side to keep going left/right through comparison
- **delete [Hibbard deleteion]**
    - if on left-side and not a leaf
        - replace with node < parent
        - greater than left subtree
        - smaller than right subtree 
    - if on right-side and not a leaf
        - replace with node > parent
        - greater than left subtree (pick biggest on left-subtree)
            - go left-side, right-most node
                - if right-most node has a left-child, this node replaces it as child of right-most node's parent
        - smaller than right subtree (pick from left-subtree)
- **balanced binary tree**
    - difference in depth for left and right sub-tree is at most 1
    - both left and right sub-tree are balanced
