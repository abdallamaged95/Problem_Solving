# [Ice Cave - 540C](https://codeforces.com/problemset/problem/540/C)
### `Graph` Problem
# Solution
```cpp

#include <bits/stdc++.h>
using namespace std;
#define _CRT_SECURE_NO_DEPRECATE
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define V vector
#define nl "\n"
#define st first
#define nd second
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define v_print(v) for(auto it : v) { cout << it << ' ';} cout << nl
#define m_print(m) for(auto it : m) { cout << it.st << " : " << it.nd << nl;} cout << nl
#define p_add(x ,y) make_pair(x.st + y.st ,x.nd + y.nd)
#define p_mult(x ,y) make_pair(x.st * y.st ,x.nd * y.nd)

map<char ,pair<int ,int>> DIR = {{'L' ,{0 ,-1}} ,{'R' ,{0 ,1}} ,{'U' ,{-1 ,0}} ,{'D' ,{1 ,0}}};
V<string> cave;
V<V<bool>> vis;
bool valid(pair<int ,int> x ,int h ,int w)
{
    if (x.st >= h || x.nd >= w || x.st < 0 || x.nd < 0)
        return false;
    return true;
}
bool BFS(pair<int ,int> start ,pair<int ,int> end)
{
    queue<pair<int ,int>> q;
    q.push(start);
    vis[start.st][start.nd] = true;
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();
        for (auto d : DIR)
        {
            auto nxt = p_add(curr ,d.nd);
            if (valid(nxt ,cave.size() ,cave[0].size()) && !vis[nxt.st][nxt.nd]
                && cave[nxt.st][nxt.nd] != 'X')
            {
                q.push(nxt);
                vis[nxt.st][nxt.nd] = true;
                cave[nxt.st][nxt.nd] = 'X';
            }
            else if (nxt == end && cave[nxt.st][nxt.nd] == 'X')
                return true;

        }
    }
    return false;
}
int main()
{
    IamVengeance;
    // freopen("../input.txt", "r", stdin);
    // freopen("../output.txt", "w", stdout);
    int tt = 1;
    while (tt--)
    {
        int n ,m;
        cin >> n >> m;
        cave.clear();
        cave.resize(n ,"");
        for (int i = 0; i < n; i++) 
            cin >> cave[i];
        pair<int ,int> start ,end;
        cin >> start.st >> start.nd >> end.st >> end.nd;
        start = p_add(start ,make_pair(-1 ,-1));
        end = p_add(end ,make_pair(-1 ,-1));
        vis.clear();
        vis.resize(n ,V<bool>(m ,false));
        if (BFS(start ,end))
            cout << "YES\n";
        else cout << "NO\n";
    }

}

```