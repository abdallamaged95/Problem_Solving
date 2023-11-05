# [10090 - Marbles](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1031)
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
//#include "Functions.h"
ll GCD(ll a, ll b)
{
    if (b == 0)
        return a;
    return GCD(b, a%b);
}
ll ExtGcd(ll a, ll b, ll& x, ll& y)
{
    if (b == 0)
    {
        x = 1, y = 0;
        return a;
    }
    ll g = ExtGcd(b, a%b, x, y);
    ll tmp = x;
    x = y;
    y = tmp - ((a/b)*x);
    return g;
}
void Solve(int n)
{
    ll c1, c2, n1, n2, x, y;
    cin >> c1 >> n1 >> c2 >> n2;
    int g = ExtGcd(n1, n2, x, y);
    if (n % g)
    {
        cout << "failed\n";
        return;
    }
    x *= (n / g);
    y *= (n / g);
    ll start = ceil((double)(-1*x*g) / (double)n2);
    ll end = floor((double)(y*g) / (double)n1);

    if (start > end)
    {
        cout << "failed\n";
        return;
    }
    ll x1 = x + (start * (n2 / g));
    ll y1 = y - (start * (n1 / g));
    ll x2 = x + (end * (n2 / g));
    ll y2 = y - (end * (n1 / g));
    ll cost1 = (x1 * c1) + (y1 * c2);
    ll cost2 = (x2 * c1) + (y2 * c2);
    if (cost1 <= cost2)
    {
        cout << x1 << ' ' << y1 << '\n';
    }
    else cout << x2 << ' ' << y2 << '\n';
}

int main()
{
    IamVengeance;
    ll tt = 1;
    clock_t s_watch1, s_watch2;
#ifndef ONLINE_JUDGE
    s_watch1 = clock();
    freopen("../input.txt", "r", stdin);
//    freopen("../output.txt", "w", stdout);
#endif

//    cin >> tt;
    ll n;
    while (cin >> n)
    {
        if (n == 0)
            break;
        Solve(n);
    }



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```