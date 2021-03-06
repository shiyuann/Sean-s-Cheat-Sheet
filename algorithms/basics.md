<extoc></extoc>

# Algorithm Basics

## 问题分析思路

- 使用**循环**拆成重复的子问题 - `loop`
- 使用**分类讨论**拆分多种情况/分支 - `if-else`
- 使用**分治法(divide and conquer)**拆成**可继续拆分的子问题**直到**最小情况(base case)** - `recursion / iteration`

## Time & Space Complexity Analysis

### 分析方法

- **展开recursion tree进行分析**
    - **分析每个节点花的时间、空间。**
    - **分析每层花的总时间、空间。**
- **注意分析Worst Case**
- 分析空间时，注意**分析Call Stack占用的最大内存大小**
- 针对Tree问题
    - 不要针对树本身分析，要画出recursion tree
    - Eg. isIdentical 四叉树 in Class 03/24
- Amortized Time Complexity - 平均用时分析方法
    - 一次大量耗时的Action为之后很多次Action节省时间。
    - 注意：Amortized time仍然可能有worst case， Amortized分析只针对不适合对算法的单次操作进行分析。

## 常见的优化方向

- Space
    - **in-place** - 利用input的空间，减少额外空间的使用
- Time
    - **Dynamic Programming** 
        - 记录子问题的Solution，方便解决相同子问题时利用
    - 减少内存分配释放次数。
        - Java的堆内存垃圾回收机制，回收内存需要时间开销。所以过多创建局部变量是开销更大的。
        - 减少局部堆内存分配，比如在merge sort中，可以只在初始化时创建一次临时变量，减少开销。
- 代码可读性    
    - 尽可能避免使用global varible。 使用stateful的写法，尽量使用参数传递，避免使用field。
    
    ```java
    // 1) stateful
    int[] helper;
    public void mergeSort(int[] array){
    	mergeSort(array, 0, array.length - 1);
    }
    
    // 2) stateless
    public void mergetSort(int[] array){
    	int[] helper = new int[array.length];
    	mergeSort(array, helper, 0, array.length - 1);
    }
    ```
    
## Divide and Conquer - 分治法

__适用问题__

- 问题缩小到一定规模可以很容易的被解决，子问题相互独立。
- 问题可以分解为若干个规模较小的同类型子问题，即该问题具有**最优子结构**性质
- 利用该问题分解出的子问题的解可以合并为该问题的解。
- 该问题所分解出的各个子问题是相互独立的，即子问题之间不包含公共的子问题。

__基本问题__

- 是很多算法的基础（快速排序、归并排序）。
- 二叉树相关问题 - 使用二叉树的数据结构目的是，在解决问题时可以用分治法提高速度。

__三个步骤__

- **Divide 分解** - 将原问题分解为若干子问题，这些子问题都是原问题规模较小的实例。
- **Conquer 解决** - 递归地求解各子问题。如果子问题规模足够小，则直接求解该**base case**。
- **Combine 合并** - 将所有子问题的解合并为原问题的解。

__Conquer 的顺序__

- recursion 递归 / iteration 迭代
- DFS 纵向 / BFS 横向

## Rewrite recursive implementation to iterative implementation


- All recursive algorithms can be written as a _iterative_ version. Recursive version is a version using the system's call-function stack.
    - The size of call-function is 8M.
    - recursion缺点，可能会stackoverflow
    - 工业界场景中，很多应用是recursion写的。

- if it is a **tail recursion**, it can be easily written as iterative.
    - tail recursion: the recursive call is always the last execution statement
        - preorder/in/post都是dfs都不是tail recursion
- call stack vs. stack
- iteration写法中，如果需要回到目标节点的上一层，需要加入prev节点。


## Backtracking Implementation

- Base case
    - can be terminated condition
- Recursive rule


DFS / Backtracking / Recursion problems:

- [Subsets Problem](http://www.lintcode.com/zh-cn/problem/subsets-ii/#)
    - [Subsets Solution](http://www.jiuzhang.com/solutions/subsets/)

```python
# 1. recursive helper parameter and return type
# for return type, if we needs to record a max or min,
# we can use a global varible or put it both in the parameters and return type.
# Eg. subsets problem
# thisnode = (subsetStart, startIndex)
# background = nums
def recurhelper(background, thisnode, results):
    # 2. recursive helper exit
    if GOAL_TEST(thisnode):
        results.add(thisnode)
    
    # 3. expand this node and call recurhelper recursively.
    # EXPAND function returns hard copy of nodes
    for node in EXPAND(thisnode):
        recurhelper(background, node, results)
    
    return results
```
