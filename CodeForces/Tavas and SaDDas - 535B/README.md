# [Tavas and SaDDas - 535B](https://codeforces.com/problemset/problem/535/B)
### `BackTracking` Problem
# Solution
```cpp
#include <bits/stdc++.h>
// #include "Functions.h"
typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
#define IamVengeance ios::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define vprint(v) for(auto it : v) { cout << it << ' ';} cout << "\n";
#define mprint(m) for(auto it : m) { cout << it.first << " : " << it.second << "\n";} cout << "\n";
using namespace std;
 
bool Pair2ndComp(const pair<ll ,ll> &a ,const pair<ll ,ll> &b)
{
	return a.second < b.second;
}
 
string n;
int idx = 0;
 
void Lucky(string num)
{	
	for(int i=num.size()-1 ; i>=0 ;i--){
		if (num == n)
			return;
 
		if (num[i] == '7'){
			num[i] = '4';
			continue;
		}
		else{
			num[i] = '7';
			idx++;
			i = num.size();
		}
	}
	idx++;
	num += "4";
	Lucky(num);
}
 
int main()
{
    IamVengeance;
	while (cin >> n)
	{
			idx = 1;
		Lucky("4");
		cout << idx << endl;
	}
}
```