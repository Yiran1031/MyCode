### Question 86 : Partition List
---

Given a linked list and a value *x*, partition it such that all nodes less than *x* come before nodes greater than or equal to *x*.

You should preserve the original relative order of the nodes in each of the two partitions.

**Example:**

```java
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```



**Solution : **

1. Divide list to 2 part, one is less than target and another one is greater or equal than target.

2. merge 2 list and return head.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode minList = new ListNode(-1);
        ListNode maxList = new ListNode(-1);
        
        ListNode minh = minList;
        ListNode maxh = maxList;
        
        while(head != null)
        {
            if(head.val >= x)
            {
                maxList.next = head;
                maxList = maxList.next;
                head = head.next;
                maxList.next = null;
            }else if(head.val < x)
            {
                minList.next = head;
                minList = minList.next;
                head = head.next;
                minList.next = null;
            }
        }
        
        minList.next = maxh.next;
        maxh = null;
        return minh.next;
    }
}
```

