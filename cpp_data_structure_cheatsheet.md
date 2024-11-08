# AtCoderのためのC++入門:データ構造編

## vector

```cpp
vector<型> 配列変数名;                    // 配列変数を宣言する
配列変数名 = { 要素1, 要素2, ... };       // 配列変数に値を代入する
vector<型> 配列変数名(要素数);            // 要素数で配列を初期化する
vector<型> 配列変数名(要素数, 初期値);    // 配列の各要素を初期値で初期化する

配列変数.at(i);                           // i番目の要素にアクセスする
配列変数.push_back(値);                   // 末尾に要素(値)を追加する
配列変数.pop_back();                      // 末尾の要素を削除する
配列変数.size();                          // 配列の要素数を取得する
```

ループを使って配列に値を代入する

```cpp
vector<int> vec(N);
for(int i = 0; i < N; i++){
  cin >> vec.at(i);
}
```

存在しない要素にアクセスしようとすると実行時エラーが発生する。

```cpp
vector<int> vec(3);
cout << vec.at(10) << "\n";
```

`配列変数[添字]`は、範囲外の添字を指定してしまったときに、エラーメッセージを表示しない。何が原因でプログラムが正しく動作しないのかが分かりにくいので、`配列変数.at(添字)`の書き方を使うようにすること。

### 範囲for文

コンテナと呼ばれるデータ型に対して使うことができる。

```cpp
for(配列の要素の型 変数名 : 配列変数){
  // 各要素に対する処理
}

vector<int> vec = { 1, 3, 1, 2, 5, 10 };
for(int x : vec){
  cout << x << "\n";
}
```

### 2次元配列

```cpp
vector<vector<要素の型>> 変数名(要素数1, vector<要素の型>(要素数2, 初期値));  // 2次元配列を宣言する
vector<vector<要素の型>> 変数名(要素数1, vector<要素の型>(要素数2));          // 初期値を省略して宣言する
変数名.at(i).at(j);                                                           // i行j列目へアクセスする
変数名.size();                                                                // 行の大きさを取得する
変数名.at(0).size();                                                          // 列の大きさを取得する
```

要素を指定して初期化する例

```cpp
vector<vector<int>> data = {
  { 7, 4, 0, 8 },
  { 2, 0, 3, 5 },
  { 6, 1, 7, 0 }
};
```

### 3次元配列

```cpp
vector<vector<vector<要素の型>>> 変数名(要素数1, vector<vector<要素の型>>(要素数2, vector<要素の型>(要素数3, 初期値))); // 3次元配列を宣言する
vector<vector<vector<要素の型>>> 変数名(要素数1, vector<vector<要素の型>>(要素数2, vector<要素の型>(要素数3)));         // 初期値を省略して宣言する
```

要素を指定して初期化する例

```cpp
vector<vector<vector<char>>> data = {
  {
    { '-', '-', '-' },
    { '-', 'x', '-' },
    { '-', 'o', '-' }
  },
  {
    { 'x', 'o', '-' },
    { '-', 'o', '-' },
    { 'x', '-', '-' }
  }
};
```

## pair

```cpp
pair<型1, 型2> 変数名;            // pairを宣言する
pair<型1, 型2> 変数名(値1, 値2);  // pairの初期値を指定して宣言する
変数名.first;                     // 1番目の値にアクセスする
変数名.second;                    // 2番目の値にアクセスする
変数名 = make_pair(値1, 値2);     // pairを生成する

型1 変数1;
型2 変数2;
tie(変数1, 変数2) = pair型の値;   // pairを分解する
```

## tuple

```cpp
tuple<型1, 型2, 型3, (...)> 変数名;                     // tupleを宣言する
tuple<型1, 型2, 型3, (...)> 変数名(値1, 値2, 値3, ...); // tupleの初期値を指定して宣言する
get<K>(tuple型の変数);                                  // K(定数)番目にアクセスする
make_tuple(値1, 値2, 値3, (...));                       // tupleを生成する

型1 変数1;
型2 変数2;
型3 変数3;
...
tie(変数1, 変数2, 変数3, (...)) = tuple型の値;          // tupleを分解する
```

### 範囲for文でautoを使う

```cpp
for(auto 変数名 : 配列変数){
  // 変数名を使う
}
```

## map:連想配列

```cpp
map<Keyの型, Valueの型> 変数名; // mapを宣言する
変数[key] = value;              // 値を追加する
変数.erase(key);                // 値を削除する
変数.at(key);                   // 値にアクセスする
変数.count(key);                // 所属判定
変数.size();                    // 要素数を取得する
```

ループ

```cpp
// ループ処理(Keyの値が小さい順にループ)
for(pair<Keyの型, Valueの型> p : 変数名){
  Keyの型 key = p.first;
  Valueの型 vakue = p.second;
  // key, valueを使う処理
}

// ループをautoで書き換える
for(auto p : 変数名){
  auto key = p.first;
  auto value = p.second;
  // key, valueを使う処理
}
```

