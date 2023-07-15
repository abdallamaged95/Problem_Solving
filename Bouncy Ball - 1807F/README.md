# [Bouncy Ball - 1807F](https://codeforces.com/contest/1807/problem/F)
### `Graph` Problem
# Solution
```cpp

#include <bits/stdc++.h>
using namespace std;
#define _CRT_SECURE_NO_WARNINGS
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define V vector
#define st first
#define nd second
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define v_print(v) for(auto it : v) { cout << it << ' '; } cout << '\n';
#define m_print(m) for(auto it : m) { cout << it.st << " : " << it.nd << '\n'; } cout << '\n';
#define p_add(x ,y) make_pair(x.st + y.st ,x.nd + y.nd)
#define p_mult(x ,y) make_pair(x.st * y.st ,x.nd * y.nd)
map<string ,pair<int ,int>> DIR = {{"DR" ,{1 ,1}} ,{"DL" ,{1 ,-1}} ,{"UR" ,{-1 ,1}} ,{"UL" ,{-1 ,-1}}};
V<V<string>> room;
string check_direction(pair<int ,int>& pos ,string d)
{
    if (pos.st == room.size()-1)
        d[0] = 'U';
    if (pos.st == 0)
        d[0] = 'D';
    if (pos.nd == room[0].size()-1)
        d[1] = 'L';
    if (pos.nd == 0)
        d[1] = 'R';
    return d;
    
}
int solve(pair<int ,int> pos ,pair<int ,int> end ,string d)
{
    int bounces = 0;
    while (true)
    {
        if (pos == end)
            return bounces;
        if (room[pos.st][pos.nd] == d)
            return -1;
        else if (room[pos.st][pos.nd] == "-")
            room[pos.st][pos.nd] = d;
        
        string d2 = check_direction(pos ,d);
        if (d2 != d)
        {
            bounces++;
            d = d2;
        }
        else
            pos = p_add(pos ,DIR[d]);
    }
    return -1;
}
int main()
{
    IamVengeance;
    // freopen("../input.txt", "r", stdin);
    // freopen("../output.txt", "w", stdout);

    int tt = 1;
    cin >> tt;
    while (tt--)
    {
        int n ,m;
        pair<int ,int> start ,end;
        string d;
        cin >> n >> m;
        cin >> start.st >> start.nd;
        cin >> end.st >> end.nd;
        cin >> d;
        start = p_add(start ,make_pair(-1 ,-1));
        end = p_add(end ,make_pair(-1 ,-1));
        room.clear();
        room.resize(n ,V<string>(m ,"-"));
        cout << solve(start ,end ,d) << '\n';
    }
        
    return 0;
}

```