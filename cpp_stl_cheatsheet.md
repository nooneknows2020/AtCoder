# AtCoderのためのC++入門:STLの関数編

## 主要な関数

```cpp
min(a, b);                // 最小値を返す
min({a1, a2, ..., an});   // a1〜anの中で最小のものを返す
max(a, b);                // 最大値を返す
max({a1, a2, ..., an});   // a1〜anの中で最大のものを返す
swap(a, b);               // 値を交換する
```

## 配列操作

```cpp
// vector<int> vec = {1, 5, 3, 2};
reverse(vec.begin(), vec.end());    // 要素を逆順にソート
sort(vec.begin(), vec.end());       // 要素を昇順にソート
sort(vec.rbegin(), r.rend());       // 要素を降順にソート
```

使用形式

```cpp
関数名(配列変数.begin(), 配列変数.end());
```

## 数学関連

```cpp
abs(x);       // 絶対値
pow(x, y);    // xのy乗
sqrt(x);      // 平方根
gcd(a, b);    // 最大公約数
lcm(a, b);    // 最小公倍数
```

## その他の便利な機能

```cpp
to_string(x);   // 数値を文字列に変換
stoi(s);        // 文字列を整数に変換
stod(s);        // 文字列を浮動小数点数に変換
```

使用例

```cpp
string num_str = to_string(123);
int num = stoi("123");
double d = stod("3.14");
```