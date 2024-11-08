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
sort(vec.rbegin(), vec.rend());       // 要素を降順にソート
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

## lower_bound() / upper_bound()

- ソート済みの範囲で二分探索を行う関数
- lower_bound:指定した値以上の最初の要素を返す
- upper_bound:指定した値より大きい最初の要素を返す

```cpp
*lower_bound(配列.begin(), 配列.end(), 値)  // 「値」以上の最小の値
*upper_bound(配列.begin(), 配列.end(), 値)  // 「値」を超える最小の値
```

使用例

```cpp
vector<int> a = {0, 10, 13, 14, 20};
// aにおいて、12 以上最小の要素は 13
cout << *lower_bound(a.begin(), a.end(), 12) << endl; // 13

// 14 以上最小の要素は 14
cout << *lower_bound(a.begin(), a.end(), 14) << endl; // 14

// 10 を超える最小の要素は 13
cout << *upper_bound(a.begin(), a.end(), 10) << endl; // 13
```