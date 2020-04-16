## 설명
![segment tree](https://media.geeksforgeeks.org/wp-content/cdn-uploads/RangeMinimumQuery.png)

arr[N] = {arr[0], arr[1], ... , arr[N-1]}이 있을 때, [left, right] 범위에 해당하는 질문의 답을 저장한다.  
arr의 원소들은 길이가 1인 세그먼트 트리의 원소에 대응한다. 또한 리프 노드이다.  
세그먼트 트리는 풀 바이너리 트리이다. 풀 바이너리 트리에서 리프노드가 N개 이면 인터널 노드는 N-1개 이다. [Handshaking lemma에 의해](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)
## 코드
```cpp
int arr[N];
int k = (int)ceil(log2(N));
int MAXN = 2*(1<<k)-1;
int seg[MAXN];

int build(int ss, int se, int si){
	//build(0, N-1, 0);
	if(ss==se) return seg[si] = arr[ss]; // 리프 노드
	int m = (ss+se)/2;
	return seg[si] = min(build(ss,m,2*si+1), build(m+1,se,2*si+2)); // 인터널 노드
}

const int INF = 2e9;
int query(int ss, int se, int si, int qs, int qe){
	//query(0, N-1, 0, qs, qe);
	if(qs<=ss && se<=qe) return seg[si];
	if(se<qs || qe<ss) return INF;
	int m = (ss+se)/2;
	return min(query(ss,m,2*si+1,qs,qe), query(m+1,se,2*si+2,qs,qe));
}

//arr[i] : already changed
void update(int ss, int se, int si, int i){
	//arr[i] = newval;
	//update(0, N-1, 0, i);
	if(i<ss || i>se) return seg[si];
	if(ss==se) return seg[si] = arr[ss];
	int m = (ss+se)/2;
	return seg[si] = min(update(ss,m,2*si+1), update(m+1,se,2*si+2));
}
```

## 참고
* https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/
* https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/

## 키워드
rmq / range minimum query / segment / tree / 
