An algorithm is a mechanically-executable sequence of elementary instructions.

In my opinion, the clearest way to present an algorithm is using pseudocode. Pseudocode uses the structure of formal programming languages and mathematics to break algorithms into primitive steps; but the primitive steps themselves may be written using mathematics, pure English, or an appropriate mixture of the two. Well-written pseudocode reveals the internal structure of the algorithm but hides irrelevant implementation details, making the algorithm much easier to understand, analyze, debug, and implement.

Analyze algorithms
- Correctness: it is acceptable for programs to behave correctly most of the time, on all ‘reasonable’ inputs. Not in this class; we require algorithms that are correct for all *possible* inputs. Moreover, we must prove that our algorithms are correct; trusting our instincts, or trying a few test cases, isn’t good enough. Sometimes correctness is fairly obvious, especially for algorithms you’ve seen in earlier courses. On the other hand, ‘obvious’ is all too often a synonym for ‘wrong’. Correctness proofs almost always involve induction. We like induction. Induction is our *friend*. A problem is a task to perform, like “Compute the square root of x” or “Sort these n numbers” or “Keep n algorithms students awake for t minutes”. An algorithm is a set of instructions for accomplishing such a task.

- Running time: the common way of ranking different algos for the same problem is by how quickly they run. Ideally, we want the fastest possible algorithm for any particular problem. In many application settings, it is acceptable for programs to run efficiently most of the time, on all ‘reasonable’ inputs. Not in this class; we require algorithms that *always* run efficiently, even in the worst case.

## Algorithm Complexity in Songs & Apportionment

This text uses cumulative songs to illustrate **time complexity** ($\Theta$ and $O$ notation), showing how nested structures dictate performance.

---

### 1. Cumulative Songs (Quadratic & Exponential)

Most cumulative songs follow a nested loop structure where each new verse repeats all previous verses.

- **Quadratic Time $\Theta(n^2)$:**
    
    - **The 12 Days of Christmas:** Mentioning gifts follows the sum $\sum_{i=1}^{n} i$, resulting in $\frac{n(n+1)}{2}$ mentions.
        
    - **Total Gifts Given:** Follows a double summation $\sum_{i=1}^{n} \sum_{j=1}^{i} j$, resulting in $\frac{n(n+1)(n+2)}{6}$, which is **Cubic Time $\Theta(n^3)$**.
        
    - **Structure:** An outer loop runs $n$ times, and an inner loop runs $i$ times.
        
    - **Examples:** _Old MacDonald_, _Alouette_, _The Rattlin’ Bog_.
        
- **Exponential Time $O(2^n)$:**
    
    - **The TELNET Song:** Represents a modern example where the time to sing doubles (or grows exponentially) with each new parameter $n$.
        

---

### 2. Apportion Congress (Priority Queues)

The efficiency of the Congressional apportionment algorithm depends on the **Data Structure** used for the priority queue.

**General Bound:** $O(N + R(I + E))$

_(Where $N$=New, $I$=Insert, $E$=ExtractMax, $R$=Total Representatives, $n$=Number of States)_

|**Implementation**|**N**|**I**|**E**|**Total Complexity**|
|---|---|---|---|---|
|**Unsorted Array**|$\Theta(1)$|$\Theta(1)$|$\Theta(n)$|$O(Rn)$|
|**Binary Heap**|$\Theta(1)$|$O(\log n)$|$O(\log n)$|$O(R \log n)$|

**Key Takeaway:** Moving from an unsorted array to a binary heap improves performance from linear per representative to logarithmic per representative.

---

### Summary Table for Notes

| **Concept**                | **Example**              | **Complexity** |
| -------------------------- | ------------------------ | -------------- |
| **Nested Loops**           | "Old MacDonald"          | $\Theta(n^2)$  |
| **Double Summation**       | Total gifts in "12 Days" | $\Theta(n^3)$  |
| **Exponential Growth**     | "The TELNET Song"        | $O(2^n)$       |
| **Priority Queue (Array)** | US Census Bureau method  | $O(Rn)$        |
| **Priority Queue (Heap)**  | Optimized apportionment  | $O(R \log n)$  |

Sometimes we are also interested in other computational resources: space, randomness, page faults, inter-process messages, and so forth. We can use the same techniques to analyze those resources as we use to analyze running time.

This class is ultimately about learning two skills that are crucial for all computer scientists. 
1. *Intuition*: How to think about abstract computation. 
2. *Language*: How to talk about abstract computation.

Exercise
1.  Describe and analyze an efficient algorithm that determines, given a legal arrangement of
standard pieces on a standard chess board, which player will win at chess from the given
starting position if both players play perfectly. *Hint: There is a trivial one-line solution!*

Answer:
- **Algorithm:** Minimax search on the complete game tree.
    
- **Time Complexity:** $O(1)$ (for a fixed 8x8 board).
    
- **Space Complexity:** $O(1)$ (for a fixed 8x8 board).
    
- **Conclusion:** Theoretically solved, practically impossible for current hardware.

