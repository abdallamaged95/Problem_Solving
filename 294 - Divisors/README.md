# [294 - Divisors](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=230)
### `Number Theory` Problem
# Solution
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define V vector
#define st first
#define nd second
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define v_print(v) for(auto it : v) { cout << it << ' '; } cout << '\n'
#define m_print(m) for(auto it : m) { cout << it.st << " : " << it.nd << '\n'; } cout << '\n'
#define p_add(x ,y) make_pair(x.st + y.st ,x.nd + y.nd)
#define p_mult(x ,y) make_pair(x.st * y.st ,x.nd * y.nd)
#define precision(n,m) fixed << setprecision(m) << n
V<int> primes;
void Initialize()
{
    primes.clear();
    V<bool> valid(1e5, true);
    valid[0] = valid[1] = false;
    for (int i = 2; i*i <= valid.size(); i++)
        for (int j = i+i; j < valid.size(); j+=i)
            valid[j] = false;

    for (int i = 0; i < valid.size(); i++) if (valid[i])
        primes.push_back(i);
}
int Divs(int n)
{
    V<int> tmp;
    for (int i = 0; primes[i]*primes[i] <= n; i++)
    {
        if (n % primes[i] == 0)
            tmp.push_back(0);
        while (n % primes[i] == 0)
            n /= primes[i], tmp[tmp.size()-1]++;
    }
    if (n > 1)
        tmp.push_back(1);
//    v_print(tmp);
    int divs = 1;
    for (int i : tmp)
        divs *= i+1;
    return divs;
}
void solve()
{
    int l, u;
    cin >> l >> u;
//    Initialize(u);
    pair<int, int> ans = make_pair(INT_MIN, INT_MIN);
    for (int i = l; i <= u; i++)
    {
        pair<int, int> tmp = make_pair(i, Divs(i));
        if (tmp.nd > ans.nd)
            ans = tmp;
        else if (tmp.nd == ans.nd && tmp.st < ans.st)
            ans = tmp;
    }
    printf("Between %d and %d, %d has a maximum of %d divisors.\n", l, u, ans.st, ans.nd);
}

int main()
{
    IamVengeance;
    clock_t s_watch1, s_watch2;
    int tt = 1;
#ifndef ONLINE_JUDGE
    s_watch1 = clock();
    freopen("../input.txt", "r", stdin);
//    freopen("../output.txt", "w", stdout);
#endif
    cin >> tt;
    Initialize();
    for (int i = 1; i <= tt; i++)
    {
        solve();
    }


#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```
