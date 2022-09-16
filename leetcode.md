# ACM模式
```C++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main() {
    int n;
    /* 同时处理多个测试用例
     * getline(cin, str): 读取一行到str字符串中，需要包含string
     */
    while (cin >> n) {
        vector<int> gym(n);
        vector<int> work(n);
        for (int i = 0; i < n; i++) cin >> work[i];
        for (int i = 0; i < n; i++) cin >> gym[i];
        int result = 0;

        // 处理逻辑

        cout << result << endl;
    }
    return 0;
}
```
如何构造二叉树：https://www.programmercarl.com/%E5%89%8D%E5%BA%8F/ACM%E6%A8%A1%E5%BC%8F%E5%A6%82%E4%BD%95%E6%9E%84%E5%BB%BA%E4%BA%8C%E5%8F%89%E6%A0%91.html#java

# 数组
1. 二分查找：https://leetcode.cn/problems/binary-search/
2. 移除元素：https://leetcode.cn/problems/remove-element/
3. 有序数组的平方：https://leetcode.cn/problems/squares-of-a-sorted-array/
4. 长度最小的子数组：https://leetcode.cn/problems/minimum-size-subarray-sum/
5. 螺旋矩阵Ⅱ：https://leetcode.cn/problems/spiral-matrix-ii/

# 链表
1. 移除链表元素：https://leetcode.cn/problems/remove-linked-list-elements/
2. 设计链表：https://leetcode.cn/problems/design-linked-list/
3. 反转链表：https://leetcode.cn/problems/reverse-linked-list/
4. 两两交换链表中的节点：https://leetcode.cn/problems/swap-nodes-in-pairs/
5. 删除链表倒数第N个节点：https://leetcode.cn/problems/remove-nth-node-from-end-of-list/
6. 环形链表Ⅱ：https://leetcode.cn/problems/linked-list-cycle-ii/
7. 链表排序：https://leetcode.cn/problems/7WHec2/
8. K个一组反转链表：https://leetcode.cn/problems/reverse-nodes-in-k-group/
9. 重排链表：https://leetcode.cn/problems/reorder-list/

# 哈希表
1. 有效的字母异位词：https://leetcode.cn/problems/valid-anagram/
2. 两个数组的交集：https://leetcode.cn/problems/intersection-of-two-arrays/
3. 快乐数：https://leetcode.cn/problems/happy-number/
4. 两数之和：https://leetcode.cn/problems/two-sum/
5. 四数相加Ⅱ：https://leetcode.cn/problems/4sum-ii/
6. 赎金信：https://leetcode.cn/problems/ransom-note/
7. 三数之和：https://leetcode.cn/problems/3sum/
8. 四数之和：https://leetcode.cn/problems/4sum/

# 字符串
1. 反转字符串：https://leetcode.cn/problems/reverse-string/
2. 反转字符串Ⅱ：https://leetcode.cn/problems/reverse-string-ii/
3. 替换空格：https://leetcode.cn/problems/ti-huan-kong-ge-lcof/
4. 翻转字符串里的单词：https://leetcode.cn/problems/reverse-words-in-a-string/
5. 左旋转字符串Ⅱ：https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/
6. 重复的子字符串：https://leetcode.cn/problems/repeated-substring-pattern/

## 双指针
1. 移除元素：https://leetcode.cn/problems/remove-element/
2. 反转字符串：https://leetcode.cn/problems/reverse-string/
3. 替换空格：https://leetcode.cn/problems/ti-huan-kong-ge-lcof/
4. 翻转字符串里的单词：https://leetcode.cn/problems/reverse-words-in-a-string/
5. 反转链表：https://leetcode.cn/problems/reverse-linked-list/
6. 删除倒数第N个节点：https://leetcode.cn/problems/remove-nth-node-from-end-of-list/
7. 链表相交：https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/
8. 环形链表Ⅱ：https://leetcode.cn/problems/linked-list-cycle-ii/

## 排序
1. 链表排序：https://leetcode.cn/problems/7WHec2/
2. 数组中的第k大的数字：https://leetcode.cn/problems/xx4gT2/

## 栈与队列
1. 用栈实现队列：https://leetcode.cn/problems/implement-queue-using-stacks/
2. 用队列实现栈：https://leetcode.cn/problems/implement-stack-using-queues/
3. 有效的括号：https://leetcode.cn/problems/valid-parentheses/
4. 删除字符串中相邻重复项：https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/
5. 逆波兰表达式求值：https://leetcode.cn/problems/evaluate-reverse-polish-notation/
6. 滑动窗口最大值：https://leetcode.cn/problems/sliding-window-maximum/
7. 前k个高频元素：https://leetcode.cn/problems/top-k-frequent-elements/

