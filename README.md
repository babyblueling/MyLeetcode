# Leetcode

## 目录

- [1、数组](#1数组)
- [2、字符串](#2字符串)
- [剑指offer67题](#剑指offer67题)
- [每日一题](#每日一题)

## 1、数组

### [414.第三大的数](https://leetcode.cn/problems/third-maximum-number/description/)

要求返回第三大的数，指的是所有不同的数字中排第三的数。

**int**占用4字节，取值范围为-2^31^~2^31^-1。**long**在64位编译器上占用8字节

### [581.最短无序连续子数组](https://leetcode.cn/problems/shortest-unsorted-continuous-subarray/)

### [605.种花问题](https://leetcode.cn/problems/can-place-flowers/)

### [628.三个数的最大乘积](https://leetcode.cn/problems/maximum-product-of-three-numbers/submissions/)

### [643.子数组最大平均数](https://leetcode.cn/problems/maximum-average-subarray-i/)

### [665.非递减数列](https://leetcode.cn/problems/non-decreasing-array/) 

### [674.最长连续递增序列](https://leetcode.cn/problems/longest-continuous-increasing-subsequence/)

### [697数组的度](https://leetcode.cn/problems/degree-of-an-array/)

### [717.1比特与2比特字符](https://leetcode.cn/problems/1-bit-and-2-bit-characters/)

### [724.寻找数组的中心下标](https://leetcode.cn/problems/find-pivot-index/)

### [747.至少是其他数字两倍的最大数](https://leetcode.cn/problems/largest-number-at-least-twice-of-others/)

### [830.较大分组的位置](https://leetcode.cn/problems/positions-of-large-groups/)

### [840.矩阵中的幻方](https://leetcode.cn/problems/magic-squares-in-grid/)

### [849.到最近的人的最大距离](https://leetcode.cn/problems/maximize-distance-to-closest-person/)

### [888.公平的糖果交换](https://leetcode.cn/problems/fair-candy-swap/)

### [914.卡牌分组](https://leetcode.cn/problems/x-of-a-kind-in-a-deck-of-cards/solutions/)

- [优化的解法](https://leetcode.cn/problems/x-of-a-kind-in-a-deck-of-cards/solutions/172845/tu-jie-su-shu-shai-c-by-time-limit/)

### [941.有效的山脉数组](https://leetcode.cn/problems/valid-mountain-array/)

### [989.数组形式的整数加法](https://leetcode.cn/problems/add-to-array-form-of-integer/)

- [加法模板，秒杀所有逐位相加](https://leetcode.cn/problems/add-to-array-form-of-integer/solutions/570659/989-ji-zhu-zhe-ge-jia-fa-mo-ban-miao-sha-8y9r/)

位运算、逐位相加模板：

```
while ( A 没完 || B 没完)
    A 的当前位
    B 的当前位

    和 = A 的当前位 + B 的当前位 + 进位carry

    当前位 = 和 % 10;
    进位 = 和 / 10;

判断还有进位吗
```

### [1128.等价多米诺骨牌对的数量](https://leetcode.cn/problems/number-of-equivalent-domino-pairs/)

### [剑指offer 66.构建乘积数组](https://leetcode.cn/problems/gou-jian-cheng-ji-shu-zu-lcof/)

### [11.盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

### [1497.检查数组对是否可以被k整除](https://leetcode.cn/problems/check-if-array-pairs-are-divisible-by-k/)

### [15.三数之和](https://leetcode.cn/problems/3sum/solutions/)

> 代码随想录中的哈希表方法没看懂

### [18.四数之和](https://leetcode.cn/problems/4sum/description/)

## 2、字符串

### [13.罗马数字转整数](https://leetcode.cn/problems/roman-to-integer/)

### [67.二进制求和](https://leetcode.cn/problems/add-binary/)

利用逐位相加模板，自己写的：

```c++
class Solution {
public:
    string addBinary(string a, string b) {
        reverse(a.begin(), a.end());
        reverse(b.begin(), b.end());
        string ans;
        int len1 = a.size(), len2 = b.size(), i = 0, j = 0, carry = 0;
        while(i < len1 || j < len2) {
            int num1 = i == len1 ? 0 : a[i++]-'0';
            int num2 = j == len2 ? 0 : b[j++]-'0';
            ans += to_string((num1 + num2 + carry) % 2);
            carry = (num1 + num2 + carry) / 2;
        }
        if(carry != 0) ans.push_back('1');
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

### [434.字符串中的单词数](https://leetcode.cn/problems/number-of-segments-in-a-string/)

### [680.验证回文串II](https://leetcode.cn/problems/valid-palindrome-ii/)

### [686.重复叠加字符串匹配](https://leetcode.cn/problems/repeated-string-match/)
> KMP算法进阶

### [819.最常见的单词](https://leetcode.cn/problems/most-common-word/)
使用标准库的代码(力扣大神子不语)

```c++
class Solution {
public:
    string mostCommonWord(string paragraph, vector<string>& banned) {
        transform(paragraph.cbegin(), paragraph.cend(), paragraph.begin(), 
            [](auto& i) { return isalpha(i) ? tolower(i) : ' '; });
        stringstream ss(paragraph);
        unordered_set ban(banned.cbegin(), banned.cend());
        unordered_map<string, size_t> dict;

        for (string tmp; ss >> tmp; ban.count(tmp) ? 0 : dict[tmp]++);
        return max_element(dict.cbegin(), dict.cend(), [](auto& a, auto& b) {return a.second < b.second; })->first;
    }
};
```

### [859.亲密字符串](https://leetcode.cn/problems/buddy-strings/)

### [6.N字形变换](https://leetcode.cn/problems/zigzag-conversion/)

### [541.反转字符串II](https://leetcode.cn/problems/reverse-string-ii/description/) 

### [151.反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string/description/)
> 进阶：原地修改

## 剑指offer67题

### [04.二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

如果没有判断矩阵为空，会报错

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        int i = 0, j = n-1;
        while(j >= 0 && i < m) {
            if(matrix[i][j] > target) --j;
            else if(matrix[i][j] < target) ++i;
            else return true;
        }
        return false;
    }
};
```

> **执行出错** Line 1033: Char 9: runtime error: reference binding to null pointer of type 'std::vector<int, std::allocator<int>>' (stl_vector.h) SUMMARY: UndefinedBehaviorSanitizer: undefined-behavior /usr/bin/../lib/gcc/x86_64-linux-gnu/9/../../../../include/c++/9/bits/stl_vector.h:1043:9

**k神代码也没有判断数组为空，为什么不会报错？**

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        int i = matrix.size() - 1, j = 0;
        while(i >= 0 && j < matrix[0].size())
        {
            if(matrix[i][j] > target) i--;
            else if(matrix[i][j] < target) j++;
            else return true;
        }
        return false;
    }
};
```

### [05.替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

### [06.从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

### [07.重建二叉树](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/description/)

### [09.用两个栈实现队列](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

> 理解代码随想录中的解法

### [11.旋转数组的最小数字](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

### [10.斐波那契数列](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/)

### [10-II.青蛙跳台阶问题](https://leetcode.cn/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

### [跳台阶扩展问题](https://www.nowcoder.com/practice/22243d016f6b47f2a6928b4313c85387?tpId=13&&tqId=11162&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### [矩阵覆盖](https://www.nowcoder.com/practice/72a5a919508a4251859fb2cfb987a0e6?tpId=13&&tqId=11163&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### [15.二进制中1的个数](https://leetcode.cn/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

### [16.数值的整数次方](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

自己写的

```c++
class Solution {
public:
    // 快速幂 + 递归
    double myPowCore(double x, long long a) {
        if(a == 1) return x;
        if(a % 2 != 0) {
            double half = myPowCore(x, a/2);
            return half*half*x;
        }
        else {
            double half = myPowCore(x, a/2);
            return half*half;
        }
    }
    double myPow(double x, int n) {
        if(n == 0 || x == 1) return 1;
        long long a = n;
        bool flag = false;
        if(n < 0) {
            a = -a;
            flag = true;
        }
        return flag ? 1.0/myPowCore(x,a) : myPowCore(x,a);
    }
};
```

> 在处理有可能溢出的问题时，**不要用abs()函数**

![image](https://user-images.githubusercontent.com/132556492/236165090-64fa75cb-f36c-4ae0-9026-e0b3dbf4e309.png)

### [21.调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

### ~~[22.链表中倒数第k个节点](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)~~

### [24.反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)

> 别定义pre、cur、next三个指针，显得代码臃肿

### [25.合并两个排序的链表](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/description/)

> 要写出简洁代码

### [26.树的子结构](https://leetcode.cn/problems/shu-de-zi-jie-gou-lcof/)

### [27.二叉树的镜像](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/description/)

> 递归、辅助栈

## 每日一题

### [2532.过桥的时间](https://leetcode.cn/problems/time-to-cross-a-bridge/solutions/)

### [16.最接近的三数之和](https://leetcode.cn/problems/3sum-closest/description/) 灵神题解

### [1911.最大子序列交替和](https://leetcode.cn/problems/maximum-alternating-subsequence-sum/description/) -> [看这个题解](https://leetcode.cn/problems/maximum-alternating-subsequence-sum/solutions/2339030/python3javacgotypescript-yi-ti-yi-jie-do-22yp/)

### [979.在二叉树中分配硬币](https://leetcode.cn/problems/distribute-coins-in-binary-tree/) 灵神题解

### [834.树中距离之和](https://leetcode.cn/problems/sum-of-distances-in-tree/description/) 灵神题解

### [1851.包含每个查询的最小区间](https://leetcode.cn/problems/minimum-interval-to-include-each-query/description/) [b站题解](https://www.bilibili.com/video/BV1Gq4y1L7cz/?spm_id_from=333.337.search-card.all.click&vd_source=e9b57106217eb0b65e4076cf4bcc7a73)

### [874.模拟行走机器人](https://leetcode.cn/problems/walking-robot-simulation/description/)
> 哈希

### [2569.更新数组后处理求和查询](https://leetcode.cn/problems/handling-sum-queries-after-update/description/) 灵神b站视频->[这里](https://www.bilibili.com/video/BV15D4y1G7ms/?spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=e9b57106217eb0b65e4076cf4bcc7a73)

- 将nums1构造成seg_tree，实现为数组，树中每个元素表示对应区间内1的个数
- seg_tree索引从1开始
- update函数的边界条件：当要更新的区间包含对应节点的区间时
- 注意关于lazy的部分

### [2050.并行课程III](https://leetcode.cn/problems/parallel-courses-iii/description/) 有向无环图

- [拓扑排序解法](https://www.bilibili.com/video/BV1PP4y1j7ik/?spm_id_from=333.337.search-card.all.click&vd_source=e9b57106217eb0b65e4076cf4bcc7a73)
- 含有dp的解法

### [2681.英雄的力量](https://leetcode.cn/problems/power-of-heroes/description/)

### [1749.任意子数组和的绝对值的最大值](https://leetcode.cn/problems/maximum-absolute-sum-of-any-subarray/description/)

### [1289.下降路径最小和II](https://leetcode.cn/problems/minimum-falling-path-sum-ii/description/)

### [23.合并k个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/) 
> 最小堆 分治

### [833.字符串中的查找与替换](https://leetcode.cn/problems/find-and-replace-in-string/description/)

### [1444.切披萨的方案数](https://leetcode.cn/problems/number-of-ways-of-cutting-a-pizza/description/)

### [1388.3n块披萨](https://leetcode.cn/problems/pizza-with-3n-slices/description/)

### [57.插入区间](https://leetcode.cn/problems/insert-interval/description/)

### [823.带因子的二叉树](https://leetcode.cn/problems/binary-trees-with-factors/description/) 灵神题解
