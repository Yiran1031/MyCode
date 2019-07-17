### Question 24 : Swap Nodes in Pairs
---

Given a linked list, swap every two adjacent nodes and return its head.

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

 

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```
**Solution : **

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
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode cur = head;
        ListNode pre = null;
        head = head.next;
        // ListNode nex = head.next;
        while(cur != null && cur.next != null)
        {
            ListNode temp = cur.next.next;
            cur.next.next =  cur;
            if(pre!=null)
                pre.next = cur.next;
            cur.next = temp;
            pre = cur;
            cur = cur.next;
        }
        return head;
    }
}
```

