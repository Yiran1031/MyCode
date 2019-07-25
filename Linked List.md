### Linked List

**Merge two Sorted List**

```java
//Iteration
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(-1);
        ListNode t = head;
        ListNode node1 = l1;
        ListNode node2 = l2;
        while(l1 != null && l2 != null)
        {
            if(l1.val <= l2.val)
            {
                t.next = l1;
                l1 = l1.next;
            }else if(l1.val > l2.val){
                t.next = l2;
                l2 = l2.next;
            }
            t = t.next;
        }
        
        if(l1 != null)
            t.next = l1;
        else if(l2 != null)
            t.next = l2;
        
        return head.next;
    }
}
```

---

**Delete a node by a specific value**

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
    public ListNode removeElements(ListNode head, int val) {
        ListNode temp = null;
        //remove the target at head
        while(head != null && head.val == val ) head = head.next;
        temp = head;
        while(temp != null && temp.next != null)
        {
            
            if(temp.next.val == val)
            {
                temp.next = temp.next.next;
                //temp = temp.next; do not move reference !
            }else
                temp = temp.next;
        }
        
        return head;
    }
}
```

