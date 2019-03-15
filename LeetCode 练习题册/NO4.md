# 4. 寻找两个有序数组的中位数  python hard

### 知识点

。。

### 题目

给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

#### 示例 

nums1 = [1, 3]  
nums2 = [2]  

则中位数是 2.0

nums1 = [1, 2]  
nums2 = [3, 4]  

则中位数是 (2 + 3)/2 = 2.5

#### 代码
```
class Solution(object): 
    def findMedianSortedArrays(self, nums1, nums2):
          
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        nums = nums1 +nums2
        nums = sorted(nums)
        medium = len(nums)/2
        if len(nums)%2 :
            return nums[medium]
        else:
            return (nums[medium]+nums[medium-1])/2.0
        
```