## 二叉树
1. 前序遍历：https://leetcode.cn/problems/binary-tree-preorder-traversal/
2. 中序遍历：https://leetcode.cn/problems/binary-tree-inorder-traversal/
3. 后序遍历：https://leetcode.cn/problems/binary-tree-postorder-traversal/
4. 层序遍历：https://leetcode.cn/problems/binary-tree-level-order-traversal/
5. 翻转二叉树：https://leetcode.cn/problems/invert-binary-tree/
6. 对称二叉树：https://leetcode.cn/problems/symmetric-tree/
7. 二叉树的最大深度：https://leetcode.cn/problems/maximum-depth-of-binary-tree/
8. 二叉树的最小深度：https://leetcode.cn/problems/minimum-depth-of-binary-tree/
9. 完全二叉树的节点个数：https://leetcode.cn/problems/count-complete-tree-nodes/
10. 平衡二叉树：https://leetcode.cn/problems/balanced-binary-tree/
11. 二叉树的所有路径：https://leetcode.cn/problems/binary-tree-paths/
12. 左叶子之和：https://leetcode.cn/problems/sum-of-left-leaves/
13. 找树左下角的值：https://leetcode.cn/problems/find-bottom-left-tree-value/
14. 路径总和：https://leetcode.cn/problems/path-sum/
15. 从中序和后序遍历序列构造二叉树：https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
16. 最大二叉树：https://leetcode.cn/problems/maximum-binary-tree/
17. 合并二叉树：https://leetcode.cn/problems/merge-two-binary-trees/
18. 二叉搜索树的搜索：https://leetcode.cn/problems/search-in-a-binary-search-tree/
19. 验证二叉搜索树：https://leetcode.cn/problems/validate-binary-search-tree/
20. 二叉搜索树的最小绝对差：https://leetcode.cn/problems/minimum-absolute-difference-in-bst/
21. 二叉搜索树的众数：https://leetcode.cn/problems/find-mode-in-binary-search-tree/
22. 二叉树的最近公共祖先：https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/
23. 二叉搜索树的最近公共祖先：https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/
24. 二叉搜索树中的插入操作：https://leetcode.cn/problems/insert-into-a-binary-search-tree/
25. 删除二叉搜索树中的节点：https://leetcode.cn/problems/delete-node-in-a-bst/
26. 修建二叉搜索树：https://leetcode.cn/problems/trim-a-binary-search-tree/
27. 将有序数组转换为二叉搜索树：https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/
28. 把二叉搜索树转换为累加树：https://leetcode.cn/problems/convert-bst-to-greater-tree/
29. 二叉搜索树的后序遍历序列：https://leetcode.cn/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/

## 回溯
1. 组合：https://leetcode.cn/problems/combinations/
2. 组合总和Ⅲ：https://leetcode.cn/problems/combination-sum-iii/
3. 电话号码的字母组合：https://leetcode.cn/problems/letter-combinations-of-a-phone-number/
4. 组合总和：https://leetcode.cn/problems/combination-sum/
5. 组合总和Ⅱ：https://leetcode.cn/problems/combination-sum-ii/
6. 分割回文串：https://leetcode.cn/problems/palindrome-partitioning/
7. 复原ip地址：https://leetcode.cn/problems/restore-ip-addresses/
8. 子集：https://leetcode.cn/problems/subsets/
9. 子集Ⅱ：https://leetcode.cn/problems/subsets-ii/
10. 递增子序列：https://leetcode.cn/problems/increasing-subsequences/
11. 全排列：https://leetcode.cn/problems/permutations/
12. 全排列Ⅱ：https://leetcode.cn/problems/permutations-ii/

# dfs & bfs
1. 岛屿数量：https://leetcode.cn/problems/number-of-islands/
2. 统计子岛屿：https://leetcode.cn/problems/count-sub-islands/
3. 岛屿的最大面积：https://leetcode.cn/problems/max-area-of-island/
4. 太平洋大西洋水流问题：https://leetcode.cn/problems/pacific-atlantic-water-flow/
5. **二进制矩阵中的最短路径**：https://leetcode.cn/problems/shortest-path-in-binary-matrix/

## 贪心算法
1. 分发饼干：https://leetcode.cn/problems/assign-cookies/
2. 摆动序列：https://leetcode.cn/problems/wiggle-subsequence/
3. 最大子数组和：https://leetcode.cn/problems/maximum-subarray/
4. 买卖股票最佳时机Ⅱ：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/
5. 跳跃游戏：https://leetcode.cn/problems/jump-game/
6. 跳跃游戏Ⅱ：https://leetcode.cn/problems/jump-game-ii/
7. K次取反后最大化数组和：https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/
8. **加油站**：https://leetcode.cn/problems/gas-station/
9. 分发糖果：https://leetcode.cn/problems/candy/
10. 柠檬水找零：https://leetcode.cn/problems/lemonade-change/
11. 根据身高重建队列：https://leetcode.cn/problems/queue-reconstruction-by-height/
12. 用最少数量的箭引爆气球：https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/
13. 无重叠区间：https://leetcode.cn/problems/non-overlapping-intervals/
14. 划分字母区间：https://leetcode.cn/problems/partition-labels/
15. 合并区间：https://leetcode.cn/problems/merge-intervals/
16. 单调递增的数字：https://leetcode.cn/problems/monotone-increasing-digits/
17. 盛最多水的容器：https://leetcode.cn/problems/container-with-most-water/

