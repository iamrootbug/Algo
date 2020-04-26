## 코드
```cpp
auto cntBit = [](int n){
  int cnt = 0;
  for(int i=n; i>0; i&=(i-1)) cnt++;
  return cnt;
};
```
## 키워드
bit / bits / count / 비트 / 카운트
