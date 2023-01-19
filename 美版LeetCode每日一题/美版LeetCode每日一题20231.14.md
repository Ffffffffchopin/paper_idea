
![[Pasted image 20230114170306.png]]

这是一个简单的并查集问题，一开始尝试用最小堆但发现无法处理堆的归并问题所以想到用数组做树进行并查集（看了Solutions好像他们都是用递归实现的并查集，不知道是不是时间复杂度会低一点，在查找的过程中顺便解决排序的问题。

```c++
class Solution {

public:

    string smallestEquivalentString(string s1, string s2, string baseStr) {

        vector<int> tree(26);

        for(int i=0;i<26;i++){

            tree[i]=i;

        }

        unordered_set<char> visited;

        for(int i=0;i<s1.size();i++){

            char a=s1[i]-'a';

            char b=s2[i]-'a';

            if(tree[a]==tree[b]){

                continue;

            }

            int min,max;

            if (tree[a]<=tree[b]){

                min=a;

                max=b;

            }

            else{

                min=b;

                max=a;

            }

            for(char c:visited){

                if((c==s1[i])||(c==s2[i])){

                    continue;

                }

                if(tree[c-'a']==tree[max]){

                    tree[c-'a']=tree[min];

                }

            }

             tree[max]=tree[min];

            visited.insert(s1[i]);

            visited.insert(s2[i]);

        }

        string ret="";

        for(char c:baseStr){

            char tmp=tree[c-'a']+97;

            ret+=tmp;

        }

        return ret;

    }

};
```