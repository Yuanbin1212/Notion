# algorithm

Last edited time: May 4, 2023 2:04 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: C++

## unique函数可以删除有序数组中的重复元素

- 这里的删除不是真的delete，而是**重复元素的位置被不重复的元素给占领了**
- unique函数的返回值是去重之后的尾地址
- 一定要先对数组进行排序才可以使用unique函数

```cpp
//iterator unique(iterator it_1,iterator it_2);
//表示对容器中[it_1，it_2)范围的元素进行去重(注：区间是前闭后开，即不包含it_2所指的元素)
//返回值是一个迭代器，它指向的是去重后容器中不重复序列的最后一个元素的下一个元素

#include <stdio.h>
#include <vector>
#include <algorithm> //unique
#include <iostream> //cout

int main()
{
    std::vector<int> nums = {2,3,3,5,5,9,10,10};
    //两个迭代器相减得到的是这两个迭代器的距离
    std::cout << "原本vector的长度是" <<nums.end() - nums.begin() << std::endl;
    
    size_t res = unique(nums.begin(), nums.end()) - nums.begin();
    std::cout <<"去重后vector的长度是"<< res << std::endl;
    
    for(int&val : nums){
        std::cout << val << std::endl;
    }
    
}

// 原本vector的长度是 8
// 去重后vector的长度是 5
// 2 3 5 9 10 9 10 10 
```