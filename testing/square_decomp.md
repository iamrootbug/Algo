## 설명
부분합을 구할때, 사이즈가 sqrt(N)인 작은 조각으로 배열을 미리 나눈다.  
각 조각의 부분합을 미리 구한다.  

![sqrt0](https://user-images.githubusercontent.com/62944263/80816982-7f825c00-8c0b-11ea-9a04-70303d404361.jpg)

## 코드
```cpp
int N;
int arr[N];
int blk[N];
int blk_sz = sqrt(N);

auto build = [&](){
  int blk_ix = -1;
  for(int i=0; i<N; i++){
    if(i%blk_sz == 0) blk_ix++;
    blk[blk_ix] += arr[i];
  }
};
//build();

auto query = [&](int a, int b){
  int sum = 0;
  for(int i=0; i<blk_sz; i++){
    if(a%blk_sz == 0) break;
    sum += arr[a++];
  }
  for(int i=0; i<blk_sz; i++){
    if(a+blk_sz-1 > b) break;
    sum += blk[a/blk_sz];
    a += blk_sz;
  }
  for(int i=0; i<blk_sz; i++){
    if(a>b) break;
    sum += arr[a++];
  }
  return sum;
};

auto update = [&](int i, int newVal){
	blk[i/blk_sz] += (newVal - arr[i]);
	arr[i] = newVal;
};

```

## 참고
* https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/?ref=lbp
* https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/?ref=lbp

## 키워드
square root decomposition / range query /
