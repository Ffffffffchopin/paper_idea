![[Pasted image 20230113160908.png]]

为了统计词频使用数组哈希表节省时间，但因为target字符串中可能出现重复所以要在target中也建立一个哈希表。之后再循环每个词的频率除以在target中出现的频率再找到最小值即可

  
  

```c++

class Solution {

public:

    int rearrangeCharacters(string s, string target) {

        vector<int> map_s(26,0);

        vector<int> map_tar(26,0);

        for(char c:target){

            map_tar[c-'a']++;

        }

        for(char c:s){

            map_s[c-'a']++;

        }

        int min=10000;

        for(char c :target){

            int tmp=map_s[c-'a']/map_tar[c-'a'];

            if(tmp<=min){

                min=tmp;

            }

        }

        return min;

    }

};

```