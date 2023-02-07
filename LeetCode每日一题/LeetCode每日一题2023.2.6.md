
![[Pasted image 20230206165631.png]]

今天的每日一题确实没什么好说的，非常简单的递归，只是一开始没看到完整二叉树的规则还纠结怎么判断子树数量和退出条件耽误了时间

```c++ 
/**

 * Definition for a binary tree node.

 * struct TreeNode {

 *     int val;

 *     TreeNode *left;

 *     TreeNode *right;

 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}

 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}

 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}

 * };

 */

class Solution {

public:

    bool evaluateTree(TreeNode* root) {

        if(root==nullptr){

            return false;

        }

        return recursion(root);

    }

  

    bool recursion(TreeNode* root){

        if(root->val==2){

            return recursion(root->left)||recursion(root->right);

        }

        if(root->val==3){

            return recursion(root->left)&&recursion(root->right);

        }

        if(root->val==0){

            return false;

        }

        else{

            return true;

        }

    }

};
```

第一次用python写递归发现python的类内方法访问非常不同，要用到装饰器而且似乎不大好用

```python
class Solution:

    def evaluateTree(self, root: Optional[TreeNode]) -> bool:

        if root.left is None:

            return root.val == 1

        if root.val == 2:

            return self.evaluateTree(root.left) or self.evaluateTree(root.right)

        return self.evaluateTree(root.left) and self.evaluateTree(root.right)
```

第一次用js写题也是看了半天前面注释的类型
似乎LeetCode中直接用function作为对象使用
定义的意思是用三元表达式来防止空树
这或许就是js的undefined和null的区别吧

undefined表示未定义，在这里表示一种行为，而left和right属性未来要表示对象所以应该用三元表达式进行区分

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var evaluateTree = function(root) {
    if(!root.left){
        return root.val===1;
    }
    if(root.val===2){
        return evaluateTree(root.left)||evaluateTree(root.right);
    }
    else{
        return evaluateTree(root.left)&&evaluateTree(root.right);
    }
    
};
```