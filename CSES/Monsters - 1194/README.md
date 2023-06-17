# [Monsters - 1194](https://cses.fi/problemset/task/1194)
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
#define st first
#define nd second
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define v_print(v) for(auto it : v) { cout << it;} cout << "\n"
#define m_print(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n"
#define p_add(x ,y) make_pair(x.first+y.first ,x.second+y.second)
#define p_mult(x ,y) make_pair(x.first*y ,x.second*y)
map<char ,pair<int ,int>> DIR = {{'L' ,{0 ,-1}} ,{'R' ,{0 ,1}} ,{'U' ,{-1 ,0}} ,{'D' ,{1 ,0}}};

V<string> maze;
V<V<int>> prediction;
V<V<bool>> visited;
V<V<char>> parent;

bool valid(int x ,int y ,int n ,int m){
    if (x >= 0 && y >= 0 && x < n && y < m)
        return true;
    return false;
}

pair<int ,int> GetOut(int x ,int y)
{
    queue<pair<int ,int>> q;
    V<V<bool>> vis(maze.size() ,V<bool>(maze[0].size() ,false));
    parent.resize(maze.size() ,V<char>(maze[0].size() ,'0'));
    V<V<int>> timing(maze.size() ,V<int>(maze[0].size() ,0));
    q.push({x ,y});
    vis[x][y] = true;
    timing[x][y] = 0;
    pair<int ,int> found = {-1 ,-1};
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();
        vis[curr.st][curr.nd] = true;
        int step = timing[curr.st][curr.nd];
        for (auto d : DIR)
        {
            auto next = p_add(curr ,d.nd);
            if (valid(next.st ,next.nd ,maze.size() ,maze[0].size()) && !vis[next.st][next.nd]
            && step+1 < prediction[next.st][next.nd] && maze[next.st][next.nd] == '.')
            {
                q.push(next);
                parent[next.st][next.nd] = d.st;
                timing[next.st][next.nd] = step+1;
                if (next.st == 0 || next.st == maze.size()-1 || next.nd == 0 || next.nd == maze[0].size()-1){
                    found = next;
                    break;
                }
            }
            if (found.first != -1)
                break;
        }
    }

    return found;
}

void BFS(V<pair<int ,int>> monsters)
{
    queue<pair<int ,int>> q;
    for (auto monster : monsters)
    {
        q.push(monster);
        prediction[monster.st][monster.nd] = 0;
    }
    V<V<bool>> vis(maze.size() ,V<bool>(maze[0].size() ,false));
    while (!q.empty())
    {
        auto curr = q.front();
        vis[curr.st][curr.nd] = true;
        q.pop();
        int x = prediction[curr.st][curr.nd];
        for (auto d : DIR)
        {
            auto next = p_add(curr ,d.nd);
            if (valid(next.st ,next.nd ,prediction.size() ,prediction[0].size())
                && maze[next.st][next.nd] != '#'&& !vis[next.st][next.nd])
            {
                if (x+1 < prediction[next.st][next.nd])
                {
                    q.push(next);
                    prediction[next.st][next.nd] = x+1;
                }
            }
        }
    }   
}

int main()
{
    IamVengeance;

    int n, m;
    cin >> n >> m;
    maze.resize(n,"");
    for (int i = 0; i < n; i++) cin >> maze[i];

    pair<int ,int> start;
    V<pair<int ,int>> monsters;
    for (int i = 0; i < n; i++){
        for (int j = 0; j < m; j++){
            if (maze[i][j] == 'M')
                monsters.push_back({i ,j});
            else if (maze[i][j] == 'A')
                start = {i ,j};
        }
    }
    if (start.st == 0 || start.nd == 0 || start.st == n-1 || start.nd == m-1){
        cout << "YES\n";
        cout << 0 << "\n";
        return 0;
    }
    
    prediction.resize(n ,V<int>(m ,INT_MAX));
    BFS(monsters);

    visited.resize(n ,V<bool>(m ,false));
    auto sol = GetOut(start.st ,start.nd);
    V<char> path;
    if (sol.st == -1)
    {
        cout << "NO\n";
        return 0;
    }
    else {
        while (sol != start)
        {
            path.push_back(parent[sol.st][sol.nd]);
            sol = p_add(sol ,p_mult(DIR[path.back()] ,-1));
        }
    }
    reverse(path.begin() ,path.end());
    if (path.size() <= n*m)
    {
        cout << "YES\n";
        cout << path.size() << "\n";
        v_print(path);
    }
    else cout << "NO\n";
}

```