# ADT-Algorithm-Notes

## Set

- **MaxIntSet**
    - Integer Set that only includes integers value up to given maximum

- **IntSet**
    - Integer set that stores value inside buckets(array) by moding given number by the total number of buckets
- **ResizingIntSet**
    - Integer Set that resizes whenever that number of elements insize the integer set is greater than the number of buckets in it
    - Resizes usually by create a new array twiced it's size(num_buckets) and re-inserting all values into resized Integer set