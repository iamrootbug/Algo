## 설명
[todo]

## 코드
```cpp
bool check(int m);

auto b = [&](){
  int t; //TRUE
  int f; //FALSE
  while(t+1<f){
    int m = (t+f)/2
    bool res = check(m);
    if(res) t=m;
    else f=m;
  }
  return t;
}
```

## 참고
* https://github.com/iamrootbug/CodeJam/tree/master/2020_Round_1B_2_Blindfolded

## 키워드
binary search / 바이너리 서치
