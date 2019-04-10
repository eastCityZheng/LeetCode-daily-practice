# 6. Z 字形变换 python medium

### 知识点

字符串

### 题目

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。  
比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：  
```
L   C   I   R
E T O E S I I G
E   D   H   N
```
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。  
请你实现这个将字符串进行指定行数变换的函数：  
string convert(string s, int numRows);  

#### 示例 

输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"

输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:
```
L     D     R
E   O E   I I
E C   I H   N
T     S     G
```

#### 总结
i 为行数  a 为间隔  
找好规律 就能马上做出来 间隔 2n-2 第一行和最后一行除外 间隔中都有两个数 这两个数的间隔为 a-2*i

#### 代码
```
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        n = numRows
        a = 2*n-2
        l = len(s)
        ans = []
        if n == 1 :
            return s
        for i in range(n):
            cur =i
            if i == 0 or i == n-1:
                while(cur <l):
                    ans.append(s[cur])
                    cur +=a
            while (cur <l and cur+a-2*i<l):
                ans.append(s[cur])
                ans.append(s[cur+a-2*i])
                cur +=a
            if cur < l:
                ans.append(s[cur])
        return ''.join(ans)
```
