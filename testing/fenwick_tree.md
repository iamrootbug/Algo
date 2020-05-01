## 설명
arr[N+1] = {-1, arr[1], ..., arr[N]} 인덱스를 1부터 사용한다.
두가지 형태가 있을 수 있다.  
fen1[i] = arr[i]까지 LSB(i)개 원소의 최소값  
fen2[i] = arr[i]부터 LSB(i)개 원소의 최소값  
### Fenwick_1
![Fenwick1_BIT1](https://user-images.githubusercontent.com/62944263/80810874-b6527500-8bff-11ea-86e6-09b3f97f48d8.jpeg)

### Fenwick_2
![Fenwick2_BIT2](https://user-images.githubusercontent.com/62944263/80810879-b94d6580-8bff-11ea-9e13-231dbde97d66.jpeg)
## 코드
각 구간의 최소값을 저장하는 펜윅트리 코드
```cpp
int N;
int arr[N+1]; // 인덱스 1부터 사용
vector<int> fen1(N+1, 1e9); //arr[i]까지 LSB(i)개 원소의 최소값 
vector<int> fen2(N+1, 1e9); // arr[i]부터 LSB(i)개 원소의 최소값

auto update = [&](int ix){
  for(int i=ix; i<=N; i+=(i&-i)){ //i+(i&-i) = parent
    int val = arr[i];
    for(int c=i-(i&-i)/2; c<=i-1; c++){ //child
      val = min(val, fen1[c]);
    }
    if(fen1[i]==val) break;
    fen1[i] = val; 
  }
  for(int i=ix; i>0; i-=(i&-i)){ //i-(i&-i) = parent
    int val = arr[i];
    for(int c=i+1; c<=i+(i&-i)/2; c++){ //child
      val = min(val, fen2[c]);
    }
    if(fen2[i]==val) break;
    fen2[i] = val;
  }
};

auto query = [&](int a, int b){
  int ret = 1e9;
  int i;
  for(i=b; i-(i&-i)>=a; i-=(i&-i)) //i-(i&-i) = left sibling
    ret = min(ret, fen1[i]);
  for(i=a; i+(i&-i)<=b; i+=(i&-i)) //i+(i&-i) = right sibling
    ret = min(ret, fen2[i]);
  ret = min(ret, arr[i]);
  return ret;
};
```

부분합을 저장하는 펜윅트리 코드
```cpp
int N;
int arr[N+1];
vector<int> fen(N, 0);

auto update = [&](int ix, int diff){
  for(int i=ix; i<=N; i+=(i&-i)){
    fen[i] += diff;
  }
};

auto sum = [&](int ix){
  int ret = 0;
  for(int i=ix; i>0; i-=(i&-i)){
    ret += fen[i];
  }
  return ret;
};

auto query = [&](int a, int b){
  return sum(b)-sum(a-1);
};
```
## 참고
* https://stackoverflow.com/questions/20800375/solving-range-minimum-queries-using-binary-indexed-trees-fenwick-trees
* https://stackoverflow.com/questions/31106459/how-to-adapt-fenwick-tree-to-answer-range-minimum-queries/34602284#34602284
* https://www.acmicpc.net/blog/view/21

## 키워드
Fenwick / Binary Indexed Tree / rmq / range minimum query / query /
