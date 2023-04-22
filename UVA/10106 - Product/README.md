#[10106 - Product](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1047)
### `Adhoc` Problem
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
int isbigger(string n1, string n2)
{
    int z = 0;
    int c = 0;
    if (n1.length() == n2.length())
    {
        for (int i = 0; i < n1.length(); i++)
        {
            if (n1[i] == n2[i]) {
                c++;
                //continue;
            }
            else if (n1[i] > n2[i]) {
                z = 1;
                return z;
            }
            else if (n1[i] < n2[i]) {
                z = 2;
                return z;
            }
        }
        if (c == n1.length()) {
            z = 0;
            return z;
        }
    }
    else if (n1.length() > n2.length()) z = 1;
    else z = 2;
    return z;
}
string multiply(string n1, string n2)
{
    string res = "";
    vector<int> result(n1.length() + n2.length(), 0);
    int carry = 0, value = 0, mult = 0;
    if (isbigger(n1, n2) == 2)
    {
        swap(n1, n2); // to make n1 is always bigger
    }
    int x = n1.length() - 1; // last index of n1
    int y = n2.length() - 1; // last index of n2

    int index1 = 0;
    int index2 = 0;

    for (int i = y; i >= 0; i--)
    {
        index1 = 0;
        for (int j = x; j >= 0; j--)
        {
            mult = ((n2[i] - '0') * (n1[j] - '0')) + carry + result[index1 + index2];
            value = mult % 10;
            carry = mult / 10;
            result[index1 + index2] = value;
            index1++;
        }
        if (carry)
        {
            result[index1 + index2] += carry;
        }
        index2++;
        carry = 0;
        value = 0;
    }
    for (int i = result.size() - 1; i >= 0; i--)
    {
        res += to_string(result[i]);
    }
    int c = 0;
    for (int i = 0; i < res.length(); i++)
    {
        if (res[i] == '0') c++;
        else break;
    }
    res = res.substr(c);
    return res;
}
int main()
{
    string n1 ,n2;
    while(cin >> n1){
        cin >> n2;
        if (n1 == "0" || n2 == "0")
            cout << '0' << endl;
        else
            cout << multiply(n1 ,n2) << endl;
    }
}

```