# [Recursive Queries - 932B](https://codeforces.com/contest/932/problem/B)
### `Partial Sum` Problem
# Solution
```cpp
#include <bits/stdc++.h>
// #include "Functions.h"
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define vprint(v) for(auto it : v) { cout << it << ' ';} cout << "\n"
#define mprint(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n"
using namespace std;
int l ,r ,k;
vector<int> sols(1000002);
vector<vector<int>> partial(9 ,vector<int>(1000002));
int solve(int n)
{
    while (n >= 10){
        int mult = 1;
        while (n > 0){
            int dig = n % 10;
            if (dig != 0)
                mult *= dig;
            n /= 10;
        }
        n = mult;
    }
    return n;
}
int main()
{
    IamVengeance;
    for (int i = 1 ; i <= 1000000 ; i++){
        sols[i] = solve(i);
        partial[sols[i]-1][i]++;
        partial[sols[i]-1][1000001]--;
    }
    for (int i = 0 ; i < 9 ; i++){
        for (int j = 2 ; j <= 1000001 ; j++){
            partial[i][j] += partial[i][j-1];
        }
    }
    int tt = 1; 
    // cin >> tt;
    while (tt--)
    {
        int q; cin >> q;
        while (q--){
            cin >> l >> r >> k;
            int cnt = partial[k-1][r] - partial[k-1][l-1];
            cout << cnt << '\n';
        }
    }
    

    return 0;
}
```
