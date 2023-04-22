# [11085 - Back to the 8-Queens](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=2026)
### a `BackTracking` Problem
# Solution
```cpp
#include <bits/stdc++.h>
// #include "Functions.h"
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define vprint(v) for(auto it : v) { cout << it << ' ';} cout << "\n"
#define mprint(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n"
using namespace std;

int n = 8;
vector<vector<int>> sols;
vector<bool> d1((2*n)-1);
vector<bool> d2((2*n)-1);
vector<bool> rows(n);
void Solve(vector<int> &Q , int col , bool repos)
{
    if (col == n) {
        sols.push_back(Q);
        return Solve(Q ,col-1 ,true);
    }
    if (col < 0)
        return ;

    int curd1 = ((n-(col+1)) + Q[col]) - 1;
    int curd2 = (Q[col] + col) - 1;

    int row = 0;
    if (repos) {
        d1[curd1] = d2[curd2] = rows[Q[col] - 1] = false;
        row = Q[col];
    }
    bool found = false;
    for (; row < n ; row++)
    {
        int tmpd1 = ((n-(col+1))+(row+1))-1;
        int tmpd2 = ((row+1)+(col))-1;
        if (!(d1[tmpd1] || d2[tmpd2] || rows[row]))
        {
            d1[tmpd1] = d2[tmpd2] = rows[row] = true;
            Q[col] = row + 1;
            found = true;
            break;
        }
    }
    if (found) {
        return Solve(Q, col + 1, false);
    }
    else return Solve(Q , col - 1 , true);
}

int main()
{
    IamVengeance;
    vector<int> queens(n);
    for (int cases = 1; cin >> queens[0] ; cases++){
        for (int i=1 ; i<n ; i++) {
            cin >> queens[i];
        }
        d1.clear();
        d1.resize((2*n)-1);
        d2.clear();
        d2.resize((2*n)-1);
        rows.clear();
        rows.resize(n);
        vector<int> Q(n ,1);
        Solve(Q , 0 , false);
        int count = n;
        for (int i = 0 ; i < sols.size() ; i++){
//            vprint(sols[i]);
            int cnt = 0;
            for (int j = 0 ; j < sols[i].size() ; j++){
                if (queens[j] != sols[i][j])
                    cnt++;
            }
            if (cnt < count)
                count = cnt;
        }
        cout << "Case " << cases << ": " << count << '\n';
    }

}
```
