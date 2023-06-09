# std::vector

Last edited time: May 4, 2023 3:21 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: C++

```cpp

vector<T> v; 默认构造
vector(v.begin(),v.end());  将v.begin，end()区间中的元素拷贝给本身
vector(n,elem); 构造函数将n个elem拷贝给本身
vector(const vector &vec); 拷贝构造函数
```

| 访问元素 |  |
| --- | --- |
| at | access specified element with bounds checking（校验索引） |
| operator[] | access specified element（存在索引越界） |
| front | access the first element |
| back | access the last element |
| data | direct access to the underlying array（返回一个指向数组中第一个元素的指针） |

```cpp
#include <iostream>
#include <vector>

int main()
{
    std::vector<char> letters = {'h', 'e', 'l', 'l', 'o'};
    std::cout << "The first letter is(using front): "<< letters.front() << std::endl;
    std::cout << "The second letter is(using at): "<< letters.at(1) << std::endl;
    std::cout << "The third letter is(using []): "<< letters[2] << std::endl;
    std::cout << "when index out of bounds with at: "<< letters.at(6) << std::endl;
    std::cout << "when index out of bounds with []: "<< letters[6] << std::endl;
}

// 输出
The first letter is(using front): h
The second letter is(using at): e
The third letter is(using []): l
terminate called after throwing an instance of 'std::out_of_range'
  what():  vector::_M_range_check: __n (which is 6) >= this->size() (which is 5)
when index out of bounds with []:
```

| 迭代器 | (c* 读出的的const_iterator，只可读不可写) |
| --- | --- |
| begin
cbegin(C++11) | returns an iterator to the beginning
(如果vector是空的，vector.begin() == vector.end() ) |
| end
cend(C++11) | returns an iterator to the en |
| rbegin
crbegin(C++11) | returns a reverse iterator to the beginning |
| rend
crend(C++11) | returns a reverse iterator to the end |

![2021020114132174.jpeg](std%20vector%204022ab624ddc4ea9bf02187b10f9c1ed/2021020114132174.jpeg)

```cpp
#include <iostream>
#include <vector>

int main()
{
    std::vector<char> letters = {'h', 'e', 'l', 'l', 'o'};
    std::vector<char> isempty;
    std::cout << "The first letter is(using front): "<< *letters.begin() << std::endl;
    if(isempty.begin()==isempty.end()){
        std::cout << "The isempty is indeed empty(isempty.begin()==isempty.end() is true) "<< std::endl;
    }
}
```

| Capacity |  |
| --- | --- |
| empty | checks whether the container is empty |
| size | returns the number of elements |
| max_size | returns the maximum possible number of elements |
| reserve | reserves storage |
| capacity | returns the number of elements that can be held in currently allocated storage（内存用完之后，会重新分配一部分空间，至于大小不同的库实现也不同） |
| shrink_to_fit(C++11) | reduces memory usage by freeing unused memory（收缩到合适） |

| Modifiers |  |
| --- | --- |
| clear | clears the contents（保持向量的capacity（）不变） |
| insert | inserts elements |
| emplace(C++11) | constructs element in-place |
| erase | erases elements |
| push_back | adds an element to the end |
| emplace_back(C++11) | constructs an element in-place at the end |
| pop_back | removes the last element |
| resize | changes the number of elements stored |
| swap | swaps the contents |

```cpp
#include <iostream>
#include <vector>
#include <iomanip>

int main()
{
    std::vector<int> nums = {2, 4, 6, 8} ;
    std::cout << "nums contains " << nums.size() << " element" <<std::endl;
    std::cout << "nums's capacity is " << nums.capacity() <<std::endl;
    
    std::vector<int> v;
    int sz = 100;
    auto cap = v.capacity();
    std::cout << "Initial v's size is " << v.size() 
              << " and capacity is " << v.capacity() << std::endl;
    
    std::cout << "\nDemonstrate the capacity's growth policy."
                 "\nSize:  Capacity:  Ratio:\n" << std::left;
    while (sz-- > 0) {
        // v.push_back(sz);
        v.emplace_back(sz);
        if (cap != v.capacity()){
            std::cout << std::setw(7) << v.size()
                      << std::setw(11) << v.capacity()
                      << std::setw(10) << v.capacity() / static_cast<float>(cap) 
                      << '\n';
            cap = v.capacity();
        }
    }
    
    std::cout << "\nFinal size: " << v.size() << ", capacity: " << v.capacity() 
    << '\n';
}

nums contains 4 element
nums's capacity is 4
Initial v's size is 0 and capacity is 0

Demonstrate the capacity's growth policy.
Size:  Capacity:  Ratio:
1      1          inf       
2      2          2         
3      4          2         
5      8          2         
9      16         2         
17     32         2         
33     64         2         
65     128        2         

Final size: 100, capacity: 128 
```