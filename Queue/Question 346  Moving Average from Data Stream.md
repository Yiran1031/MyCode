### Question 346 : Moving Average from Data Stream
---

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

**Example:**

```java
MovingAverage m = new MovingAverage(3);
m.next(1) = 1
m.next(10) = (1 + 10) / 2
m.next(3) = (1 + 10 + 3) / 3
m.next(5) = (10 + 3 + 5) / 3
```

**Solution : **

```java
class MovingAverage {
    int len;
    double sum;
    int num;
    Queue<Double> q = new LinkedList<Double>(); 
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        len = size;
        sum = 0;
        num = 0;
    }
    
    public double next(int val) {
        if(num < len)
        {
            sum = sum + val;
            q.offer(Double.valueOf(val));
            num++;
        }else
        {
            sum = sum - q.poll();
            sum = sum + val;
            q.offer(Double.valueOf(val));
        }
        
        return sum/num;
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```

