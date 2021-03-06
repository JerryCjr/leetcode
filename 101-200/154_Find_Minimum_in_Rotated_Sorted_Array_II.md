### 154. Find Minimum in Rotated Sorted Array II

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element.

The array may contain duplicates.

**Example 1:**
```
Input: [1,3,5]
Output: 1
```

**Example 2:**
```
Input: [2,2,2,0,1]
Output: 0
```

**Note:**
- This is a follow up problem to Find Minimum in Rotated Sorted Array.
- Would allow duplicates affect the run-time complexity? How and why?

**Solution**
```Python
class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return -1
        
        start = 0
        end = len(nums) - 1

        while start + 1 < end:
            mid = start + (end - start) / 2
            if nums[mid] == nums[end]:
                if mid != end:
                    end -= 1
            elif nums[mid] < nums[end]:
                end = mid
            else:
                start = mid

        if nums[start] < nums[end]:
            return nums[start]
        
        return nums[end]
```