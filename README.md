数组
栈
队列
链表
二分搜索树
堆

线段树
Trie
并查集

AVL
红黑树
哈希表

平摊分析：Amortized Analysis, resize时候会引入。
remove_last时resize太过着急，出现复杂度震荡，使用lazy方案：
扩容2倍，缩容1/4（错开）

删除任意节点：
1. 叶子节点
2. 只有左孩子或者只有右孩子
3. 既有做孩子又有右孩子（* Hibbard Deletion *）:找被删节点右子树中方的最左节点（最小值）来代替

完全二叉树：不一定是满二叉树，但是缺失的节点一定是在树的右下侧

满二叉树：除了叶子节点，所有节点既有左孩子又有右孩子

二叉堆：
- 堆中任意节点的值一定小于等于其父节点的值（最大堆）
- 用数组实现即可
- 对于任意节点i，左孩子是2 * i + 1, 右孩子是2 * i + 2，父节点(i - 1) // 2 （因为索引从0开始）
- 添加元素时候，先在最下面的最左边添加一个元素，再执行sift_up操作
- sift_up: 新添加的节点和父亲节点比较，交换，再递归重复（因为如果新节点的值比父亲节点大，则一定比父亲节点的另一个节点大，大于号保持不变性）
- extract_max_heap: 取出堆顶的值，并将最小层最左边的元素移到堆顶，再执行sift_down
- sift_down: 每次要下沉的元素和两个孩子比较，和两个孩子中最大的交换位置，再递归重复
- replace: 取出一个最大的，再放入一个新元素，set 0 index，再从0开始sift_down
- heapify: 将任意数组整理成堆的形状, 从最后一个非叶子节点开始计算，倒着从后向前sift_down即可 (算法复杂度是O(n)的！！！)
- 最后一个非叶子节点：先拿到最后一个节点的索引，计算它的父亲节点的索引即可(再递归所有非叶子节点)！！！
- d叉堆 d-ary heap
- 索引堆：可以看到堆中间的元素（最短路径和Dijkstra中可能用到）
- 二项堆，斐波那契堆
- 广义队列（普通队列，优先队列，随机队列，栈也可以理解成一个队列）

线段树：O(logn)
- 区间染色
- 区间查询(动态不停的更新和查询), 区间本身固定
- 线段树不是完全二叉树，但是是一棵平衡二叉树（任何节点的左右深度之差小于等于1）
- 第h层（h从0开始）：h层有2 ** h - 1个节点
- 如果区间有n个元素，则4n的空间足以

Trie:
- 重点应用是查询前缀

UnionFind
- 连接问题
- union(e1, e2), query(e1, e2)
- use array for implementation
- 可以基于size优化
- 可以基于rank优化
- 路径压缩(发生在find操作中顺便进行)
- 查询合并都是O(h)
- 并查集的优势是在合并查询都有的场景

AVL
- G.M.Adelson-Velsky and E.M.Landis
- 自平衡二分搜索树
- 对于任意一个节点，左子树和右子树的高度差不能超过1
- 平衡因子：叶子节点为0，非叶子节点左右子树高度差
- 左旋转，右旋转，在插入节点的时候造成了不平衡 LL, RR
- 插入的元素在不平衡的节点的左侧的左侧 -> 右旋转，将下图的B作为新节点
```
          A
        /
      B
    /
new node
```
- LR和RL LR -> LL, RL -> RR
```
          A
         /
        B
         \
      new node
```