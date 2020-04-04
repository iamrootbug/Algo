s[0:i] = {s[0], s[1], s[2], ..., s[i]}  
p[0:j] = {p[0], p[1], p[2], ..., p[j]}  
s[0:i] 와 p[0:j]에서 문자가 같지 않을때, p[0:j-1]의 가장 긴 prefix = suffix로 이동한다. 


PI 함수
```cpp
vector<int> getPi(string p){
	int m = (int)p.size();
	int j = 0;
	vector<int> pi(m,0);
	for(int i=1; i<m; i++){
		if(p[i] == p[j]) pi[i] = ++j;
		else if(j>0){
			j = pi[j-1]; --j;
		}
	}
}
```
```cpp
vector<int> getPi(string p){
	int m = (int)p.size();
	int j = 0;
	vector<int> pi(m,0);
	for(int i=1; i<m; i++){
		while(j>0 &&p[i]!=p[j]){
			j = pi[j-1];
		}
		if(p[i] == p[j]) pi[i] = ++j;
	}
}
```
문자열 비교 과정
```cpp
vector<int> kmp(string s, string p){
	vector<int> ans;
	auto pi = getPi(p);
	int n = (int)s.size();
	int m = (int)p.size();
	int j = 0;
	for(int i=0; i<n; i++){
		if(s[i] == p[j]){
			if(j==m-1){ ans.push_back(i-m+1); j=pi[j]}
			else j++;
		}
		else if(j>0){
			j=pi[j-1]; --j;
		}
	}
}
```

## 참고
 
 * https://bowbowbow.tistory.com/6#comment5168448
 

