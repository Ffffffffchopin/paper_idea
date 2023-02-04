
![[Pasted image 20230204211511.png]]

这道题的主要思想是贪心算法，即每次在遍历一个数时就判断修改返回结果。

我一开始的想法是暴力循环把每一种组合求和的结果都计算出来用有序的set来存储再比较最大连续区间

```C++
class Solution {

public:

    int getMaximumConsecutive(vector<int>& coins) {
        int n=coins.size();
        set<int> s;
        s.insert(0);
        for(int i=1;i<=n;i++){
            for(int j=0;j<n-i+1;j++){
                 int tmp=0;
                for(int k=j;k<j+i;k++){
                    tmp+=coins[k];
                }
                s.insert(tmp);
            }
        }
        int count=1;
        int pre=0;
        int ret=1;
        auto start=s.begin();
        start++;
        for(auto it=start;it!=s.end();it++){

            if(*it!=pre+1){

                if(count>=ret){

                    ret=count;
                }
                count=0;
                pre=*it;
            }
            else{
                count++;
                pre++;
            }
        }
        return ret;
    }
};
```

但是这个算法一开始就忽略了组合中的很大一部分（如果真的把循环全部写出来的话要四重循环估计还是会TLE），注定不会成功

看了题解以后才明白应该用DP贪心。

```c++
class Solution {
public:
    int getMaximumConsecutive(vector<int>& coins) {
        int res = 1;
        sort(coins.begin(), coins.end());
        for (auto& i : coins) {
            if (i > res) {
                break;
            }
            res += i;
        }
        return res;
    }
};
```
```python
class Solution:

    def getMaximumConsecutive(self, coins: List[int]) -> int:

        res=1

        coins=sorted(coins)

        for coin in coins:

            if coin>res :

                break

            res+=coin

        return res
       
```


假设一开始能得到的连续区间为 $[0,x]$，如果读入的剩余数中最小的那一个都大于当前的$x$，即$[x,x+y]$，那么后面的就更不可能构成连续区间。

这一类贪心题的特点就是推理比较复杂但表现在最后的算法上比较简洁，连续区间的题目经常用到这个算法。感觉自己在这方面还是有些不足，曾经做过的[795. 区间子数组个数 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-subarrays-with-bounded-maximum/)打算再看一遍，[洛谷的题单]([【算法1-5】贪心 - 题单 - 洛谷 | 计算机科学教育新生态 (luogu.com.cn)](https://www.luogu.com.cn/training/110#problems))也打算做一些再写一个总结。





