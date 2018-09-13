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
        - greater than left subtree (pick biggest from left-subtree)
            - go left-side, right-most node
                - if right-most node has a left-child, this node replaces it as child of right-most node's parent
        - smaller than right subtree (pick biggest from left-subtree)
- **balanced binary search tree**
    - difference in depth for left and right sub-tree is at most 1
    - both left and right sub-tree are balanced

- **Graphs**
    - vertices (dots)
    - edges(lines)
        - need to have directions that are consistent
        - if have weighted, all of them have to be weighted
   - |V| = # vertices
   - |E| = # edges
   - Density = |E|/ |V| * (|V| - 1)
   - Max of Density = 1, min of density = 0

    ```ruby
        class Graph
            def initialize
                @vertices = []
                @edges = []
            end

        class Vertex
            def initialize(data)
                @data = data
            end
        end
        
        class Edge
            def initialize(A,B)
                @vertices = [A,B]
                @weight = 1
            end
        end
    ```

- **Graph (Trees)**
    - n vertices
    - n-1 edges (not cyclic)
    - tree are often sparse graph where density ~ 1/n
    - Vertex should have access to edges
    - Graph class sould have access to edges

- **Topological Sort**
    -  Use Cases
        - task/dependencies
        - webpack
        - scheduling
        - scheduling restriction
        - minimal spanning tree

    - Kahn's Algorithm
        - queue up all vertices with no in edges
        - pop off vertices from queue
            -remove vertex and edges from graph
            - push vertex into sorted array
            - examine destination vertices, push onto queue if no more in edges
        - pick vertice whichs has no in edges and put on list.
        - delete all of it's out edges
        - pick vertices with no in edges
    ```ruby
     def top_sort(graph) #O(|V| + |E|)
         sorted = []
         top = new Queue()
         # O(|v|)
         graph.vertices.each do |vertex|
             if vertex.in_edges.empty?
                top.enqueue(vertex)
             end
         end

         # O(|E|)
         until top.empty?
             current = top.pop
             sorted << current
             current.out_edgges.each do |edge|
                 graph.delete_edge(edge)
                 if edge.destination.in_edges.empty?
                     top.enqueue(edge.destination)
                 end
             end
         end
         sorted
     end
    ```
    - Tarjan's Algorithm
        - loop through each node and terminate when it hits any node that has been visited
        - each N node gets prepended into an output list L
            -guaranteeing that all nodes that are dependent on it are already in L
                -added either by recursive call visit which ended before the call to visit N or by a call to visit
                which started even before the call to visit N

    - Other Graph Algorithms
        - Coffman-Graham 
        - Modifying DFS

- **Dynamic Programming**
    - improving performance by using methods that resuse work that you've already done
    - top-down
        - memoization
        - typical of recursive implementations
        - build your stacks and save the work to a cache as you bubble up
    - bottom-up
        - use smaller solutions as the basis of the larger solution
        - typical of iterative implementation
        - can use cachce as well without incurring additional stacks
    - Fibonnacci example
        ```ruby
        #O(2^n)
        def fibonacci(n)
            return 1 if n == 1 || n == 2
            return fibonacci(n - 1) + fibonacci(n - 2)
        end

        #top-down
        #O(n)
        class Fibonacci
            def initialize
                @cache = {1 => 1, 2 => 1}
            end

            def fibonacci(n)
                return @cache[n] if @cache[n]
                ans = fibonacci( n - 1) + fibonacci(n - 2)
                @cache[n] = ans
                ans
            end
        end
        ```
    - Burgar Problem
        - rob houses that are not adjacent to each other
        - keep track of sub-solutions
        - each decision relies on relationships with sub-solutions 
    

## Distributed Systems
- most of the times we do read to DB
    - RAM (10,000x quicker thhan reading from disk) is very useful to speed up process
- database biggest factor in speed performance
- Vertical Scaling
    - reduce N + 1 Query
    - increase RAM
    - reduce inefficiency in code
- Application Server Horizontal Scaling
    - use load banner (NGINX) - receives request processes it and then send to one of the application server
- Leader/Follower Database Horizontal Scaling
- User can read from any of the databases (leader/ follower)
- Writes come into leader
    - Leader forward the writes to followers
    -Two ways
        - synchronous replication
            - leader lets application know when all the databases(follower/leader) have been updated
            - immeadiately send updates to followers
        - asynchronous replication
            -app server does not need to wait as long to know whether leader has been updated
            - it could try to read from follower information that does not exist
- Conflicts of having more than one leader
    - bank transfer (databases have different states(not up to date))
    - solve conflict through 
        - locking(blocking other databases from been written to)
        - reconciling strategies ("last writer wins")
- Partitioning Database (separate databases into small parts)
    - usually have followers behind each separate paritition (take care of failing)
    - denormalize state
        ```SQL
        Users
            id
            fname
            lname
            grav_url 
        
        Friends
            friend_id1 = 101
            friend2_fname = 'Markov'
            friend2_lname = 'Puggeri'
            friend2_grav_url = 'markov.com'
        ```
    -tradeoffs
        - normalized state
            -write faster, read slower
        - denormalized state
            -read faster, write slower
            - takes more memory (many copies in different parts)

## Financial Literacy
- Income and Benefits
    - Vesting
        - get part of shares after certain amount of time
    - 401(k) match
        - retirement account
        - lowers taxable income now
        - lower tax rate when withdrawn
        - free money (from company)
        - always move your 401k to new bank
    - stock options (understand that private you may not get money back)
        - options have expitation date usually
        -get an accountant messy
        - calculate value of stocks
            - shares, fully diluted shares outstanding, strike price, vesting schedule
    - Employee Stock Purchase Plan (Free money)
        - discount for stock
- Healthcare
    - PPO
        - you choose your doctor
    - HMO
        - public
    - HDHP (cheaper, pay out of pocket)
- Reduce Tax
    - 401k
    - IRA
    - HSA
- Budgeting
    - align spending with values
    - quantifiable self
    - peace of mind
    - pay off debt
    - Tools:
        - Mint
        - Personal Capital (investment)
- Investing
    - Open an acoount on vanguard (brokage firm)
    - Invest in Target Funds
    - Individual stocks ( <5% investing budget)




