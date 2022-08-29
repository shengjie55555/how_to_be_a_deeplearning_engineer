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

## 回溯
1. 全排列：https://leetcode.cn/problems/permutations/
2. 全排列Ⅱ：https://leetcode.cn/problems/permutations-ii/

## 贪心算法
1. 分发饼干：
2. 摆动序列：https://leetcode.cn/problems/wiggle-subsequence/
3. 最大子数组和：https://leetcode.cn/problems/maximum-subarray/
4. 买卖股票最佳时机Ⅱ：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/
5. 跳跃游戏：https://leetcode.cn/problems/jump-game/
6. 跳跃游戏Ⅱ：https://leetcode.cn/problems/jump-game-ii/
7. K次取反后最大化数组和：https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/


## 动态规划
1. 斐波那契数：
2. 爬楼梯：
3. 使用最小花费爬楼梯：
4. 不同路径：
5. 不同路径Ⅱ：
6. 整数拆分：
7. 不同的二叉搜索树：
8. 分割等和子集：https://leetcode.cn/problems/partition-equal-subset-sum/
9. 最后一块石头的重量Ⅱ：
10. 目标和：https://leetcode.cn/problems/target-sum/
11. 一和零：https://leetcode.cn/problems/ones-and-zeroes/
12. 零钱兑换Ⅱ：https://leetcode.cn/problems/coin-change-2/
13. 组合总和Ⅳ：
14. 爬楼梯：
15. 零钱兑换：
16. 完全平方数：
17. 单词拆分：
18. 打家劫舍：https://leetcode.cn/problems/house-robber/
19. 打家劫舍Ⅱ：
20. 打家劫舍Ⅲ：
21. 买卖股票的最佳时机：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/
22. 买卖股票的最佳时机Ⅱ：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/
23. 买卖股票的最佳时机Ⅲ：
24. 买卖股票的最佳时机Ⅳ：
25. 最佳买卖股票时机含冷冻期：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/
26. 买卖股票的最佳时机含手续费：
27. 最长递增子序列：
28. 最长连续递增子序列：
29. 最长重复子数组：
30. 最长公共子序列：
31. 最大子序和：https://leetcode.cn/problems/maximum-subarray/
32. 判断子序列：
33. 不同的子序列：
34. 两个字符串的删除操作：
35. 编辑距离：
36. 回文子串：
37. 最长回文子序列：
38. **最大正方形**：https://leetcode.cn/problems/maximal-square/

## 单调栈
1. 每日温度：https://leetcode.cn/problems/daily-temperatures/
2. 下一个更大元素Ⅰ：https://leetcode.cn/problems/next-greater-element-i/
3. 下一个更大元素Ⅱ：https://leetcode.cn/problems/next-greater-element-ii/
4. 接雨水：https://leetcode.cn/problems/trapping-rain-water/
5. 柱状图中最大的矩形：https://leetcode.cn/problems/largest-rectangle-in-histogram/