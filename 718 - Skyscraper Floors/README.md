# [718 - Skyscraper Floors](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&category=0&problem=659&mosmsg=Submission+received+with+ID+28857061)
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
bool BFS(V<V<bool>>& map, V<bool>& start, V<bool>& end)
{
    V<bool> vis(end.size(), false);
    queue<ll> q;
    for (ll i = 0; i < start.size(); i++)
        if (start[i])
            q.push(i), vis[i] = true;
    while (!q.empty())
    {
        ll curr = q.front();
        q.pop();
        if (end[curr])
            return true;
        for (ll i = 0; i < map[curr].size(); i++)
            if (map[curr][i] && !vis[i])
                q.push(i), vis[i] = true;
    }
    return false;
}
bool Valid(pair<ll, ll> p1, pair<ll, ll> p2, ll limit)
{
    if (abs(p1.nd - p2.nd) % GCD(p1.st, p2.st))
        return false;
    ll x, y, g, lower;
    g = ExtGcd(p1.st, p2.st, x, y);
    if (p1.nd < p2.nd && x < 0)
    {
        x += p2.st / g;
        y -= p1.st / g;
        lower = p1.nd + (p1.st * x * (abs(p1.nd - p2.nd) / g)) % (p1.st * p2.st);
    }
    else if (p2.nd < p1.nd && y < 0)
    {
        y += p1.st / g;
        x -= p2.st / g;
        lower = p2.nd + (p2.st * y * (abs(p1.nd - p2.nd) / g)) % (p1.st * p2.st);
    }
    else lower = p1.nd + (p1.st * abs(x) * (abs(p1.nd - p2.nd) / g)) % (p1.st * p2.st);
    if (lower <= limit)
        return true;
    return false;
}
bool Solve()
{
    ll f, e, a, b;
    cin >> f >> e >> a >> b;
    V<pair<ll, ll>> elevator(e);
    for (auto& i : elevator)
        cin >> i.st >> i.nd;

    V<bool> end(e), start(e);
    bool found = false;
    for (ll i = 0; i < e; i++)
        if (b == elevator[i].nd || (b >= elevator[i].nd && ((b - elevator[i].nd) % elevator[i].st == 0)))
            end[i] = true, found = true;
    if (!found)
        return false;
    found = false;
    for (ll i = 0; i < e; i++)
        if (a == elevator[i].nd || (a >= elevator[i].nd && ((a - elevator[i].nd) % elevator[i].st == 0)))
            start[i] = true, found = true;
    if (!found)
        return false;

    V<V<bool>> map(e, V<bool>(e, false));
    for (ll i = 0; i < e; i++)
        for (ll j = i+1; j < e; j++)
            if (Valid(elevator[i], elevator[j], f))
            {
                map[i][j] = true;
                map[j][i] = true;
            }
    if (BFS(map, start, end))
        return true;
    return false;
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
        if (Solve())
            cout << "It is possible to move the furniture.\n";
        else cout << "The furniture cannot be moved.\n";
    }



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```