# [Jumping on Walls - 199D](https://codeforces.com/contest/199/problem/D)
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
map<char ,pair<int ,int>> DIR = {{'U' ,{0 ,1}} ,{'D' ,{0 ,-1}} ,{'J' ,{1 ,0}}};
V<V<char>> wall;
bool BFS(int k)
{
    V<V<bool>> vis(2 ,V<bool>(wall[0].size() ,false));
    pair<int ,int> start = {0 ,0};
    queue<tuple<int ,int ,int>> q;
    q.push(make_tuple(start.st ,start.nd ,-1));
    vis[get<0>(start)][get<1>(start)] = true;
    bool out = false;
    int water = -1;
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();

        for (auto d : DIR)
        {
            auto nxt = make_tuple(get<0>(curr)+d.nd.st ,get<1>(curr)+d.nd.nd ,get<2>(curr)+1);
            if (d.st == 'J')
            {
                get<0>(nxt) %= 2;
                get<1>(nxt) += k;
            }
            int x = get<1>(nxt) ,y = wall[0].size();
            if (x >= y)
                return true;
            
            if (get<1>(nxt) >= 0 && wall[get<0>(nxt)][get<1>(nxt)] == '-' 
                && !vis[get<0>(nxt)][get<1>(nxt)] && get<2>(nxt) < get<1>(nxt))
            {
                q.push(nxt);
                vis[get<0>(nxt)][get<1>(nxt)] = true;
            }
        }
        // water++;
    }
    return out;
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
        int n ,k;
        cin >> n >> k;
        wall.clear();
        wall.resize(2 ,V<char>(n ,'-'));
        for (int i = 0; i < 2; i++)
            for (int j = 0; j < n; j++)
                cin >> wall[i][j];
        
        (BFS(k))? cout << "YES\n" : cout << "NO\n";

    }
        
    return 0;
}

```