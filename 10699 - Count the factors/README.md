# [10699 - Count the factors](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1640)
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
    V<bool> valid(1000001, true);
    valid[0] = valid[1] = false;
    for (int i = 2; i*i <= valid.size(); i++)
        for (int j = i+i; j < valid.size(); j+=i)
            valid[j] = false;

    for (int i = 0; i < valid.size(); i++) if (valid[i])
        primes.push_back(i);

}
void solve(int n)
{
    int ans = 0, tmp = n;
    for (int i = 0; primes[i]*primes[i] < n; i++) if (n%primes[i] == 0)
    {
        ans++;
        while (n%primes[i] == 0)
            n /= primes[i];
    }
    if (n > 1)
        ans++;
    cout << tmp << " : " << ans << '\n';
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
//    cin >> tt;
#endif

    Initialize();
    for (int i = 1; true; i++)
    {
        int n; cin >> n;
        if (n == 0)
            break;
        solve(n);
    }


#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```
