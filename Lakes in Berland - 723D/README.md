# [Lakes in Berland - 723D](https://codeforces.com/contest/723/problem/D)
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
#define v_print(v) for(auto it : v) { cout << it << nl;} cout << nl
#define m_print(m) for(auto it : m) { cout << it.st << " : " << it.nd << nl;} cout << nl
#define p_add(x ,y) make_pair(x.st + y.st ,x.nd + y.nd)
#define p_mult(x ,y) make_pair(x.st * y.st ,x.nd * y.nd)

map<char ,pair<int ,int>> DIR = {{'L' ,{0 ,-1}} ,{'R' ,{0 ,1}} ,{'U' ,{-1 ,0}} ,{'D' ,{1 ,0}}};
V<string> berland;
V<V<bool>> vis;
bool valid(pair<int ,int> x ,int h ,int w)
{
    if (x.st >= h || x.nd >= w || x.st < 0 || x.nd < 0)
        return false;
    return true;
}
pair<int ,pair<int ,int>> BFS(pair<int ,int> start)
{
    if (berland[start.st][start.nd] == '*' || vis[start.st][start.nd]) return {0 ,start};
    queue<pair<int ,int>> q;
    q.push(start);
    vis[start.st][start.nd] = true;
    int lake = 0;
    bool ocean = false;
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();
        lake++;
        if (curr.st == berland.size()-1 || curr.st == 0 || curr.nd == berland[0].size()-1 || curr.nd == 0)
            ocean = true;
        for (auto d : DIR)
        {
            auto nxt = p_add(curr ,d.nd);
            if (valid(nxt ,berland.size() ,berland[0].size()) && !vis[nxt.st][nxt.nd]
                && berland[nxt.st][nxt.nd] == '.')
            {
                q.push(nxt);
                vis[nxt.st][nxt.nd] = true;
            }
        }
    }
    if (ocean)
        return {0 ,start};
    return {lake ,start};
}
void Fill(pair<int ,int> start)
{
    queue<pair<int ,int>> q;
    q.push(start);
    berland[start.st][start.nd] = '*';
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();
        for (auto d : DIR)
        {
            auto nxt = p_add(d.nd ,curr);
            if (valid(nxt ,berland.size() ,berland[0].size()) && berland[nxt.st][nxt.nd] == '.'){
                berland[nxt.st][nxt.nd] = '*';
                q.push(nxt);
            }
        }
    }
}
int main()
{
    IamVengeance;
    // freopen("../input.txt", "r", stdin);
    // freopen("../output.txt", "w", stdout);
    int tt = 1;
    while (tt--)
    {
        int n ,m ,k;
        cin >> n >> m >> k;
        berland.clear();
        berland.resize(n ,"");
        for (int i = 0; i < n; i++) 
            cin >> berland[i];

        vis.clear();
        vis.resize(n ,V<bool>(m ,false));
        V<pair<int ,pair<int ,int>>> lakes;
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++) 
            {
                auto x = BFS({i ,j});
                if (x.st) lakes.push_back(x);
            }
        }
        sort(lakes.begin() ,lakes.end());
        int res = 0;
        for (int i = 0; i < (lakes.size() - k); i++){
            res += lakes[i].st;
            Fill(lakes[i].nd);
        }
        cout << res << nl;
        v_print(berland);
    }

}

```