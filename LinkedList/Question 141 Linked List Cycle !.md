### Question 141: Linked List Cycle !
---

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

 

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**Follow up:**

Can you solve it using *O(1)* (i.e. constant) memory?



**Solution1 : Hash Table**

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        Set<ListNode> nodesSeen = new HashSet<>();
        if(head == null)
            return false;
        while(head != null)
        {
            if(nodesSeen.contains(head))
            {
                return true;
            }else
            {
               nodesSeen.add(head);
            }
            head = head.next;
        }  
        return false;
    }
}
```

**Complexity analysis :**

- Time complexity : O(n). We visit each of the n elements in the list at most once. Adding a node to the hash table costs only O(1) time.
- Space complexity: O(n). The space depends on the number of elements added to the hash table, which contains at most n elements. 

---

**Solution 2: Two Pointers**

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null)
            return false;
        ListNode fast = head.next;
        ListNode slow = head;
        while(fast != null && fast.next != null)
        {
            if(fast == slow)
            {
                return true;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        return false;
    }
}
```

**Complexity analysis : **

- Time complexity : O(n). Let us denote n as the total number of nodes in the linked list. To analyze its time complexity, we consider the following two cases separately.
  - ***List has no cycle:***
    The fast pointer reaches the end first and the run time depends on the list's length, which is O(n).
    
  - ***List has a cycle:***
  
    O(N+K) which k is the length of the cycle;
- Space complexity : O(1). We only use two nodes (slow and fast) so the space complexity is O(1).