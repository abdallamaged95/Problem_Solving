# [10110 - Light, more light](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1051)
### `Number Theory` Problem
# Solution
```cpp
#include <iostream>
#include <algorithm>
#include <deque>
#include <string>
#include <vector>
#include <set>
#include <math.h>
// #include "StackArr.cpp"
using namespace std;

int main()
{
    unsigned int n;
    while (cin >> n){
        if (n == 0) return 0;
        if (n == 1){
            cout << "yes\n";
            continue;
        }
        double x = sqrt(n);
        unsigned int y = trunc(x);
        if (y == x){
            cout << "yes\n";
            continue;
        }
        else cout << "no\n";
    }
}


```