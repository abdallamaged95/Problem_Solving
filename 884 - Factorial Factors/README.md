# [884 - Factorial Factors](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&category=0&problem=825&mosmsg=Submission+received+with+ID+28772399)
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

int facts[1000001];
V<int> primes;
int PrimeFactors(int n)
{
    int ans = 0;
    for (int i = 0; primes[i]*primes[i] <= n; i++)
        while (n%primes[i] == 0)
            n/=primes[i], ans++;
    if (n > 1)
        ans++;
    return ans;
}
void Init()
{
    V<bool> valid(1e5, true);
    valid[0] = valid[1] = false;
    for (int i = 2; i*i <= valid.size(); i++)
        if (valid[i])
            for (int j = i*2; j <= valid.size(); j+=i)
                valid[j] = false;

    for (int i = 0; i < valid.size(); i++)
        if (valid[i])
            primes.push_back(i);

    facts[2] = 1;
    for (int i = 2; i <= 1e6; i++)
        facts[i] = facts[i-1] + PrimeFactors(i);
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
    Init();
    int n;
    while (cin >> n)
        cout << facts[n] << '\n';



#ifndef ONLINE_JUDGE
    s_watch2 = clock();
    cout << "\nTime Elapsed: " << (ll)(((double)(s_watch2 - s_watch1) / CLOCKS_PER_SEC) * 1000);
    cout << " ms\n";
#endif
    return 0;
}
```