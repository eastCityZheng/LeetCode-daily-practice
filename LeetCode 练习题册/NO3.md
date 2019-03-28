# 3. 无重复字符的最长子串 python medium

### 知识点

hash table

### 题目

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

#### 示例 

输入: "abcabcbb"  
输出: 3   
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

输入: "bbbbb"  
输出: 1  
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
	 
#### 代码
```
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        hash_table = {}
        idx , res = 0,0
        for i in range(len(s)):
            if s[i] in hash_table:
                idx = max(hash_table[s[i]],idx)
            res = max (res ,i-idx+1)
            hash_table[s[i]] = i+1
        return res 
```
