![image](https://user-images.githubusercontent.com/132556492/236167107-7bf3f0cc-8ad6-4f58-a65b-82b84e9f4957.png)
![image](https://user-images.githubusercontent.com/132556492/236167147-89351694-5484-4b37-adbb-6672d0d11be8.png)

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

