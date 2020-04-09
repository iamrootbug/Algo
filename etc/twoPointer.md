두 개의 포인터를 이용하여 O(N)시간에 배열을 탐색하는 알고리즘

예제. '#'가 백스페이스 문자일 때 문자열 s, t가 동일한 문자열인지 판단하라.
https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/529/week-2/3291/


```cpp
bool backspaceCompare(string s, string t) {
	int i = s.size()-1;
	int j = t.size()-1;
	int skipS = 0;
	int skipT = 0;
	while(i>=0 || j>=0){
		//백스페이스를 처리하고 비교할 s[i]를 찾는다
		while(i>=0){
			if(s[i]=='#'){skipS++; i--;}
			else if(skipS>0){skipS--; i--;}
			else break;	
		}
		//백스페이스를 처리하고 비교할 t[j]를 찾는다
		while(j>=0){
			if(t[j]=='#'){skipT++; j--;}
			else if(skipT>0){skipT--; j--;}
			else break;	
		}
		// 두 문자가 다른 경우
		if(i>=0 && j>=0 && s[i]!=t[j]) return false;
		// 한 쪽은 문자가 있고 다른 쪽은 없을 경우
		if((i>=0) != (j>=0)) return false;
		i--; j--;
	}
	return true;
}
```

## 참고
 * https://www.geeksforgeeks.org/two-pointers-technique/
 * https://m.blog.naver.com/kks227/220795165570
