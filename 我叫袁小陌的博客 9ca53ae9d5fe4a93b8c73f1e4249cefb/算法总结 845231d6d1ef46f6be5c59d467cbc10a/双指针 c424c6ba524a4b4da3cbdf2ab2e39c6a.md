# 双指针

Last edited time: May 4, 2023 2:03 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: 算法

双指针法（快慢指针法）： **通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。**

定义快慢指针

- 快指针：**寻找新数组的元素** ，新数组就是不含有目标元素的数组
- 慢指针：**指向更新 新数组下标的位置**

[27. 移除元素 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-element/submissions/)

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 **原地** 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

假设不在原数组上修改

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        right = 0
        left = 0
        result = [0] * len(nums)
        while right < len(nums):
            if nums[right] != val:
                result[left] = nums[right]
                left += 1
            right += 1
        print(result)
```

![Untitled](%E5%8F%8C%E6%8C%87%E9%92%88%20c424c6ba524a4b4da3cbdf2ab2e39c6a/Untitled.png)

然后更改为在原数组上修改

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
       left = right = 0
        while right < len(nums):
            if nums[right] != val:
                #每一次的移动都是在复制值到新的数组中，只是是在原本数组的基础上修改
                nums[left] = nums[right]
                left += 1
						# 当 right 指针遇到要删除的元素时停止赋值left 指针停止移动, fast 指针继续前进
            right +=1
        return left
```

[977. 有序数组的平方 - 力扣（LeetCode）](https://leetcode.cn/problems/squares-of-a-sorted-array/)

给你一个按 **非递减顺序**排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序**排序

```python
#**时间复杂度为O(n + nlogn)**
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        return sorted([pow(num, 2) for num in nums])

#**时间复杂度为O(n)**
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        size = len(nums) - 1 
        result = [0] * len(nums)
        left, right = 0, size
        while left <= right:
            if nums[left]  * nums[left] > nums[right] * nums[right]:
                result[size] = nums[left] * nums[left]
                left += 1
            else:
                result[size] = nums[right] * nums[right]
                right -= 1
            size -= 1
        return result
```

[209. 长度最小的子数组 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-size-subarray-sum/)

暴力破解法

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        sum = 0
        lenth = 10**6
        for i in range(len(nums)):
            sum = 0
            for j in range(i, len(nums)):
                sum += nums[j]
                if sum >= target:
                    lenth = min(lenth, j - i + 1)
                    break
        if lenth == 10**6:
            return 0            
        return lenth
```

双指针之**滑动窗口**

所谓滑动窗口，**就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果**

![Untitled](%E5%8F%8C%E6%8C%87%E9%92%88%20c424c6ba524a4b4da3cbdf2ab2e39c6a/Untitled%201.png)

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        sum = 0
        left = 0
				#定义无穷大与无穷小
				#_max = float("inf")
				#_min = float("-inf")
        lenth = float("inf")
        for right in range(len(nums)):
            sum += nums[right]
            while sum >= target:
                lenth = min(lenth, right - left + 1)
                sum -= nums[left]
                left += 1
        return 0 if lenth == float("inf") else lenth
```

### 双指针之快慢指针

快慢指针指的是两个步调不一样的指针，**快指针一次遍历两个节点，慢指针一次遍历一个节点**。

快慢指针主要有三大类应用场景：

- **找到链表的中点。**
- **判断链表中是否存在环。**
- **查找或删除链表（线性表）的某个节点。**

[202. 快乐数 - 力扣（Leetcode）](https://leetcode.cn/problems/happy-number/description/)

```cpp
class Solution {
public:
    bool isHappy(int n) {
        //快慢指针法
        int slow = n;
        int fast = GetNextNum(n);
        while(fast !=1 and slow != fast){
            slow = GetNextNum(slow);
            fast = GetNextNum(GetNextNum(fast));
        }

    return fast == 1;
    }

    int GetNextNum(int n) {
        int64_t sum = 0;
        while(n > 0){
            sum += pow(n % 10, 2);
            n /= 10;
        }
        return sum;
    }

};
```