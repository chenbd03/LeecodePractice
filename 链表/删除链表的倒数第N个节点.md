## 删除链表的倒数第N个节点

【题目来源】https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

示例1：

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]

示例 2：
输入：head = [1], n = 1
输出：[]

示例 3：
输入：head = [1,2], n = 1
输出：[1]

【解题思路】这道题直接用双指针方式去解决最直接！先让快指针先走n步，然后再同步一起走，细节就是要判断一些边界条件

```c
struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
    if (head->next == NULL && n==1){ //表示只有一个节点
        return NULL;
    }
    int len = 1;
    int n_copy = n;
    struct ListNode* slow = head;
    struct ListNode* fast = head;
    while(fast->next != NULL){   //这里判断条件是快指针的下一指针是否为空,便于下面删除操作
        fast=fast->next;
        len++;
        if (n>0){  // 这里表示只让快指针先走n步,
            n--;
        }else{  //当n为0,则就跟快指针同步走,
            slow = slow->next;
        }
    }
    if (n_copy==len){  //若要删除得倒数第n步刚好是链表长度,直接返回head的下一指针
        return head->next;
    }
    // 删除常规操作
    struct ListNode* temp = slow->next;
    slow->next = temp->next;
    free(temp);
    return head;
}
```

