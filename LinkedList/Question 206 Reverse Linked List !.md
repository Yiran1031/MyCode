### Question 206: Reverse Linked List !
---

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?

**Solution : Iteratively**

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
    public ListNode reverseList(ListNode head) {
        if(head == null)
            return head;
        ListNode pre = null;
        ListNode nex = head.next;
        while(head != null && head.next!=null)
        {
            head.next = pre;
            pre = head;
            head = nex;
            nex = head.next;
        }
        head.next = pre;
        return head;
    }
}
```

**Solution : Recursively**

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
    public ListNode reverseList(ListNode head) {
        if(head == null)
            return null;
        head = rec(head);
        return head;
    }
    public ListNode rec(ListNode head)
    {
        if(head.next == null)
            return head;
        ListNode temp = rec(head.next);
        head.next.next = head;
        head.next = null;
        
        return temp;
    }
}
```

