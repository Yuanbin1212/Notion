# std::numeric_limits

Last edited time: May 4, 2023 2:04 PM
Level: 二级标题
Owner: 我叫袁小陌
Tags: C++

Defined in header `[<limits>](https://en.cppreference.com/w/cpp/header/limits)`

### **std::numeric_limits<T>::epsilon**

功能：返回机器 epsilon ，即 1.0 与浮点类型 `T`的下个可表示值的差。它仅当 [std::numeric_limits](https://www.apiref.com/cpp-zh/cpp/types/numeric_limits.html)<T>::is_integer == false 才有意义。

| T | std::numeric_limits<T>::epsilon() |
| --- | --- |
| bool | false |
| float | FLT_EPSILON |
| double | DBL_EPSILON |
| long double | LDBL_EPSILON |

```cpp
#include <stdio.h>
#include <iostream> //include cout
#include <iomanip> //include setprecision
#include <cmath>
#include <type_traits> //include enable_if
#include <limits> //include numeric_limits

template<class T>
typename std::enable_if<!std::numeric_limits<T>::is_integer, bool>::type almost_equal(T x, T y){
    return std::fabs(x-y) <= std::numeric_limits<T>::epsilon();
}

int main()
{
    double d1 = 0.2;
    double d2 = 1/sqrt(5)/sqrt(5);
    std::cout << std::fixed << std::setprecision(20) 
        << "d1=" << d1 << "\nd2=" << d2 << '\n';
    
    if(d1 == d2){
        printf("d1 == d2\n");
    }else{
        printf("d1 != d2\n");
    }

    if(almost_equal(d1, d2)){
        printf("d1 almost equals d2\n");
    }else{
        printf("d1 does not almost equal d2\n");
    }
    
    return 0;
}
```