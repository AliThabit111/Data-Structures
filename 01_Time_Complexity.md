# Asymptotic Analysis & Big O Notation

## 📌 What is Big O Notation?
**Big O Notation** is a mathematical metric used to describe the limiting behavior of an algorithm. It measures how the **execution time** or **space requirements** scale as the input size ($n$) grows arbitrarily large.

---

## ⚡ Common Time Complexities (Fastest to Slowest)

| Notation | Name | Description / Example |
| :--- | :--- | :--- |
| **$O(1)$** | **Constant Time** | Execution time remains constant regardless of input size (e.g., accessing an array element by index). |
| **$O(\log n)$** | **Logarithmic Time** | The problem size is divided by a constant factor in each step (e.g., Binary Search on sorted data). |
| **$O(n)$** | **Linear Time** | Execution time grows proportionally with input size (e.g., a single loop traversing an array). |
| **$O(n \log n)$** | **Linearithmic Time** | Efficient divide-and-conquer sorting algorithms (e.g., Merge Sort, Quick Sort, Heap Sort). |
| **$O(n^2)$** | **Quadratic Time** | Performance is proportional to the square of input size (e.g., nested loops, Bubble Sort). |
| **$O(2^n)$** | **Exponential Time** | Growth doubles with each addition to input dataset (e.g., recursive calculation of Fibonacci numbers). |
| **$O(n!)$** | **Factorial Time** | Growth grows factorially (e.g., generating all permutations of a set). |

---

## 💡 Quick Rules of Thumb

* **Single Loop ($0 \to n$):** Usually **$O(n)$**
* **Nested Loops ($n \times n$):** Usually **$O(n^2)$**
* **Halving the Input Size (Divide & Conquer):** Usually **$O(\log n)$**
* **No Loops / Fixed Steps:** **$O(1)$**
