Merge Intervals Problem 

Given an array of intervals where each interval is represented as [start, end], merge all overlapping intervals.

Return an array containing the non-overlapping intervals that cover all the intervals in the input.

Example Input: [[1,3], [2,6], [8,10], [9,12]] Output [[1,6], [8,12]] 

The intervals [1,3] and [2,6] overlap, so they are merged into [1,6].

Similarly, [8,10] and [9,12] are merged into [8,12].

Approach 

The key observation is that intervals become easy to merge after sorting them by their start position.

For each interval:

If it does not overlap with the last merged interval, add it to the result. Otherwise, extend the end of the last merged interval. 

Two intervals overlap when:

current_start <= previous_end 

When they overlap, the merged end is:

max(previous_end, current_end) Algorithm Sort all intervals by their starting position. Initialize an empty result list. Iterate through the sorted intervals. If the result is empty or the current interval does not overlap with the last interval: Add the current interval. Otherwise: Update the end of the last interval. Return the merged intervals. Python Implementation def merge_intervals(intervals): if not intervals: return [] intervals.sort(key=lambda interval: interval[0]) merged = [intervals[0]] for start, end in intervals[1:]: last_start, last_end = merged[-1] if start <= last_end: merged[-1][1] = max(last_end, end) else: merged.append([start, end]) return merged Complexity 

Let n be the number of intervals.

Sorting takes:

O(n log n) 

The merging pass takes:

O(n) 

Therefore, the overall complexity is:

Time: O(n log n) Space: O(n) for the output and sorting-related storage. Example Walkthrough 

Consider:

[[1,4], [2,5], [7,9], [8,10]] 

After sorting:

[[1,4], [2,5], [7,9], [8,10]] 

Start with:

[1,4] 

The next interval is [2,5].

Since:

2 <= 4 

they overlap:

[1,5] 

Next is [7,9].

Since:

7 > 5 

there is no overlap:

[[1,5], [7,9]] 

Finally, [8,10] overlaps with [7,9]:

[[1,5], [7,10]] Key Insight 

The most important step is sorting by the start position.

Once the intervals are sorted, we only need to compare each interval with the most recently merged interval.

Without sorting, determining which intervals can overlap would require significantly more comparisons.

This pattern appears frequently in scheduling, range processing, calendar systems, and resource allocation problems.


