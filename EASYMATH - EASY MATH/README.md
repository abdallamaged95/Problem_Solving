# [EASYMATH - EASY MATH](https://www.spoj.com/problems/EASYMATH/)
### `Math` Problem
# Solution
```cpp

#include <bits/stdc++.h>
// #include "Functions.h"
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define vprint(v) for(auto it : v) { cout << it << ' ';} cout << "\n";
#define mprint(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n";
using namespace std;
 
//bool sortbysec(const pair<int,int> &a,
//              const pair<int,int> &b)
//{
//    return (a.second < b.second);
//}
ll GCD(ll a ,ll b)
{
    if (b == 0)
        return a;
    return GCD(b ,a%b);
}
ll LCM(ll a ,ll b)
{
    return (a*b)/GCD(a,b);
}
vector<ll> arr;
 ll divisors(ll sum ,ll index=0 ,ll cnt=0 ,ll digit=1)
 {
     if (index < arr.size() && arr[index] == 0)
         index++;    // Skip element ,can't divide by zero
 
     if (index == arr.size())
     {
         if (cnt == 0)
             return 0;
         if (cnt % 2 == 0)
             return -1 * (sum / digit);
         return (sum / digit);
     }
     return divisors(sum,index+1 ,cnt+1 ,LCM(arr[index] ,digit)) + divisors(sum ,index+1 ,cnt ,digit);
 }
 
int main()
{
    IamVengeance;
    int tt = 1;
    cin >> tt;
    while (tt--)
    {
        ll n ,m ,a ,b;
        cin >> n >> m >> a >> b;
        arr = {a ,a+b ,a+(2*b) ,a+(3*b) ,a+(4*b)};
        ll res1 = m - divisors(m);
        ll res2 = (n-1) - divisors(n-1);
        cout << res1 - res2 << endl;
    }
} 

```