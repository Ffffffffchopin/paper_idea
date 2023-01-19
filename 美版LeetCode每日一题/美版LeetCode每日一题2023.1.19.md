![[Pasted image 20230119220722.png]]

这道题其实并不算难，但最终我是靠看了一个印度人的题解才做出来的。

实际上这种连续子数组的题一般都会有一些规律，比如这道题我们发现求出每个数前缀和与k取余的结果西相同的两项可以组成满足条件的连续子数组，因此我们只需要求出循环求出加上每一个数后的前缀和取余K的结果即可。

为了不减少空间消耗不存储前缀和数组，只储存当前前缀和，每次加上一个数的取余结果，但因为Hashmap数组只有k位，为了防止溢出每次都要加K和取余K。

```c++
class Solution {

public:

    int subarraysDivByK(vector<int>& nums, int k) {

  

       int count=0;

       vector<int> sums(k,0);

       sums[0]++;

       int curr_sum=0;

       for(int num : nums){

           curr_sum=(curr_sum+num%k+k)%k;

           count+=sums[curr_sum];

           sums[curr_sum]++;

       }

       return count;

  

    }

};
```
