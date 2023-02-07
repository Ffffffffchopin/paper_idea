
![[Pasted image 20230115205406.png]]

这道题很简单，用递归就可以轻松解决，在每一个递归循环中新建数组直到数组中只有一个数
```c++
class Solution {

public:

    int minMaxGame(vector<int>& nums) {

        vector<int> ret= recursion(nums);

        return ret[0];

    }

    vector<int> recursion(vector<int>& nums){

        if(nums.size()==1){

            return nums;

        }

        vector<int> newNums(nums.size()/2);

        for(int i=0;i<nums.size()/2;i++){

            if(i%2==0){

                newNums[i]=min(nums[2*i],nums[2*i+1]);

            }

            else{

                newNums[i]=max(nums[2*i],nums[2*i+1]);

            }

        }

        return recursion(newNums);

  

    }

};
```
