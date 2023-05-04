# Leetcode

## 目录

- [1、数组](#1数组)
- [2、字符串](#2字符串)
- [剑指offer67题](#剑指offer67题)

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

