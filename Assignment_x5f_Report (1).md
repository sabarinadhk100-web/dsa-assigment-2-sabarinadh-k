# DSA Assignment - Q10 Logistics Package Sorting
**Name: Sabari Nadh K**

### Question
A logistics company receives package weights: 20,15,20,10,15,20,25,10
Each package has unique package ID.

### Implementation Details
Packages defined as struct { id, weight }
- P1=20, P2=15, P3=20, P4=10, P5=15, P6=20, P7=25, P8=10

#### a) Merge Sort and Quick Sort with intermediate steps
**merge_sort.c** - prints each merge operation
**quick_sort.c** - prints each pivot and partition result

#### b) Modified Program for Stability
**quick_sort_stable.c** - Modified partition condition:
```c
if (arr[j].weight < pivot.weight || 
   (arr[j].weight == pivot.weight && arr[j].id < pivot.id))
```
This ensures same weight retains original relative order.
Verified using IDs:
- Weight 10: P4 before P8 in both original and sorted -> stable
- Weight 15: P2 before P5 -> stable
- Weight 20: P1, P3, P6 order retained in stable versions

#### c) Analysis

| Criteria | Merge Sort | Quick Sort (Standard) | Stable Quick Sort (Modified) |
|---|---|---|---|
| **Duplicate Values** | Handles well, merging keeps order | Partitions may swap equal values | Handles with ID tie-breaker |
| **Stability** | Stable by default (uses <=) | Unstable | Made Stable |
| **No. of Comparisons** | ~18-20 for 8 elements (always n log n) | ~15-22 avg, worst O(n^2) | Similar to Quick Sort + extra ID check |
| **Time Complexity** | O(n log n) best/avg/worst | O(n log n) avg, O(n^2) worst | O(n log n) avg |
| **Space Complexity** | O(n) auxiliary array | O(log n) stack, O(1) extra | O(log n) stack |
| **Suitable when equal-weight order important?** | YES - most suitable | NO - not suitable | YES - suitable after modification |

**Conclusion:** When maintaining original order of equal-weight packages is important (FIFO for same weight), Merge Sort is naturally suitable. Standard Quick Sort is not suitable because it is unstable. Modified Stable Quick Sort becomes suitable by using package ID as secondary key.

### How to Run
gcc merge_sort.c -o merge_sort && ./merge_sort > merge_sort_output.txt
gcc quick_sort.c -o quick_sort && ./quick_sort > quick_sort_output.txt
gcc quick_sort_stable.c -o stable && ./stable > quick_sort_stable_output.txt
