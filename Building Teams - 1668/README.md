# [Building Teams - 1668](https://cses.fi/problemset/task/1668)
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
#define v_print(v) for(auto it : v) { cout << it << ' ';} cout << "\n"
#define m_print(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n"
#define p_add(x ,y) make_pair(x.first+y.first ,x.second+y.second)
#define p_mult(x ,y) make_pair(x.first*y ,x.second*y)

V<int> dis;
V<V<int>> adj;
V<int> team;
bool BFS(int vrtx)
{
    if (dis[vrtx] != -1) return true;
    queue<int> q;
    q.push(vrtx);
    dis[vrtx] = 0; 
    team[vrtx] = 1;
    while (!q.empty())
    {
        int curr = q.front();
        q.pop();
        for (int i : adj[curr])
        {
            if (dis[i] != dis[curr])
                team[i] = (2 - team[curr]) + 1;

            if (dis[i] == -1){
                q.push(i);
                dis[i] = dis[curr]+1;
            }
            else if (dis[i] == dis[curr])
                return false;
        }
    }
    return true;
}

int main()
{
    IamVengeance;

    int n ,m;
    cin >> n >> m;
    adj.resize(n+1 ,V<int>(0));
    for (int i = 0; i < m; i++)
    {
        int x ,y;
        cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    team.resize(n+1 ,0);
    dis.resize(n+1 ,-1);
    for (int i = 1; i <= n; i++)
    {
        if (!BFS(i))
        {
            cout << "IMPOSSIBLE\n";
            return 0;
        }
    }
    for (int i = 1; i <= n; i++)
        cout << team[i] << ' ';
    cout << nl;
}

```