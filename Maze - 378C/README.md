# [Maze - 378C](https://codeforces.com/contest/378/problem/C)
### `BackTracking` Problem
# Solution
```cpp
#include <bits/stdc++.h>
// #include "Functions.h"
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define vprint(v) for(auto it : v) { cout << it;} cout << "\n"
#define mprint(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n"
using namespace std;
int n ,m ,k;
vector<vector<char>> maze;
//vector<vector<char>> res;
void print_maze(vector<vector<char>> x){
    for (int i = 0 ; i < n ; i++){
        vprint(x[i]);
    }
}
bool Solve(int x=0 ,int y=0)
{
    if (k <= 0)
        return true;
    if (x == n || x == -1 || y == m || y == -1 || maze[x][y] != '.')
        return false;
    maze[x][y] = '@';
//    print_maze(maze);
//    cerr << "----------------------\n";
    bool s1 = Solve(x+1 ,y);
    if (k <= 0) return true;
    bool s2 = Solve(x, y+1);
    if (k <= 0) return true;
    bool s3 = Solve(x-1 ,y);
    if (k <= 0) return true;
    bool s4 = Solve(x ,y-1);
    if (k <= 0) return true;
    if (!s1 && !s2 && !s3 && !s4) {
        maze[x][y] = 'X';
        k--;
    }
    return (s1 || s2 || s3 || s4);
}

int main()
{
    IamVengeance;
    cin >> n >> m >> k;
    vector<vector<char>> tmp(n ,vector<char>(m));
    maze = tmp;
    int x ,y;
    for (int i = 0 ; i < n ; i++){
        for (int j = 0 ; j < m ; j++){
            cin >> maze[i][j];
            if (maze[i][j] == '.') {
                x = i;
                y = j;
            }
        }
    }
    Solve(x ,y);
    for (int i = 0 ; i < n ; i++){
        for (int j = 0 ; j < m ; j++){
            if (maze[i][j] == '@')
                maze[i][j] = '.';
        }
    }
    print_maze(maze);
    return 0;
}
```