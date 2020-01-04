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
**:exclamation: - Note that intervals [1, 2] and [2, 3] are considered an overlap**

## Approach :

### Implementation

```java
public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> merged = new ArrayList<int[]>();
        for(int[] interval : intervals) {
        	if(interval[1] < newInterval[0]) {
        		merged.add(interval);
        	} else if(newInterval[1] < interval[0]) {
        		merged.add(newInterval);
        		newInterval = interval;
        	} else {
        		newInterval[0] = Math.min(newInterval[0], interval[0]);
        		newInterval[1] = Math.max(newInterval[1], interval[1]);
        	}
        }
        
    merged.add(newInterval);
    return merged.toArray(new int[merged.size()][]);
}
```
