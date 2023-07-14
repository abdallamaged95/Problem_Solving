# [Olya and Energy Drinks - 877D](https://codeforces.com/contest/877/problem/D)
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
#define m_print(m) for(auto it : m) { cout << it.st << " " << it.nd << '\n'; } cout << '\n';
#define p_add(x ,y) make_pair(x.st + y.st ,x.nd + y.nd)
#define p_mult(x ,y) make_pair(x.st * y.st ,x.nd * y.nd)

map<char ,pair<int ,int>> DIR = {{'R' ,{0 ,1}} ,{'L' ,{0 ,-1}} ,{'D' ,{1 ,0}} ,{'U' ,{-1 ,0}}};
V<string> room;

bool valid(int x ,int y)
{
    return (x < room.size()) && (y < room[0].size()) && (x >= 0) && (y >= 0);
}

int BFS(pair<int ,int> start ,pair<int ,int> end ,int k)
{
    V<V<int>> vis(room.size() ,V<int>(room[0].size() ,INT_MAX));
    queue<pair<int ,int>> q;
    q.push(start);
    vis[start.st][start.nd] = '-';
    bool found = false;
    int cost = 0;
    vis[start.st][start.nd] = cost;
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();
        if (curr == end)
        {
            found = true;
            break;
        }
        for (auto d : DIR)
        {
            auto nxt = curr;
            for (int i = 0; i < k; i++)
            {
                nxt = p_add(nxt ,d.nd);
                if (valid(nxt.st ,nxt.nd) && room[nxt.st][nxt.nd] == '.' 
                    && vis[nxt.st][nxt.nd] >= vis[curr.st][curr.nd]+1)
                {
                    if (vis[nxt.st][nxt.nd] == INT_MAX)
                    {
                        q.push(nxt);
                        vis[nxt.st][nxt.nd] = vis[curr.st][curr.nd]+1;
                    }
                }
                else
                    break;
            }
        }
    }
    if (found)
        return vis[end.st][end.nd];
    return -1;
}
int main()
{
    IamVengeance;
    // freopen("../input.txt", "r", stdin);
    // freopen("../output.txt", "w", stdout);
    
    int tt = 1;
    // cin >> tt;
    while (tt--)
    {
        int n ,m ,k;
        cin >> n >> m >> k;
        room.clear();
        room.resize(n ," ");
        for (int i = 0; i < n; i++)
            cin >> room[i];
        pair<int ,int> start ,end;
        cin >> start.st >> start.nd >> end.st >> end.nd;
        start = p_add(start ,make_pair(-1 ,-1));
        end = p_add(end ,make_pair(-1 ,-1));
        cout << BFS(start ,end ,k) << '\n';
    }

    return 0;
}

```