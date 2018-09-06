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


    