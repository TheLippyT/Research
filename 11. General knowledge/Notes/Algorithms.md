#### Algorithm
- An algorithm is a set of steps or instructions to complete a task
- Has a clearly defined problem statement, input, and output
- The steps need to be in a specific order
- The steps need to be distinct
- The algorithm shold produce a result
- The algorithm needs to complete in a finite amount of time
- The agorithm is deemed correct if on every run of the algorithm with an input yields a the right output
- The algorithm is deemed efficient 

When you determine the efficiency of an algorithm always evaluated it at its worst case scenario

#### Big O
Big O is a theoretical definition of the complexity of an algorithm as a function of the size

O => Order of magnitude of complexity

compexity is relative. Big O is used to measure the time and space complexity between algorithms that solve the same problem. for example a binary search algorithm won't be benchmarked against a sorting algorithm but instead with other searching algorithms.

Big O => the function of the size

#### Common complexities

these are common complexities and it plotted in a graph that measures runtime per operations over N:

- O(1) = constant time => the runtime is the same in any given case regardless of the amount of inputs
- O(log n)/O(ln n) = logarithmic runtime => when N grows really large

algorithms with algorithmic runtimes are called sublinear. sublinear runtime algorithms are more
prefered that linear runtimes because they are efficient.

linear runtimes do come with their own set of advantages.

- O(n) = linear runtime => the number of opertations is the same as N.

any algorithm that has sequential input has a linear runtime.
why would we use linear search?
in comparison to binary search, a linear search does not have to be sorted. a binary search however requires the 
list of objects to be sorted to efficiently work.

- O(n^2) = Quadratic runtime => an opertation raised to the second power. for any given value of N, we carry out N^2 amount of operations
- O(n^3) = Quebic runtime => for any given value of N, we carry out N^3 amount of operations. not common as quadratic runtimes
- O(n log n) = Quasilinear runtime => for every value of N we are gonna excute a log N numnber of operations. runs between linear and logarithmic runtime.

all runtimes we have witnessed until now are called polynomial runtimes. a algorithm is considered a polynomial runtime if its worst case can be calculates with
- O(n^k) where k can be any value. example k = 2, k = 3. polynomial runtime algorithms are considered efficient and the are likely to be used in practice

exponential runtimes are runtimes that are not considered efficient.
- O(X^n) = exponential runtime => examples algorithms of exponential runtimes are bruteforce algorithms. very expensive algorithms.

##### Big O cheatsheet
- the big O cheatsheet can be found at this website => https://www.bigocheatsheet.com/

![[common big o complexity chart.png]]
![[common data structure operations.png]]
![[array sorting algorithms.png]]


