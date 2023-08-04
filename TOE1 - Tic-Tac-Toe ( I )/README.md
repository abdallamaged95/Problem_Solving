# [TOE1 - Tic-Tac-Toe ( I )](https://www.spoj.com/problems/TOE1/)
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
#define float_points(x) fixed << setprecision(x)

bool CheckWin(V<V<char>>& TicTac)
{
    // horizontal
    for (int i = 0; i < 3; i++)
    {
        bool found = true;
        for (int j = 1; j < 3; j++) if (TicTac[i][j] != TicTac[i][j-1] || TicTac[i][j] == '.')
                found = false;
        if (found)
            return true;
    }
    // vertical
    for (int j = 0; j < 3; j++)
    {
        bool found = true;
        for (int i = 1; i < 3; i++) if (TicTac[i][j] != TicTac[i-1][j] || TicTac[i][j] == '.')
            found = false;
        if (found)
            return true;
    }
    // diagonal
    bool found = true;
    for (int i = 1; i < 3; i++)
        if (TicTac[i][i] != TicTac[i-1][i-1] || TicTac[i][i] == '.')
            found = false;
    if (found)
        return true;
 
    found = true;
    for (int i = 1; i < 3; i++)
        if (TicTac[i][2-i] != TicTac[i-1][2-(i-1)] || TicTac[i][2-i] == '.')
            found = false;
    if (found)
        return true;
 
    return false;
}

bool BFS(V<V<char>>& TicTac)
{
    queue<pair<V<V<char>>, bool>> q;
    q.push(make_pair(V<V<char>>(3, V<char>(3, '.')), 1));
    while (!q.empty())
    {
        auto curr = q.front();
        q.pop();
        if (curr.st == TicTac)
            return true;
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++) if (curr.st[i][j] == '.' && TicTac[i][j] != '.' && !CheckWin(curr.st))
            {
                (curr.nd)? curr.st[i][j] = 'X' : curr.st[i][j] = 'O';
                if (curr.st[i][j] == TicTac[i][j])
                    q.push(make_pair(curr.st, !curr.nd));
                curr.st[i][j] = '.';
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
    cin >> tt;

    while (tt--)
    {
        V<V<char>> TicTac(3, V<char>(3, '.'));
        V<pair<int, int>> X, O;
        for (int i = 0; i < 3; i++) 
            for (int j = 0; j < 3; j++)
                cin >> TicTac[i][j];

        BFS(TicTac)? cout << "yes\n" : cout << "no\n";
    }

    return 0;
}

```