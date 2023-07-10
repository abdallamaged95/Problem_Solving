# [Road Map - 34D](https://codeforces.com/problemset/problem/34/D)
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
#define v_print(v) for(auto it : v) { cout << it << ' ';} cout << '\n';
#define m_print(m) for(auto it : m) { cout << it.st << " : "; v_print(it.nd) } cout << '\n';
#define p_add(x ,y) make_pair(x.st + y.st ,x.nd + y.nd)
#define p_mult(x ,y) make_pair(x.st * y.st ,x.nd * y.nd)
V<int> route;
V<bool> vis;
map<int ,V<int>> graph;
void DFS(int city ,int r2 = 0)
{
    if(vis[city])
        return;
    vis[city] = true;
    route[city] = r2;
    for(int i : graph[city])
        DFS(i ,city);
}
int main()
{
    IamVengeance;
    // freopen("../../input.txt", "r", stdin);
    // freopen("../../output.txt", "w", stdout);

    int tt = 1;
    // cin >> tt;
    while(tt--)
    {
        int n ,r1 ,r2;
        cin >> n >> r1 >> r2;
        graph.clear();
        for(int i = 1; i <= n; i++) if(i != r1)
        {
            int x; cin >> x;
            graph[i].push_back(x);
            graph[x].push_back(i);
        }
        // m_print(graph);
        route.resize(n+1 ,0);
        vis.clear();
        vis.resize(n+1 ,false);
        DFS(r2);
        for(int i : route) if(i != 0)
            cout << i << ' ';
        cout << '\n';
    }
}  		 		 	 	  			 	 	        		

```