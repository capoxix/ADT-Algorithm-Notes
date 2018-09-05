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
    - Great to find min/max in constant time
    - Peek - find min/max which is always the first value (O(1))
    - Insert - insert into end and if it does not follow the rule, swap with parent until in correct place (log(n))
    - extract - get min/max and remove it (log(n))
    - addition should occur from left to right (should be a complete tree ()
    - min-heap (parent <= child) or max-heap (parent >=  child)