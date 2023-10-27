# [11768 - Lattice Point or Not](https://vjudge.net/problem/UVA-11768/origin)
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
pair<int, int> readPoint()
{
    float a, b;
    cin >> a >> b;
    return make_pair(a*10, b*10);
}
int Solve()
{
    auto p1 = readPoint();
    auto p2 = readPoint();
    auto tmp = p1;
    p1 = min(tmp, p2);
    p2 = max(tmp, p2);

    int x = p2.st - p1.st ,y = p2.nd - p1.nd;
    int k = GCD(abs(x), abs(y));
    int alpha = abs(x) / k;
    int beta = abs(y) / k;
    int cnt = 0;
    if (y >= 0)
    {
        int idx = 0;
        while (idx <= k)
        {
            if (((idx * alpha) + p1.st) % 10 == 0 &&
                ((idx * beta) + p1.nd) % 10 == 0)
                cnt++;
            idx++;
        }
    }
    else
    {
        int idx = 0;
        while (idx <= k)
        {
            if (((idx * alpha) + p1.st) % 10 == 0 &&
                (p1.nd - (idx * beta)) % 10 == 0)
                cnt++;
            idx++;
        }
    }
    return cnt;
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

    cin >> tt;
    while (tt--)
    {
        cout << Solve() << '\n';
    }



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```