# Insert interval
## https://leetcode.com/problems/insert-interval

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.
```
Example 1:

Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

Example 2:

Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

**:exclamation: Input intervals are already sorted according to their start times**

**:exclamation: Note that intervals [1, 2] and [2, 3] are considered an overlap**

## Approach :
#### Non Overlapping Scenarios
Below are three cases where the newInterval doesn't overlap with any of the intervals.
1. newInterval [5, 6] can be added after interval [3, 4]
2. newInterval [3, 4] will sit, in between [1, 2] and [5, 6]
3. newInterval [1, 2] will come before interval [3, 4]

![Insert Interval No Overlap Scenarios](insert-interval-no-overlap.PNG?raw=true "Insert Interval No Overlap Scenarios")

#### Overlapping Scenarios
newInterval can overlap with one or more than one intervals, as shown in example below.
![Insert Interval Overlap Scenarios](insert-interval-overlap.PNG?raw=true "Insert Interval Overlap Scenarios")

**So how to solve this problem :worried:**

Iterate over the sorted intervals and check the following conditions :

1. If the start time of `newInterval` is greater than the end time of the current Interval then it means, there is no overlap and current Interval comes before the `newInterval`. So we add the current Interval to output list.

2. Now if the above first condition is false, it means start time of the `newInterval` is less than or equal to end time of the current Interval. So we check if the end time of the `newInterval` is less than, start time of the current Interval, if thats the case, it means there is no overlap and `newInterval` comes before current Interval. So we first add `newInterval` to the output list and then we add the current Interval to the output list. And we set the `newInterval` to null since we inserted the `newInterval` to the output list. 

3. If both first and second checks are false, then we are sure that `newInterval` overlaps with current Interval. Since the `newInterval` overlaps, we update the start and end time of the `newInterval` as follow

 ```java 
 newInterval[0] = Math.min(newInterval[0], currentInterval[0])
 newInterval[1] = Math.max(newInterval[1], currentInterval[1])
 ```
 
### Implementation

```java
public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> merged = new ArrayList<int[]>();
        for(int[] interval : intervals) {
        	if(newInterval == null || interval[1] < newInterval[0]) {
        		merged.add(interval);
        	} else if(newInterval[1] < interval[0]) {
        		merged.add(newInterval);
        		merged.add(interval);
          newInterval = null;
        	} else {
        		newInterval[0] = Math.min(newInterval[0], interval[0]);
        		newInterval[1] = Math.max(newInterval[1], interval[1]);
        	}
        }
        
        if(newInterval != null)
            merged.add(newInterval);
        
        return merged.toArray(new int[merged.size()][]);
    }
```
