
c++11新提供的关键字，用例:
```
int x;
decltype(x) y; // make y the same type as x
```

泛型编程用例:
```
template<class T1, class T2>
void ft(T1 x, T2 y){
	decltype(x+y) xpy = x + y;
}
```
