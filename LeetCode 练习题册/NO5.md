# 5. 最长回文子串 python medium

### 知识点

Manacher 算法

### 题目

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

#### 示例 

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。

输入: "cbbd"
输出: "bb"

#### 总结
第一步：将字符串中用未出现的字符间隔起来 一般用#这样可以巧妙地解决奇偶的问题
例如：  
s：a  a  b  a  b  b  a  
s_new: #  a  #  a  #  b  #  a  #  b  #  b  #  a  #  
 
 第二步：  
 根据s_new求出每个字符为中心到最右端回文的距离  
 s_new :#  a  #  a  #  b  #  a  #  b  #  b  #  a  #  
 len :  1  2  3  2  1  4  1  4  1  2  5  2  1  2  1  
 
 第三步：  
 遍历s_new数组，i为当前遍历到的位置，即求解以S_new[i]为中心的最长回文子串的Len[i]  
 一共图中三种情况，sub_midd是当前i之前最右端的回文长度最长的中心位置。sub_side和2sub_midd-sub_side分别是sub_midd的右端和左端
 j 为i以sub_midd对称的位置。2Len[i]-1为i的对称长度。
 
 ![avatar](https://github.com/eastCityZheng/LeetCode-daily-practice/blob/master/imgs/NO5_1.png)
 当Len[j] < sub_side-i 说明以s_new[i]为中心的最长回文串未超出，因为以sub_midd对称 所以Len[j]=Len[i]
 
 ![avatar](https://github.com/eastCityZheng/LeetCode-daily-practice/blob/master/imgs/NO5_2.png)
 当Len[j] >= sub_side-i 说明以s_new[i]为中心的最长回文串超出了sub_side 所以要从sub_side开始匹配
 
 ![avatar](https://github.com/eastCityZheng/LeetCode-daily-practice/blob/master/imgs/NO5_3.png)
 当sub_side<i 则 i 只能老老实实从最旁边的开始匹配了
 
#### 代码
```
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        s = '#'.join(s)
        s = '#'+s+'#'
        lens = len(s) 
        f = [] # 辅助列表：f[i]表示i作中心的最长回文子串的长度 
        maxj = 0 # 记录对i右边影响最大的字符位置j 
        maxl = 0 # 记录j影响范围的右边界 
        maxd = (0,0) # 记录最长的回文子串长度 
        for i in range(lens): # 遍历字符串 
            if maxl > i: 
                count = min(maxl-i, int(f[2*maxj-i]/2)+1) # 这里为了方便后续计算使用count，其表示当前字符到其影响范围的右边界的距离 
            else : 
                count = 1 
            while i-count >= 0 and i+count < lens and s[i-count] == s[i+count]: # 两边扩展 
                count += 1 
            if(i-1+count) > maxl: # 更新影响范围最大的字符j及其右边界 
                maxl, maxj = i-1+count, i 
            f.append(count*2-1) 
            maxd = max(maxd, (f[i],i)) # 更新回文子串中心位置 和 长度
        return s[maxd[1]-maxd[0]/2:maxd[1]+maxd[0]/2].replace('#','')

```
