# [10139 - Factovisors](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1080)
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
void Init()
{
    V<bool> valid(1e5, true);
    valid[0] = valid[1] = false;
    for (int i = 2; i*i <= valid.size(); i++)
        for (int j = i*2; j < valid.size(); j+=i)
            valid[j] = false;
    for (int i = 0; i < valid.size(); i++)
        if (valid[i])
            primes.push_back(i);
}
V<pair<int, int>> Divs(int m)
{
    V<pair<int, int>> divs;
    for (int i = 0; primes[i]*primes[i] <= m; i++) if (m % primes[i] == 0)
    {
        divs.push_back(make_pair(primes[i], 0));
        while (m % primes[i] == 0)
        {
            m /= primes[i];
            divs[divs.size()-1].nd++;
        }
    }
    if (m > 1)
        divs.push_back(make_pair(m, 1));
    return divs;
}
int MaxDivPower(int n, int p)
{
    int ans = 0;
    for (ll i = p; i <= n; i*=p)
        ans += n/i;
    return ans;
}
void solve(int n, int m)
{
    if (m <= n)
    {
        cout << m << " divides " << n << "!\n";
        return;
    }
    V<pair<int, int>> divs = Divs(m), divs2 = Divs(n);
//    m_print(divs);
//    m_print(divs2);
    for (int i = 0; i < divs.size(); i++)
    {
        int x = MaxDivPower(n, divs[i].st);
//        cout << x << " - " << divs[i].nd << '\n';
        if (x < divs[i].nd)
        {
            cout << m << " does not divide " << n << "!\n";
            return;
        }
    }
    cout << m << " divides " << n << "!\n";
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

    int n, m;
    Init();
    while (cin >> n >> m)
        solve(n, m);



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```