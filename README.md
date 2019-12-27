# Insert interval


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
