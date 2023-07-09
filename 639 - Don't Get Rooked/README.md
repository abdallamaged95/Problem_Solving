# [639 - Don't Get Rooked](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=580)
### `BackTracking` Problem
```cpp
#include <bits/stdc++.h>
// #include "Functions.h"
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define vprint(v) for(auto it : v) { cout << it << ' ';} cout << '\n'
#define mprint(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n"
using namespace std;
vector<vector<char>> board;
int n ,rooks;
void solve(int x ,int y)
{
    if (board[x][y] == '.'){
        rooks++;
        board[x][y] = '@';
        int idx = x-1;
        while(idx >= 0 && board[idx][y] != 'X'){
            board[idx][y] = '@';
            idx--;
        }
        idx = x+1;
        while(idx < n && board[idx][y] != 'X'){
            board[idx][y] = '@';
            idx++;
        }
        idx = y-1;
        while(idx >= 0 && board[x][idx] != 'X'){
            board[x][idx] = '@';
            idx--;
        }
        idx = y+1;
        while(idx < n && board[x][idx] != 'X'){
            board[x][idx] = '@';
            idx++;
        }
    }
}
int main()
{
    IamVengeance;
    while (cin >> n)
    {
        if (n == 0) return 0;
        vector<vector<char>> origin;
        for (int i = 0 ; i < n ; i++) {
            char x;
            vector<char> r;
            for (int j = 0; j < n; j++) {
                cin >> x;
                r.push_back(x);
            }
            origin.push_back(r);
        }
        rooks = 0;
        int ans = 0;
        for (int r = 0 ; r < n ; r++){
            for (int c = 0 ; c < n ; c++){
                int num1 = 0;
                board = origin;
                rooks = 0;
                for (int i = r ; num1 < n ; i=(i+1)%n ,num1++){
                    int num2 = 0;
                    for (int j = c ; num2 < n ; j=(j+1)%n ,num2++){
                        solve(i ,j);
                    }
                }
                if (rooks > ans)
                    ans = rooks;
            }
        }
        cout << ans << '\n';
    }

}

```