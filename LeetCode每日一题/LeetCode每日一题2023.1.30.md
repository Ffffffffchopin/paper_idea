
![[Pasted image 20230130124856.png]]


没有什么技巧，直接简单模拟即可。

先用一个一个临时变量指针找到a的位置，再用另一个临时变量找到b，再用第三个临时变量找到List2的末尾接上即可。

  

```c++
/**

 * Definition for singly-linked list.

 * struct ListNode {

 *     int val;

 *     ListNode *next;

 *     ListNode() : val(0), next(nullptr) {}

 *     ListNode(int x) : val(x), next(nullptr) {}

 *     ListNode(int x, ListNode *next) : val(x), next(next) {}

 * };

 */

class Solution {

public:

    ListNode* mergeInBetween(ListNode* list1, int a, int b, ListNode* list2) {

        ListNode* tmp_a=list1;

        for(int i=0;i<a-1;i++){

            tmp_a=tmp_a->next;

        }

        ListNode* tmp_b=tmp_a->next;

        for(int i=a;i<=b;i++){

            tmp_b=tmp_b->next;

        }

        tmp_a->next=list2;

        ListNode* tmp_2=list2;

        while(tmp_2->next!=nullptr){

            tmp_2=tmp_2->next;

        }

        tmp_2->next=tmp_b;

        return list1;

  

    }

};

```
