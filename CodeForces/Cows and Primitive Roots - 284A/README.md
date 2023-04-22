# [Cows and Primitive Roots - 284A](https://codeforces.com/contest/284/problem/A)
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

ll FastPower(ll n ,ll pow ,ll p)
{
	if (pow == 0)
		return 1;
	
	ll res = FastPower(n ,pow/2 ,p);
	res *= res;
	res %= p;
	if (pow % 2)
		return (res * (n%p))%p;
	return res;
}


int main()
{
    IamVengeance;
	int p;
	while (cin >> p)
	{
		int count = 0;
		for (int x = 1 ; x < p ; x++){
			bool valid = true;
			for (int j = 1 ; j <= p-2 ; j++){
				if ((FastPower(x ,j ,p)-1) == 0){
					valid = false;
					break;
				}
			}
			if (valid && (FastPower(x ,p-1 ,p)-1) == 0)
				count++;
		}
		cout << count << endl;
	}

}



```