ループとautoの使用例

```cpp
map<string, int> score;
score["Alice"] = 100;
score["Dave"] = 95;
score["Bob"] = 89;

// for (pair<string, int> p : score) {
//   string k = p.first;
//   int v = p.second;
//   cout << k << " => " << v << endl;
// }

for (auto p : score) {
  auto k = p.first;
  auto v = p.second;
  cout << k << " => " << v << endl;
}
```

出力

```
Alice => 100
Bob => 89
Dave => 95
```

所属判定の使用例

```cpp
if(変数.count(key)){
  // keyに対応する関係が存在するときの処理
}else{
  // keyに対応する関係が存在しないときの処理
}
```

## queue:待ち行列

```cpp
queue<型> 変数名;   // queueを宣言する
変数.push(値);      // 要素を追加する
変数.front();       // 先頭の要素へアクセスする
変数.pop();         // 先頭の要素を削除する
変数.size();        // 要素数を取得する
変数.empty();       // キューが空であるかを調べる
```

使用例

```cpp
queue<int> q;
q.push(10);
q.push(3);
q.push(6);
q.push(1);

while(!q.empty()){
  cout << q.front() << "\n";
  q.pop();
}
```

出力

```
10
3
6
1
```

## priority_queue:優先度付きキュー

それまでに追加した要素のうち、最も大きいものを取り出す。

```cpp
priority_queue<型> 変数名;    // priority_queueを宣言する
変数.push(値);                // 要素を追加する
変数.top();                   // 最大の要素を取得する
変数.pop();                   // 最大の要素を削除する
変数.size();                  // 要素数の取得
変数.empty();                 // キューが空であるかを調べる

// 値が小さい順に取り出されるpriority_queueの宣言
priority_queue<型, vector<型>, greater<型>> 変数名;
```

使用例

```cpp
priority_queue<int> pq;
pq.push(10);
pq.push(3);
pq.push(6);
pq.push(1);

while(!pq.empty()){
  cout << pq.top() << "\n";
  pq.pop();
}
```

出力

```
10
6
3
1
```

最小の要素を取り出す例

```cpp
priority_queue<int, vector<int>, greater<int>> pq;
pq.push(10);
pq.push(3);
pq.push(6);
pq.push(1);

while(!pq.empty()){
  cout << pq.top() << "\n";
  pq.pop();
}
```

出力

```
1
3
6
10
```

## set:重複の無いデータのまとまりを扱う

```cpp
set<値の型> 変数名;   // setを宣言する
変数.insert(値);      // 要素を追加する
変数.erase(値);       // 要素を削除する
変数.count(値);       // 所属判定
変数.size();          // 要素数を取得する
変数.empty();         // 空であるかを調べる
*begin(変数);         // 最小値を取得する
*rbegin(変数);        // 最大値を取得する
```

ループ

```cpp
for(auto value : 変数名){
  // valueを使う
}
```

使用例

```cpp
set<int> S;
S.insert(3);
S.insert(7);
S.insert(8);
S.insert(10);
S.insert(3);  // 3はすでに含まれているのでこの操作は無視される

cout << "size: " << S.size() << "\n";

if(S.count(7)){
  cout << "found 7" << "\n";
}

for(auto x : S){
  cout << x << " ";
}
```

出力

```
size: 4
found 7
3 7 8 10
```

## stack:LIFO(Last In First Out):後入れ先出し

```cpp
stack<値の型> 変数名; // stackを宣言する
変数.push(値);  // 要素を追加する
変数.top(); // 次の要素にアクセスする
変数.pop(); // 要素を削除する
変数.size();  // 要素数を取得する
変数.empty(); // 空であるか調べる
```

使用例

```cpp
stack<int> S;
S.push(3);
S.push(7);
S.push(1);

while(!S.empty()){
  cout << S.top() << " ";
  S.pop();
}
```

出力

```
1 7 3
```

## deque(double-ended queue):両端キュー

```cpp
deque<値の型> 変数名;

// 値を追加する
変数.push_front(値);  // 先頭に値を追加する
変数.push_back(値); // 末尾に値を追加する

// 値にアクセスする
変数.front(); // 先頭の値にアクセスする
変数.back();  // 末尾の値にアクセスする
変数.at(i); // i番目の値にアクセスする

// 値を削除する
変数.pop_front(); // 先頭の要素を削除する
変数.pop_back();  // 末尾の要素を削除する

// 要素数を取得する
変数.size();

// 空であるかを調べる
変数.empty();
```

使用例

```cpp
deque<int> d;
d.push_front(10);
d.push_back(20);
d.pop_front();
d.pop_back();

d.push_back(30);
d.push_front(40);

for(int x : d){
  cout << x << " ";
}
```

出力

```
40 30
```

## multiset
## unordered_map
## unordered_set