## 动态规划
1. 斐波那契数：https://leetcode.cn/problems/fibonacci-number/
2. 爬楼梯：https://leetcode.cn/problems/climbing-stairs/
3. 使用最小花费爬楼梯：https://leetcode.cn/problems/min-cost-climbing-stairs/
4. 不同路径：https://leetcode.cn/problems/unique-paths/
5. 不同路径Ⅱ：https://leetcode.cn/problems/unique-paths-ii/
6. 整数拆分：https://leetcode.cn/problems/integer-break/
7. 不同的二叉搜索树：https://leetcode.cn/problems/unique-binary-search-trees/
8. 分割等和子集：https://leetcode.cn/problems/partition-equal-subset-sum/
9. 最后一块石头的重量Ⅱ：https://leetcode.cn/problems/last-stone-weight-ii/
10. 目标和：https://leetcode.cn/problems/target-sum/
11. 一和零：https://leetcode.cn/problems/ones-and-zeroes/
12. 零钱兑换Ⅱ：https://leetcode.cn/problems/coin-change-2/
13. 组合总和Ⅳ：https://leetcode.cn/problems/combination-sum-iv/
14. 爬楼梯：https://leetcode.cn/problems/climbing-stairs/
15. 零钱兑换：https://leetcode.cn/problems/coin-change/
16. 完全平方数：https://leetcode.cn/problems/perfect-squares/
17. 单词拆分：https://leetcode.cn/problems/word-break/
18. 打家劫舍：https://leetcode.cn/problems/house-robber/
19. 打家劫舍Ⅱ：https://leetcode.cn/problems/house-robber-ii/
20. 打家劫舍Ⅲ：https://leetcode.cn/problems/house-robber-iii/
21. 买卖股票的最佳时机：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/
22. 买卖股票的最佳时机Ⅱ：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/
23. 买卖股票的最佳时机Ⅲ：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/
24. 买卖股票的最佳时机Ⅳ：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/
25. 最佳买卖股票时机含冷冻期：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/
26. 买卖股票的最佳时机含手续费：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/
27. 最长递增子序列：https://leetcode.cn/problems/longest-increasing-subsequence/
28. 最长连续递增子序列：https://leetcode.cn/problems/longest-continuous-increasing-subsequence/
29. 最长重复子数组：https://leetcode.cn/problems/maximum-length-of-repeated-subarray/
30. 最长公共子序列：https://leetcode.cn/problems/longest-common-subsequence/
31. 不相交的线：https://leetcode.cn/problems/uncrossed-lines/
32. 最大子序和：https://leetcode.cn/problems/maximum-subarray/
33. 判断子序列：https://leetcode.cn/problems/is-subsequence/
34. 不同的子序列：https://leetcode.cn/problems/distinct-subsequences/
35. 两个字符串的删除操作：https://leetcode.cn/problems/delete-operation-for-two-strings/
36. 编辑距离：https://leetcode.cn/problems/edit-distance/
37. 回文子串：https://leetcode.cn/problems/palindromic-substrings/
38. 最长回文子序列：https://leetcode.cn/problems/longest-palindromic-subsequence/
39. **最大正方形**：https://leetcode.cn/problems/maximal-square/
40. **最小路径之和**：https://leetcode.cn/problems/0i0mDW/

## 单调栈
1. 每日温度：https://leetcode.cn/problems/daily-temperatures/
2. 下一个更大元素Ⅰ：https://leetcode.cn/problems/next-greater-element-i/
3. 下一个更大元素Ⅱ：https://leetcode.cn/problems/next-greater-element-ii/
4. 接雨水：https://leetcode.cn/problems/trapping-rain-water/
5. 柱状图中最大的矩形：https://leetcode.cn/problems/largest-rectangle-in-histogram/

## 迷宫
1. 创建迷宫
   1. Prim算法：https://blog.csdn.net/qq_38677814/article/details/79745659
      1. 用一个大矩阵代表maze，包括墙和边缘，初始化（1，1）为起点，bfs添加墙体
      2. 随机选择一个墙体，并按照方向穿过墙体，如果下一位置是墙体则拆掉，重新bfs，如果不是，不需要bfs，删除选中的墙体
2. 