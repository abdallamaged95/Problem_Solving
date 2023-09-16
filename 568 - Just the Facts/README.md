# [568 - Just the Facts](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=509)
### `Number Theory` Problem
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

int MaxDivPower(int n, int p)
{
    int ans = 0;
    for (ll i = p; i <= n; i*=p)
        ans += n/i;
    return ans;
}
void solve(int n) {
    int twos, fives;
    twos = MaxDivPower(n, 2);
    fives = MaxDivPower(n, 5);
    twos = fives = min(twos, fives);

    int ans = 1;
    for (int i = 1; i <= n; i++)
    {
        if ((i%2 == 0 && twos > 0) || (i%5 == 0 && fives > 0))
        {
            int tmp = i;
            while (twos > 0 && tmp%2 == 0)
                twos--, tmp /= 2;
            while (fives > 0 && tmp%5 == 0)
                fives--, tmp /= 5;
            if (tmp > 1)
                ans *= tmp%10;
        }
        else ans *= i % 10, ans %= 10;
    }
    ans %= 10;
    cout.width(5);
    cout << n;
    cout << " -> " << ans << '\n';
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

    int n;
    while (cin >> n)
        solve(n);



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```