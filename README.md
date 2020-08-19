# 【Leetcode】TASK 01: 分治
## 1.主要思想  
分治算法的主要思想是将原问题递归地分成若干个子问题，直到子问题满足边界条件，停止递归。将子问题逐个击破（一般是同种方法），将已经解决的子问题合并，最后，算法会层层合并得到原问题的答案。<br>
## 2.分治算法步骤  
分：递归地将问题分解为各个子问题（性质相同的、相互独立的子问题）；<br>
治：将这些规模更小的子问题逐个击破；<br>
合：将已解决的子问题逐层合并，最终得出原问题的解。<br>
## 3.分治算法适用场合
1.原问题的计算复杂度随着问题的规模的增加而增加。<br>
2.原问题能够被分解为更小的子问题。<br>
3.子问题的结构和性质与原问题一样，并且相互独立，子问题之间不包含公共的子子问题。<br>
4.原问题分解出的子问题的解可以合并为该问题的解。<br>
## 4.分治算法解题模版（pseudo code）
```PYTHON
def divide_conquer(problem,param1,param2,...):
    #不断切分的终止条件
    if problem is None:
        print_result
        return
    #准备数据
    data=prepare_data(problem)
    #将大问题拆分为小问题
    subproblems=split_problem(problem,data)
    #处理小问题，得到子结果
    subresult1=self.divide_conquer(subproblems[0],p1,...)
    subresult2=self.divide_conquer(subproblems[1],p1,...)
    subresult3=self.divide_conquer(subproblems[2],p1,...)
    #对子结果进行合并 得到最终结果
    result=process_result(subresult1,subresult2,subresult3,...)
  ```
  ## 5.Leetcode练习
  ### 5.1 Leetcode 169.多数元素<br>
  1.题目描述<br>
给定一个大小为n的数组，找到其中的众数。众数是指在数组中出现的次数大于【n/2】的元素。<br>
2.套用模版<br>
```PYTHON
class solution(object):
    def majorityElement(self,nums):
        #不断切分的终止条件
        if not nums:
            return None
        if len(nums)==1:
            return nums[0]
        #准备数据，并将大问题拆分为小问题
        left=self.majorityElement(nums[:len(nums)//2])
        right=self.majorityElement(nums[len(nums)//2:])
        #处理子问题，得到子结果
        #对子结果进行合并，得到最终结果
        if left == right:
            return left
        if nums.count(left)>nums.count(right):
            return left
        else:
            return right
```
### 5.2 Leetcode 53.最大子序和
1.题目描述<br>
给定一个整数数组nums，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。<br>
2.套用模版<br>
```PYTHON
class Solution(object):
    def maxSubArray(self,nums):
        #确定不断切分的终止条件
        n=len(nums)
        if n==1:
            return nums[0]
        #准备数据，并将大问题拆分为小问题
        left=self.maxSubArray(nums[:len(nums)//2])
        right=self.maxSubArray(nums[len(nums)//2:])

        #处理小问题，得到子结果
        #从右到左计算左边的最大子序和
        max_l=nums[len(nums)//2-1]#该组最右边的元素
        tmp=0 #用来记录连续子数组的和

        for i in range(len(nums)//2-1,-1,-1):#从右到左遍历数组的元素
            tmp+=nums[i]
            max_l=max(tmp,max_l)

        #从左到右计算右边的最大子序和
        max_r=nums[len(nums)//2]
        tmp=0
        for i in range(len(nums)//2,len(nums)):
            tmp+=nums[i]
            max_r=max(tmp,max_r)

        return max(left,right,max_l+max_r)
```
### 5.3 Leetcode 50. Pow(x,n)
1.实现 pow（x,n），即计算x的n次幂函数。<br>
2.套用模版<br>
```PYTHON
class Solution(object):
    def myPow(self,x,n):
        if n <0:
            x=1/x
            n=-n

        if n == 0:
            return 1

        if n%2 == 1:
            p= x*self.myPow(x,n-1)
            return p

        return self.myPow(x*x,n/2)
```

  


