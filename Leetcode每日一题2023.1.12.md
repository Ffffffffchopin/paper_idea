

![[Pasted image 20230112230203.png]]

今天的每日一题主题还是二叉树遍历，题意大概是遍历二叉树取出所有子树的相同字母出现频率，不算太难（虽然我还是花了好久才写出来：）

思路很清晰，先从所给的edges的数组中遍历得到邻接表再开始DFS循环，但是会遇到的问题是引用传递的全局数组ret会记录所有label出现的频率包括父节点的导致出错。

为了解决这个问题我们引入map数组，在递归函数调用时记录所求节点频率值，结束时再减去前面记录的值便得到了子树的频率值

另外一开始提交时因为全部都是直接传值，测试用例中有一个n=2650的用例死活过不去，后来看了题解才知道是因为邻接表比较大直接传值在递归的时候开销极大。（留下了新手的泪水：）

```c++
class Solution {

public:

  

    void dfs(vector<vector<int> >& adj,int node,int prev,vector<int>& ret,string& labels,vector<int>& map){

        int i=labels[node]-'a';

       int prev_count=map[i];

       map[i]++;

        for(auto ele:adj[node]){

            if(ele!=prev){

                dfs(adj,ele,node,ret,labels,map);

            }

        }

        ret[node]=map[i]-prev_count;

    }

  

    vector<int> countSubTrees(int n, vector<vector<int>>& edges, string labels) {

        vector<vector<int> > adj(n);

        for(auto edge:edges){

            adj[edge[0]].push_back(edge[1]);

            adj[edge[1]].push_back(edge[0]);

        }

        vector<int> ret(n,0);

        vector<int> map(26,0);

        dfs(adj,0,0,ret,labels,map);

        return ret;

    }

};
```

