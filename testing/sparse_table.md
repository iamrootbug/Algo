## 설명
SparseTable, ST[i][j] = index of min[i, i+(1<<j)-1] = index of min{arr[i], arr[i+1], ..., arr[i+(1<<j)-1]}  
i번째 요소부터 길이가 2^j인 부분집합 중 최소 요소의 index를 저장한다.

테이블 빌드시  
![st0](https://user-images.githubusercontent.com/62944263/80311606-972c9f80-881b-11ea-92df-d64994ae362b.jpg)

쿼리 시  
![st1](https://user-images.githubusercontent.com/62944263/80311609-9a279000-881b-11ea-8bb2-71b1cd942057.jpg)

## 코드
```cpp
int arr[N];
//int maxj = (int)log2(N);
//int st[N][maxj+1];
int st[N][100];
auto build = [&](){
  for(int i=0; i<N; i++)
    st[i][0] = i;
  for(int j=1; (1<<j)<=N; j++){ //size of range <= N
    for(int i=0; (i+(1<<j)-1)<N; i++){ //last element's index < N
      if(arr[st[i][j-1]] < arr[st[i+(1<<(j-1))][j-1]])
        st[i][j] = st[i][j-1];
      else
        st[i][j] = st[i+(1<<(j-1))][j-1];
    }
  }
};
build();

auto query = [&](int l, int r)->int{
  int s = (r-l+1);
  int j = (int)log2(s);
  //arr[l,l+(1<<j)-1]
  //arr[r-(1<<j)+1,r]
  if(arr[st[l][j]] < arr[st[r-(1<<j)+1][j]])
    return arr[st[l][r]];
  else
    return arr[st[r-(1<<j)+1][j]];
};
query(0,N-1);
```

## 참고
https://www.geeksforgeeks.org/range-minimum-query-for-static-array/?ref=lbp

## 키워드
sparse table / RMQ / range minimum query /
