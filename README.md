# P1036 [NOIP 2002 普及组] 选数

---

## 算法原理

* dfs深度优先搜索

* 素数的判断

* sqrt（）的时间复杂度

## 代码展示

~~~c++
#include <iostream>
//#include <cmath>  消耗时间长，返回double 

using namespace std;
int n,k,a[25],path = 0,ret = 0;
//素数的判断 
bool check (int x) {
	if (x <= 1) return false;
	//i = x/i代替sqrt 
	for (int i = 2;i <= x/i;i++) {
		if (x%i == 0) return false;
	}
	return true;
}
//爆搜 
void dfs (int pos,int begin) {
	if (pos > k) {
		if (check(path)) ret++;
		return ;
	}
	for (int i = begin;i <= n;i++) {
		path += a[i];
		//作者入的坑 
		dfs(pos + 1,i + 1);
		path -= a[i];
		
	} 
}

int main ()
{
	//加速器 
	ios::sync_with_stdio(0);
	cin.tie(0),cout.tie(0);
	cin >> n >> k;
	for (int i = 1;i <= n;i++) {
		cin >> a[i];
	}
	
	dfs(1,1);
	
	cout << ret << endl; 
	
	return 0;
}
~~~



## 复盘

1. 坑处，作者开始写成了dfs(pos + 1,begin + 1)，在第一层begin永远是一。当i  >= 2时，后续的dfs(pos + 1,bedin + 1)从2开始，相当于begin失忆了。而dfs(pos + 1,i + 1)则是从i后面的一位开始选，不会有重复的现象。
