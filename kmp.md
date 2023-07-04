![image](https://user-images.githubusercontent.com/132556492/236167107-7bf3f0cc-8ad6-4f58-a65b-82b84e9f4957.png)
![image](https://user-images.githubusercontent.com/132556492/236167147-89351694-5484-4b37-adbb-6672d0d11be8.png)

[力扣28题](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)

自己写的：
```c++
int kmp(string str1, string str2) {
    int i = 0, j = 0;
    vector<int> nextarr = getNextArray(str2);
    while(i < str1.size() && j < str2.size()) {
        if(str1[i] == str2[j]) {
            ++i;
            ++j;
        } else if(nextarr[j] != -1) {
            j = nextarr[j];
        } else {
            ++i;
        }
    }
    return j == str2.size() ? i - j : -1;
}

vector<int> getNextArray(string str) {
    if(str.size() < 2) return {-1};
    vector<int> next(str.size());
    next[0] = -1;
    next[1] = 0;
    int cn = 0, i = 2;
    while(i < str.size()) {
        if(str[i-1] == str[cn]) next[i++] = ++cn;
        else if(cn > 0) cn = next[cn];
        else next[i++] = 0;
    }
    return next;
}
```

代码随想录中的kmp算法：
```c++
vector<int> getNext(string& s) {
    vector<int> next(s.size());
    next[0] = 0;
    int j = 0;
    for(int i = 1; i < s.size(); ++i) {
        while(j > 0 && s[i] != s[j]) {
            j = next[j-1];
        }
        if(s[i] == s[j]) ++j;
        next[i] == j;
    }
    return next;
}
int kmp(string s1, string s2) {
    if(s1.size() == 0) return 0;
    vector<int> next = getNext(s2);
    int j = 0;
    for(int i = 0; i < s1.size(); ++i) {
        while(j > 0 && s1[i] != s2[j]) {
            j = next[j-1];
        }
        if(s1[i] == s2[j]) ++j;
        if(j == s2.size()) return i - j + 1；
    }
    return -1;
}
```

**左神对于前缀表的定义和代码随想录中不同，为代码随想录中整体往右移一位**
[这个视频](https://www.bilibili.com/video/BV1AY4y157yL/?spm_id_from=333.337.search-card.all.click&vd_source=e9b57106217eb0b65e4076cf4bcc7a73)前半段讲得可以
