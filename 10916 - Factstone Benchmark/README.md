# [10916 - Factstone Benchmark](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1857)
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

double facts[500001];
void solve(int n)
{
    int decades = ((n-1960) / 10) + 1;
    int word = 4;
    for (int i = 1; i < decades; i++)
        word *= 2;
    int idx = 1;
    while ((int)facts[idx]+1 <= word)
        idx *= 2;
    idx /= 2;
    while ((int)facts[idx]+1 <= word)
        idx++;
    cout << --idx << '\n';

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
//    cout << FactorialBits(500000) << '\n';
    facts[1] = log2(1);
    for (int i = 2; i <= 500000; i++)
        facts[i] = facts[i-1] + log2(i);
    double n;
    while (cin >> n)
    {
        if (n == 0) break;
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