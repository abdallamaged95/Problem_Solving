# [10375 - Choose and divide](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1316)
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

void solve(double p, double q, double r, double s)
{
    double tmp_q = min(p-q ,q), tmp_s = min(r-s, s);
    double ans = 1.0;
    for (double i = 1, j = 1; i <= tmp_q || j <= tmp_s; i++, j++)
    {
        double x = 1.0, y = 1.0;
        if (i <= tmp_q)
            x = (p-tmp_q+i) / i;
        if (j <= tmp_s)
            y = (r-tmp_s+j) / j;
        x /= y;
        ans *= x;
    }
    cout << precision(ans, 5) << '\n';
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
//    cin >> tt;

    double p, q, r, s;
    while (cin >> p >> q >> r >> s)
        solve(p, q, r, s);



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```