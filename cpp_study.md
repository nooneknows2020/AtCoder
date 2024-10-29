# AtCoderのためのC++入門

## 目次

- [第1章:基本文法](#第1章基本文法)
  - 出力とコメント
  - プログラムの書き方
  - プログラムのエラー
  - 四則演算と優先順位
  - 変数と型
  - プログラムの実行順序と入力
  - if文、比較演算子、論理演算子
  - 条件式の結果とbool型
  - 変数のスコープ
  - 複合代入演算子
  - while文
  - for文、break、continue
  - 文字列と文字
  - 配列
  - 組み込み関数(STL)
  - 関数の定義と使用
- 第2章:複雑な計算処理の書き方
  - ループの書き方と範囲for文
  - 多重ループ
  - 多次元配列
  - 参照
  - 再帰関数
  - 計算量
- 第3章:競技プログラミングに役立つ知識
  - 数値型
  - pair/tupleとauto
  - STLのコンテナ(標準テンプレートライブラリ)
  - 構造体
  - ビット演算
  - その他の有用な機能
- 第4章:今まで説明していなかったこと
  - includeディレクティブ
  - 名前空間
  - テンプレート
  - イテレータ
  - ポインタ

## 第1章:基本文法

### 出力とコメント

#### C++プログラムの基本構造

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    // プログラムの内容
    return 0;
}
```

- `#include <bits/stdc++.h>`:C++の機能を全て読み込む
- `using namespace std;`:標準ライブラリの機能を簡潔に使用可能にする
- `main()関数`:プログラムの実行開始点

#### 出力

- `cout`:出力のための機能
- `<<`:データを`cout`に送る演算子
- `endl`:改行を表す
- 文字列は`""`で囲む
- 数値は直接記述可能

```cpp
cout << "Hello, world!" << endl;
cout << 2525 << endl;
```

#### コメント

- `//`:行末までコメント
- `/* */`:複数行コメント

#### 注意点

- セミコロン(`;`)で文を終了
- 基本的に半角文字を使用(全角文字はエラーの原因になりうる)
- 文字列内とコメント内では全角文字使用可能

#### 複数の出力

```cpp
cout << "a" << "b" << endl; // "ab"と出力
cout << "c";
cout << "d" << endl; // "cd"と出力
```

#### コメントアウト

一時的にコードを無効化するテクニック。

```cpp
// cout << "This line will not be executed" << endl;
```

### プログラムの書き方

#### スペースと改行

- C++では基本的にスペースと改行は同じ意味
- 多くの場合省略可能
- 読みやすさのために適切に使用することが推奨される

#### インデント

- 行頭の連続したスペース
- プログラムの動作には影響しないが、可読性を高める
- 基本的に`{`の後でインデントを増やし、`}`の後で戻す
- 長い行は改行してインデントすることもある

### プログラムのエラー

- コンパイルエラー
  - 文法のエラー
  - プログラムは実行されない
  - 例：全角文字の混入、セミコロン忘れ
- 実行時エラー
  - プログラムの内容に致命的な間違いがある場合に発生
  - エラーが発生するまでプログラムは動作する
  - 例：0での除算
- 論理エラー
  - プログラムは動作するが、結果が意図したものと異なる
  - 発見が難しい
  - 例：計算式の間違い

#### エラーの修正方法

- 実行して確認→修正→再実行の繰り返し
- エラーメッセージをWeb検索
- わからない場合は他者に質問

#### コンパイルエラーの例

- 全角スペース
  - エラーメッセージに`stray '\343' in program`などが表示される
  - エラー箇所は`./Main.cpp:行:文字目:error`で特定可能
- セミコロン忘れ
  - エラーメッセージに`expected ';' before...`が表示される
  - エラー箇所はメッセージが示す次の行を確認

#### 大量のエラー・謎のエラー

- 一つのミスで多数のエラーメッセージが出ることがある
- 最初のエラーメッセージを確認し、原因を推測する

### 四則演算と優先順位

#### 基本的な算術演算子

| 演算子 | 計算内容 |
|--------|----------|
| `+`    | 足し算   |
| `-`    | 引き算   |
| `*`    | 掛け算   |
| `/`    | 割り算   |
| `%`    | 剰余     |

#### 四則演算

- 整数同士の計算が可能
- 負の値も扱える
- 整数同士の割り算は小数点以下切り捨て
- 小数点以下を扱うには`.0`をつける(例：`7.0 / 3.0`)

#### 剰余演算

- `%`演算子で割り算の余りを計算
- 例：`7 % 3` は `1`

#### 演算子の優先順位

1. `*`, `/`, `%` (高)
2. `+`, `-` (低)

※ `()`を使って優先順位を変更可能

#### 注意点

- 除算の順序
  - 整数同士の割り算では、計算順序によって結果が異なる場合がある
  - 例：`3 / 2 * 4` ≠ `3 * 4 / 2`
  - 割り算はできるだけ後の方で行うのが望ましい
- ゼロ除算
  - 0で割ると実行時エラーが発生
  - `0 / 3`や`0 % 3`は問題なく計算可能(結果は0)

#### 負の数の剰余

- `A % B`の結果は`A`の正負と一致
- `|A|, |B|`を絶対値とすると
  - `A`が正：`|A| % |B|`
  - `A`が負：`-(|A| % |B|)`

### 変数と型

#### 変数の基本概念

- 変数は「メモ」として機能
- データを保存し、後で使用するために名前を付ける

#### 変数の宣言と初期化

```cpp
int name;  // 宣言
name = 10; // 代入
int value = 20; // 宣言と初期化を同時に行う
```

#### 主要な型

| 型      | データの種類 |
|---------|--------------|
| int     | 整数         |
| double  | 小数(実数) |
| string  | 文字列       |

```cpp
int i = 10;
double d = 0.5;
string s = "Hello";
```

#### 変数の操作

- 変数間のコピー
- 演算での使用

```cpp
int a = 10;
int b = a;  // aの値がbにコピーされる
a = 5;      // aの値が変更されてもbは影響を受けない
```

#### 変数名のルール

- 数字で始まらない
- `_`以外の記号は使用不可
- キーワードは使用不可
- 同じ名前の変数を複数回宣言不可

#### 型変換

- 異なる型同士の計算時に自動的に行われる
- int型とdouble型の計算結果はdouble型になる
- 変換できない型同士の計算・代入はコンパイルエラー

```cpp
int i = 30;
double d = 1.5;
cout << i + d << endl; // 31.5
```

#### 注意点

- 初期化前の変数の値は不定
- string型は自動的に空文字列で初期化される

```cpp
int uninitializedVar;
cout << uninitializedVar << endl; // 値は不定
```

### プログラムの実行順序と入力

#### プログラムの実行順序

- プログラムは基本的に上から下へ順番に実行される
- 変数の値は上書きされると変更される

#### 入力の基本

- `cin >> 変数` で入力を受け取る
- 入力はスペースと改行で区切られる

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a;
    cin >> a;
    cout << a * 10 << endl;
}
```

#### 異なる型のデータ入力

- データの種類に合わせた型の変数を使用する

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string text;
    double d;
    cin >> text >> d;
    cout << text << ", " << d << endl;
}
```

#### 複数の入力

- `cin` を `>>` で繋げて複数の入力を受け取れる
- 入力はスペースか改行で区切る

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b, c;
    cin >> a >> b >> c;
    cout << a * b * c << endl;
}
```

#### 注意点

- `cout` は `<<` でデータを送り、`cin` は `>>` でデータを受け取る
- 入力の順序と変数の順序を合わせる必要がある

### if文、比較演算子、論理演算子

#### if文の基本

- 条件が真の時のみ処理を実行
- 構文:`if (条件式) { 処理 }`

```cpp
if (x < 10) {
    cout << "xは10より小さい" << endl;
}
```

#### 比較演算子

| 演算子 | 意味 |
|--------|------|
| `==`   | 等しい |
| `!=`   | 等しくない |
| `>`    | より大きい |
| `<`    | より小さい |
| `>=`   | 以上 |
| `<=`   | 以下 |

#### 論理演算子

| 演算子 | 意味 | 真になる条件 |
|--------|------|--------------|
| `!`    | 否定 | 条件式が偽 |
| `&&`   | AND  | 両方の条件式が真 |
| `\|\|`   | OR   | 少なくとも一方が真 |

#### 演算子の優先順位

1. `!` (最高)
2. `<`, `<=`, `>`, `>=`
3. `==`, `!=`
4. `&&`
5. `||` (最低)

括弧 `()` を使用して優先順位を明示的に指定することができる。

#### else ifとelse

- else if:前のif文が偽で、新しい条件が真の時に実行
- else:if文の条件が偽の時に実行

```cpp
if (x < 10) {
    cout << "xは10より小さい" << endl;
} else if (x < 20) {
    cout << "xは10以上20未満" << endl;
} else {
    cout << "xは20以上" << endl;
}
```

#### 注意点

- `==`と`=`の混同に注意
- if文のネストが可能
- 処理が1文の場合、`{}`を省略可能

#### 文字列の比較

文字列(string型)も比較演算子を使用して比較できる。

```cpp
string s = "hello";
if (s == "hello") {
    cout << "sはhelloです" << endl;
}
if (s < "world") {
    cout << "sはworldより辞書順で前です" << endl;
}
```

#### 条件演算子(三項演算子)

簡単なif-else文を1行で書くための演算子。

```cpp
int x = 10;
int y = (x > 5) ? 1 : 0;  // xが5より大きければ1、そうでなければ0
```

#### 条件式の型

- 条件式は`bool`型(真理値型)と呼ばれる
- `true`(真)または`false`(偽)のいずれかの値を持つ

```cpp
bool ok = true;
if (ok) {
    cout << "okはtrueです" << endl;
}
```

#### 暗黙の型変換

- 0は`false`、0以外の数値は`true`として扱われる

```cpp
int x = 1;
if (x) {
    cout << "この行は実行されます" << endl;
}
```

#### 比較演算子の連続使用

- `0 <= x <= 10`のような数学的な表現は、C++では正しく動作しない
- 代わりに `0 <= x && x <= 10` と書く必要がある

```cpp
int x = 5;
if (0 <= x && x <= 10) {
    cout << "xは0以上10以下です" << endl;
}
```

#### 短絡評価(Short-circuit evaluation)

論理演算子 `&&` と `||` は短絡評価を行う。

- `&&`:左側の式が`false`の場合、右側は評価されない
- `||`:左側の式が`true`の場合、右側は評価されない

```cpp
int x = 5;
if (x > 0 && (10 / x) > 1) {
    cout << "条件を満たします" << endl;
}
// xが0以下の場合、10/xは評価されないので、0除算エラーを回避できる
```

#### switch文

多数の条件分岐がある場合、switch文を使用すると可読性が向上することがある。

```cpp
int day = 3;
switch (day) {
    case 1:
        cout << "月曜日" << endl;
        break;
    case 2:
        cout << "火曜日" << endl;
        break;
    case 3:
        cout << "水曜日" << endl;
        break;
    // ... 他の曜日 ...
    default:
        cout << "無効な日付" << endl;
}
```

#### 条件式の結果を変数に格納

条件式の結果を直接bool型の変数に格納できる。

```cpp
int x = 10;
bool is_positive = (x > 0);
if (is_positive) {
    cout << "xは正の数です" << endl;
}
```

#### 複合条件の括弧の使用

複雑な条件式では、括弧を使用して優先順位を明確にすることが推奨される。

```cpp
if ((a < b && c < d) || (e < f && g < h)) {
    cout << "条件を満たします" << endl;
}
```

#### ネストされたif文の扱い

if文を多重にネストすると、コードの可読性が低下する。可能な限りネストを減らす工夫をすること。

```cpp
// ネストが深い例
if (condition1) {
    if (condition2) {
        if (condition3) {
            // 処理
        }
    }
}

// 改善例
if (!condition1 || !condition2 || !condition3) {
    return; // 早期リターン
}
// 処理
```

#### ガード節

条件を満たさない場合に早期リターンする方法で、コードの可読性を向上させる。

```cpp
if (error_condition) {
    // エラー処理
    return;
}
// 正常な処理
```

#### 条件演算子のネスト

条件演算子(三項演算子)をネストすることで、複数の条件分岐を1行で書くことができるが、可読性に注意が必要。

```cpp
int x = 10;
string result = (x < 0) ? "負" : (x > 0) ? "正" : "ゼロ";
cout << result << endl;
```

### 条件式の結果とbool型

#### 条件式の結果

- 真の場合:数値の`1`で表現
- 偽の場合:数値の`0`で表現

```cpp
cout << (5 < 10) << endl; // 出力:1 (真)
cout << (5 > 10) << endl; // 出力:0 (偽)
```

#### trueとfalse

- `true`:真を表す予約語
- `false`:偽を表す予約語

```cpp
if (true) {
    cout << "hello" << endl; // 実行される
}
if (false) {
    cout << "world" << endl; // 実行されない
}
```

#### bool型

- `true`または`false`のみを格納できる型
- 条件式の結果や2つの状態を持つものを表現するのに適している

```cpp
bool a = true;
bool b = x < 10; // xが10未満ならtrue、そうでなければfalse
```

#### 真偽値の表現方法

| int型の表現 | bool型の表現 |
|-------------|--------------|
| 真 | 1 | true |
| 偽 | 0 | false |

#### bool型と数値の関係

- `0`は`false`として扱われる
- `0`以外の数値は全て`true`として扱われる

```cpp
bool a = 10; // true
bool b = 0;  // false
```

#### 注意点

- `==`と`=`の書き間違いに注意
- `if (a = b)`は`if (b != 0)`とほぼ同じ意味になってしまう

### 変数のスコープ

- `{}`で囲まれた部分を**ブロック**という
- 変数が使える範囲を**スコープ**という
- 変数のスコープは「変数が宣言されたブロックとそれより内側のブロックでのみ使用可能」
- スコープが重なる場合、最も内側のブロックで宣言された変数が選ばれる

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int x = 5; // xのスコープはここからmain関数の終わりまで
    if (x == 5) {
        int y = 10; // yのスコープはここからif文の終わりまで
        cout << x + y << endl; // 正常に動作
    }
    cout << x << endl; // 正常に動作
    // cout << y << endl; // エラー:yはこのスコープで宣言されていない
}
```

#### 同じ名前の変数

- 異なるブロックであれば、同じ名前の変数を宣言可能

```cpp
int main() {
    int x = 10;
    if (x == 5) {
        int y = 10;
        // string y = "hello"; // エラー:同じブロックに変数yがすでにある
    }
    if (x == 10) {
        string y = "hello"; // OK:異なるブロックなので宣言可能
        cout << x << y << endl;
    }
}
```

#### スコープが重なっている場合

- 変数を使用できる条件
  - 使用箇所より前で宣言されている
  - 同じか外側のブロックで宣言されている
- 同名の変数のスコープが重なる場合、最も内側で宣言された変数が選ばれる

```cpp
int main() {
    int x = 5;
    cout << x << endl; // 5
    if (x == 5) {
        cout << x << endl; // 5
        string x = "hello";
        cout << x << endl; // hello
    }
    cout << x << endl; // 5
}
```

#### スコープの重要性

- プログラムの異なる部分で同じ変数名を再利用可能
- 大規模なプログラムでの変数名の管理を容易にする

### 複合代入演算子

- 同じ変数名が2回現れる代入文を短く書くための演算子
- 例：`x += 1 + 2;` は `x = x + (1 + 2);` と同じ意味
- `x += 1` は `x++` と書ける(インクリメント)
- `x -= 1` は `x--` と書ける(デクリメント)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int x = 5;
    x += 1 + 2;
    cout << x << endl; // 8
}
```

#### 他の複合代入演算子

- `-=`, `*=`, `/=`, `%=` なども同様に使用可能

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a = 5;
    a -= 2;
    cout << a << endl; // 3

    int b = 3;
    b *= 1 + 2;
    cout << b << endl; // 9

    int c = 4;
    c /= 2;
    cout << c << endl; // 2

    int d = 5;
    d %= 2;
    cout << d << endl; // 1
}
```

#### インクリメントとデクリメント

- インクリメント(1増やす):`x++` または `++x`
- デクリメント(1減らす):`x--` または `--x`

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int x = 5;
    x++;
    cout << x << endl; // 6

    int y = 5;
    y--;
    cout << y << endl; // 4
}
```

#### シンタックスシュガー

- これらのプログラムを短く書くための記法を「シンタックスシュガー」と呼ぶ

### while文

#### while文の基本

- 条件式が真の間、処理を繰り返す
- 構文:`while (条件式) { 処理 }`

```cpp
while (true) {
    cout << "Hello" << endl;
    cout << "AtCoder" << endl;
}
```

#### カウンタを使用したループ

- 変数を使って繰り返し回数を制御する

```cpp
int i = 1;
while (i <= 5) {
    cout << i << endl;
    i++;
}
```

#### 推奨されるループの書き方

- カウンタ変数は0から始め、N未満でループする

```cpp
int N = 5;
int i = 0;
while (i < N) {
    cout << "Hello" << endl;
    i++;
}
```

#### 応用例:合計値の計算

```cpp
int N;
cin >> N;
int sum = 0;
int x;
int i = 0;
while (i < N) {
    cin >> x;
    sum += x;
    i++;
}
cout << sum << endl;
```

#### 応用例:2ずつ増加

```cpp
int i = 0;
while (i < 10) {
    cout << i << endl;
    i += 2;
}
```

#### 応用例:逆順ループ

```cpp
int i = 5;
while (i >= 0) {
    cout << i << endl;
    i--;
}
```

#### 注意点

- 無限ループに注意(AtCoderでは実行時間制限あり)
- カウンタ変数の名前は通常`i`, `j`, `k`の順で使用

### for文、break、continue

#### for文の基本

- 繰り返し処理を簡潔に書くための構文
- 構文:`for (初期化; 条件式; 更新) { 処理 }`

```cpp
for (int i = 0; i < 3; i++) {
    cout << "Hello for: " << i << endl;
}
```

#### N回の繰り返し処理

- 一般的なパターン:`for (int i = 0; i < N; i++) { 処理 }`

```cpp
int N = 5;
for (int i = 0; i < N; i++) {
    cout << i << endl;
}
```

#### break文

- ループを途中で抜けるための命令

```cpp
for (int i = 0; i < 5; i++) {
    if (i == 3) {
        cout << "ぬける" << endl;
        break;
    }
    cout << i << endl;
}
```

#### continue文

- 後の処理をとばして次のループへ行くための命令

```cpp
for (int i = 0; i < 5; i++) {
    if (i == 3) {
        cout << "とばす" << endl;
        continue;
    }
    cout << i << endl;
}
```

#### for文とwhile文の違い

- カウンタ変数のスコープ:for文の方が狭い
- continueの動作:while文では更新処理を飛ばす可能性がある

#### for文の応用

- 省略形:`for (; 条件式;) { 処理 }`
- 無限ループ:`for (;;) { 処理 }`
- 多重ループ(ネスト)

```cpp
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 2; j++) {
        cout << "i: " << i << ", j:" << j << endl;
    }
}
```

#### コツと注意点

- for文は主に「決まった回数の繰り返し」に使用
- while文は主に「条件が満たされる間の繰り返し」に使用
- break文とcontinue文は適切に使用することで、コードの可読性と効率を向上させる
- 無限ループに注意(特にwhile文やcontinueを使用する際)

### 文字列と文字

#### 文字列(string型)

- 文字が順番に並んだもの
- string型を使用して扱う

```cpp
string str1, str2;
cin >> str1;
str2 = ", world!";
cout << str1 << str2 << endl;
```

#### 文字列の長さ

- `文字列変数.size()`で取得

```cpp
string str = "Hello";
cout << str.size() << endl; // 5
```

#### 文字列の要素へのアクセス

- `文字列変数.at(i)`でi番目の文字にアクセス
- 添字は0から始まる

```cpp
string str = "hello";
cout << str.at(0) << endl; // h
cout << str.at(4) << endl; // o
```

#### 文字(char型)

- 一文字のデータを保持
- シングルクォーテーション(')で囲む

```cpp
char c = 'a';
cout << c << endl; // a
```

#### 文字列と文字の関係

- `文字列変数.at(i)`はchar型を返す

```cpp
string str = "Hello";
char c = str.at(0);
cout << c << endl; // H
```

#### 文字列の操作

- 書き換え
- 比較

書き換えの例。

```cpp
string str = "Hello";
str.at(0) = 'M';
cout << str << endl; // Mello
```

比較の例。

```cpp
if (str.at(1) == 'e') {
    cout << "AtCoder" << endl;
}
```

#### ループとの組み合わせ

```cpp
string str;
cin >> str;
int count = 0;
for (int i = 0; i < str.size(); i++) {
    if (str.at(i) == 'O') {
        count++;
    }
}
cout << count << endl;
```

#### 注意点

- 添字が範囲外の場合、実行時エラーが発生
- 全角文字は正しく扱えない
- 文字列のメンバ関数使用時は変数に格納するか、リテラルの末尾に's'をつける

```cpp
cout << "Hello"s.size() << endl; // 5
```

#### 文字列の比較

- string型には比較演算子(==, !=, <, <=, >, >=)が定義されている
- 辞書順で比較される('0'\~'9' → 'A'\~'Z' → 'a'\~'z')

```cpp
string s1 = "ABC";
string s2 = "XY";
if (s1 < s2) {
    cout << "ABC < XY" << endl;
}
```

#### 文字列の連結

- `+`演算子で文字列を連結できる
- `+=`演算子も使用可能

```cpp
string hello = "Hello";
cout << hello + ", world!" << endl;
hello += ", AtCoder!";
```

#### stringとcharの比較と連結

- string型とchar型は`==`で直接比較できない
- string型とchar型は`+`で連結可能

```cpp
string str = "Hello";
char c = str.at(0);
cout << str + c << endl; // HelloH
```

#### char型の変数への入力

- cinでchar型変数に入力すると、一文字ずつ取り出せる

```cpp
char a, b;
cin >> a >> b;
```

#### エスケープシーケンス

- 特殊な文字を表現するための記法
- 主なエスケープシーケンス：
  - `\n`:改行
  - `\"`:二重引用符
  - `\'`:引用符
  - `\\`:バックスラッシュ
  - `\t`:タブ
  - `\r`:復帰

```cpp
cout << "こんにちは\nAtCoder";
```

#### 行単位での入力

- `getline(cin, 変数名)`で行単位の入力が可能
- 空白を含む文字列の入力に使用

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    getline(cin, s);
    cout << s << endl;
}
```

- 注意点
  - `cin >> 変数名`の後に`getline`を使用する場合、間に`cin.ignore()`を挿入する必要がある
  - これは`cin`が改行を読み飛ばさないため

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s, t;
    cin >> s;
    cin.ignore(); // この行を追加
    getline(cin, t);
    cout << s << endl;
    cout << t << endl;
}
```

#### 文字列の分割

- `stringstream`を使用して文字列を分割できる

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s = "Hello AtCoder";
    stringstream ss(s);
    string word;
    while (ss >> word) {
        cout << word << endl;
    }
}
```

#### 文字列から数値への変換

- `stoi(文字列)`：文字列をint型に変換
- `stoll(文字列)`：文字列をlong long型に変換
- `stod(文字列)`：文字列をdouble型に変換

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s = "100";
    int x = stoi(s);
    cout << x + 1 << endl; // 101
}
```

### 配列

#### 配列の基本

- 配列は様々なデータの列を扱う機能
- 宣言:`vector<型> 配列変数名;`
- 初期化:`配列変数名 = { 要素1, 要素2, ... };`

```cpp
vector<int> vec;
vec = {25, 100, 64};
```

#### 配列の要素へのアクセス

- `配列変数.at(i)`:i番目の要素にアクセス
- 添字は0から始まる

```cpp
cout << vec.at(0) << endl; // 25
```

#### 配列の大きさ

- `配列変数.size()`:配列の要素数を取得

```cpp
cout << vec.size() << endl; // 3
```

#### 配列の初期化

- `vector<型> 配列変数名(要素数)`:指定した要素数で初期化

```cpp
vector<int> vec(3); // {0, 0, 0}
```

#### 配列への入力

- for文を使用して入力を受け取る

```cpp
int N;
cin >> N;
vector<int> vec(N);
for (int i = 0; i < N; i++) {
    cin >> vec.at(i);
}
```

#### 配列の応用

- 複数の変数を一度に扱える
- for文と組み合わせて大量のデータを処理

```cpp
vector<int> math(N), english(N);
for (int i = 0; i < N; i++) {
    cin >> math.at(i);
}
for (int i = 0; i < N; i++) {
    cin >> english.at(i);
}
for (int i = 0; i < N; i++) {
    cout << math.at(i) + english.at(i) << endl;
}
```

#### その他の機能

- 初期値の指定:`vector<型> 配列名(要素数, 初期値);`
- 要素の追加:`配列変数.push_back(値);`

```cpp
vector<int> vec(3, 5); // {5, 5, 5}
vec.push_back(10); // {5, 5, 5, 10}
```

#### 注意点

- 範囲外アクセスに注意
- `at()`を使用することで範囲外アクセス時にエラーメッセージを得られる

#### vector以外の配列

C++には3種類の主な配列の宣言方法がある。

- vectorによる配列:`vector<int> data(3);`
- Cの配列:`int data;`
- arrayによる配列:`array<int, 3> data;`

#### 注意点

- Cの配列は落とし穴が多いため、基本的にはvectorを使用することが推奨される
- AtCoderの模範解答ではCの配列が使われることもあるため、両方の記法を理解しておくことが有用

#### atを使わないアクセス方法

- `配列変数[添字]`でも要素にアクセス可能
- しかし、この方法は範囲外アクセス時にエラーメッセージを表示しない
- デバッグの容易さから、`配列変数.at(添字)`の使用が推奨される

```cpp
vector<int> vec = {1, 2, 3};
cout << vec[0] << endl; // 1 (atを使わないアクセス)
cout << vec.at(0) << endl; // 1 (atを使うアクセス)
```

#### 配列の初期化方法

複数の初期化方法が存在する。

- 要素を直接指定:`vector<int> vec = {1, 2, 3};`
- サイズと初期値を指定:`vector<int> vec(3, 0);` // {0, 0, 0}
- サイズのみ指定(デフォルト値で初期化):`vector<int> vec(3);` // {0, 0, 0}

#### 多次元配列

- vectorを入れ子にすることで多次元配列を作成可能

```cpp
vector<vector<int>> vec(3, vector<int>(4));
```

これは3行4列の2次元配列を作成する。

### 組み込み関数(STL)

- STL(Standard Template Library):C++で用意されている関数等のまとまり
- 関数呼び出し:`関数名(引数1, 引数2, ...)`
- 引数:関数に渡す値
- 返り値(戻り値):関数の計算結果

#### 主要なSTL関数

##### min関数:2つの引数のうち小さい方の値を返す

```cpp
int answer = min(10, 5);
cout << answer << endl; // 5
```

##### max関数:2つの引数のうち大きい方の値を返す

```cpp
int answer = max(10, 5);
cout << answer << endl; // 10
```

##### swap関数:2つの引数の値を交換する

```cpp
int a = 10, b = 5;
swap(a, b);
cout << a << " " << b << endl; // 5 10
```

#### 配列を引数にする関数

##### reverse関数:配列の要素の並びを逆にする

```cpp
vector<int> vec = {1, 5, 3};
reverse(vec.begin(), vec.end());
// vec は {3, 5, 1} になる
```

##### sort関数:配列の要素を小さい順に並び替える

```cpp
vector<int> vec = {2, 5, 2, 1};
sort(vec.begin(), vec.end());
// vec は {1, 2, 2, 5} になる
```

#### 注意点

- 引数と返り値の型は関数によって決まっている
- 型が合わないとコンパイルエラーになる
- 配列を引数にする関数は特殊な形式で呼び出す:`関数名(配列変数.begin(), 配列変数.end())`

#### 応用

- sort関数とreverse関数を組み合わせて大きい順にソート

```cpp
vector<int> vec = {2, 5, 2, 1};
sort(vec.begin(), vec.end());
reverse(vec.begin(), vec.end());
// vec は {5, 2, 2, 1} になる
```

#### 引数で関数を呼び出した場合の実行順序

- 関数の引数として別の関数を呼び出す場合、内側の関数から実行される

```cpp
min(max(1, 2), 3)
```

- 実行順序
  1. `max(1, 2)` が実行され、結果は2
  2. `min(2, 3)` が実行され、最終結果は2

#### 引数の実行順序

- 引数の実行順序は環境によって異なる
- APG4bの推奨環境(GCC, C++)では、最後の引数の式から順に実行される

```cpp
min(1 + 1, 2 + 2)
```

- GCCでの実行順序
  1. `2 + 2` が実行され、4になる
  2. `1 + 1` が実行され、2になる
  3. `min(2, 4)` が実行され、最終結果は2

他の環境(Clang等)では、最初の引数の式から順に実行されることがある。

- Clangでの実行順序
  1. `1 + 1` が実行され、2になる
  2. `2 + 2` が実行され、4になる
  3. `min(2, 4)` が実行され、最終結果は2

#### 注意点

- この挙動の違いが問題になるケースは少ないが、自作関数を定義する際には注意が必要
- 環境依存の挙動に頼らないコーディングが推奨される

### 関数の定義と使用

#### 関数の定義

- 構文:`返り値の型 関数名(引数1の型 引数1の名前, 引数2の型 引数2の名前,...) { 処理 }`

```cpp
int my_min(int x, int y) {
    if (x < y) {
        return x;
    } else {
        return y;
    }
}
```

#### 返り値の指定

- `return 返り値;` で指定
- 返り値がない場合は `void` を使用し、`return;` と書く

#### 引数がない関数

- `()` だけを書く

```cpp
int input() {
    int x;
    cin >> x;
    return x;
}
```

#### 関数の動作

- 関数呼び出し時に引数の値がコピーされる
- return文に到達すると関数の処理が終了する

#### 注意点

- 返り値の指定忘れに注意(未定義の値が返る可能性)
- 引数はコピーされるため、関数内での変更は呼び出し元に影響しない

#### 関数が呼び出せる範囲

- 関数は宣言した行より後でしか呼び出せない
- プロトタイプ宣言を使用すると、定義前に呼び出し可能

#### その他の機能

- 関数のオーバーロード：同じ名前で異なる引数の関数を定義可能
- main関数：特別な関数で、returnを省略すると0を返す

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

int my_min(int x, int y) {
    if (x < y) {
        return x;
    } else {
        return y;
    }
}

void hello(string text) {
    cout << "Hello, " << text << endl;
}

int main() {
    int answer = my_min(10, 5);
    cout << answer << endl;  // 5

    hello("C++");  // Hello, C++

    return 0;
}
```

#### プロトタイプ宣言

- 関数を定義する前に呼び出すためのテクニック
- 構文:`返り値の型 関数名(引数1の型, 引数2の型, ...);`
- 引数名は省略可能

```cpp
void hello(); // プロトタイプ宣言

int main() {
    hello(); // プロトタイプ宣言により呼び出し可能
}

void hello() {
    cout << "hello!" << endl;
}
```

#### returnの省略

- 返り値がない関数(void型)では、関数末尾のreturnを省略可能

#### main関数の特殊性

- returnを省略した場合、自動的に0が返される

#### 関数のオーバーロード

- 同じ名前で異なる引数の型や数の関数を定義可能
- 返り値の型だけが異なる場合はオーバーロードできない

```cpp
int my_min(int x, int y) { /* ... */ }
int my_min(int x, int y, int z) { /* ... */ }
```

#### 複雑な引数の条件指定

- テンプレートを使用することで、より柔軟な引数の条件指定が可能
- 例：「大小比較ができる型なら何でも良い」など

#### 変数のスコープ

- 関数内の変数は、その関数のスコープ内でのみ有効
- 同じ名前の変数でも、異なる関数内では別の変数として扱われる

```cpp
void test() {
    int num = 5;
    cout << num << endl; // 5
}
int main() {
    int num = 10;
    test();
    cout << num << endl; // 10
}
```

## 第2章:複雑な計算処理の書き方

### ループの書き方と範囲for文

#### ループ処理を書く3ステップ

1. ループを使わずに書く
2. パターンを見つける
3. ループで書き直す

#### 例題解説

問題:整数aと5個の整数x_1, ..., x_5が与えられ、aと等しい個数を求める。

ステップ1:ループを使わずに書く

```cpp
int answer = 0;
if (data.at(0) == a) answer++;
if (data.at(1) == a) answer++;
if (data.at(2) == a) answer++;
if (data.at(3) == a) answer++;
if (data.at(4) == a) answer++;
```

ステップ2:パターンを見つける

```cpp
if (data.at(数値) == a) answer++;
```

ステップ3:ループで書き直す

```cpp
for (int i = 0; i < 5; i++) {
    if (data.at(i) == a) {
        answer++;
    }
}
```

#### 範囲for文

構文:`for (配列の要素の型 変数名 : 配列変数) { 処理 }`

```cpp
vector<int> a = {1, 3, 2, 5};
for (int x : a) {
    cout << x << endl;
}
```

- breakとcontinueも使用可能
- string型にも使用可能

#### ループ構文の使い分け

- 配列の全要素に対する処理:範囲for文
- 一定回数の繰り返し:for文
- それ以外:while文

#### while文が適しているケース

例:整数Nが2で最大何回割り切れるかを求める

```cpp
int count = 0;
while (N > 0) {
    if (N % 2 > 0) break;
    N = N / 2;
    count++;
}
```

### 多重ループ

- ループの中にさらにループがある構造
- 二重ループ、三重ループなどがある

```cpp
// 例:二重ループ
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        cout << "i:" << i << ", j:" << j << endl;
    }
}
```

#### 多重ループの使用例

問題例:3要素の2つの配列A, Bに同じ要素が含まれているかどうか判定する

```cpp
bool answer = false;
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (A.at(i) == B.at(j)) {
            answer = true;
        }
    }
}
```

#### 多重ループでのbreak/continue

- breakは1段階のループのみを抜ける
- 多重ループを一度に抜けるにはフラグ変数を使用する

```cpp
bool finished = false;
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        if (/* 条件 */) {
            finished = true;
            break;
        }
    }
    if (finished) {
        break;
    }
}
```

#### 関数を使った多重ループの脱出

- 関数内でreturnを使用して一気に抜ける方法もある

```cpp
void func() {
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 10; j++) {
            if (/* 条件 */) {
                return;
            }
        }
    }
}
```

#### 注意点

- 添字のミスに注意(特に内側のループの更新部分)
- カウンタ変数の命名は通常i, j, k, l...だが、意味が明確な場合は自由に命名してもよい

### 多次元配列

#### 2次元配列

```cpp
// 宣言
vector<vector<要素の型>> 変数名(要素数1, vector<要素の型>(要素数2, 初期値)); // 初期値は省略可能。

// アクセス
変数名.at(i).at(j) // i行目j列目

// 大きさの取得
変数名.size() // 縦の要素数
変数名.at(0).size() // 横の要素数
```

#### 要素を指定して初期化する方法

```cpp
vector<vector<int>> data = {
    {7, 4, 0, 8},
    {2, 0, 3, 5},
    {6, 1, 7, 0},
};
```

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<vector<int>> data(3, vector<int>(4));
    
    // 入力
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            cin >> data.at(i).at(j);
        }
    }
    
    // 0の個数を数える
    int count = 0;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            if (data.at(i).at(j) == 0) {
                count++;
            }
        }
    }
    cout << count << endl;
}
```

#### 3次元配列

```cpp
// 宣言
vector<vector<vector<要素の型>>> 変数名(要素数1, vector<vector<要素の型>>(要素数2, vector<要素の型>(要素数3, 初期値)));
```

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int N;
    cin >> N;
    vector<vector<vector<char>>> data(N, vector<vector<char>>(3, vector<char>(3)));
    
    // 入力
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < 3; j++) {
            for (int k = 0; k < 3; k++) {
                cin >> data.at(i).at(j).at(k);
            }
        }
    }
    
    // 'o'の数を数える
    int count = 0;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < 3; j++) {
            for (int k = 0; k < 3; k++) {
                if (data.at(i).at(j).at(k) == 'o') {
                    count++;
                }
            }
        }
    }
    cout << count << endl;
}
```

#### 特殊な2次元配列

##### N×0の2次元配列

後から要素を追加して使う場合に有用。

```cpp
vector<vector<型>> 変数名(N);
```

これは「要素数0の配列」のN個の配列を作成する。

##### ジャグ配列(行ごとに要素数が異なる配列)

```cpp
vector<vector<int>> data(3); // 3×0の配列
data.at(0).push_back(1);
data.at(0).push_back(2);
data.at(0).push_back(3); // data.at(0)は3要素の配列
data.at(1).push_back(4);
data.at(1).push_back(5);
data.at(1).push_back(6);
data.at(1).push_back(7); // data.at(1)は4要素の配列
data.at(2).push_back(8);
data.at(2).push_back(9); // data.at(2)は2要素の配列
```

#### 多次元配列の考え方

- 3次元配列は「2次元配列の配列」と考える
- N次元配列は「N-1次元配列の配列」と考える

#### 注意点

- 多次元配列は、次元が増えるほど宣言が複雑になる
- 実用上は3次元配列までが多く、それ以上の次元はあまり使用されない

### 参照

- 定義:`参照先の型 &参照の名前 = 参照先;`
- 参照は変数に別名を付けるような機能

```cpp
int a = 3;
int &b = a; // bはaの参照
b = 4; // aの値も4に変更される
```

#### 参照の特徴

- 宣言時に参照先を指定する必要がある
- 参照先を後から変更することはできない
- 参照自体の値にはアクセスできない(常に参照先の値を扱う)

#### 関数の引数での参照(参照渡し)

- 関数内で呼び出し側の変数を直接変更できる
- 値渡しとの違い：コピーが発生しない

```cpp
void f(int &x) {
    x = x * 2; // 呼び出し側の変数が変更される
}

int main() {
    int a = 3;
    f(a);
    cout << a << endl; // 6が出力される
}
```

#### 参照渡しの利点

1. 複数の結果を返せる

```cpp
void min_and_max(int a, int b, int c, int &minimum, int &maximum) {
    minimum = min(a, min(b, c));
    maximum = max(a, max(b, c));
}
```

2. 無駄なコピーを減らせる(特に大きな配列の場合に効果的)

```cpp
int sum100(vector<int> &a) { // 参照渡し
    int result = 0;
    for (int i = 0; i < 100; i++) {
        result += a.at(i);
    }
    return result;
}
```

#### 注意点

- 参照を宣言する際は必ず参照先を指定する
- constを使用して参照先の変更を防ぐことができる
- 参照の参照は作成できない(単に元の変数への参照になる)

#### constを用いた参照

- `const`キーワードを使用して、参照先の変更を防ぐことができる
- 関数の引数で使用すると、関数内で参照先の値を変更できなくなる

```cpp
void f(const int &x) {
    x = 2; // エラー：constな参照なので書き換えられない
}
```

#### 参照の参照

- 参照の参照を作成しようとしても、単に元の変数への参照になる

```cpp
int x = 5;
int &y = x;
int &&z = y; // zはxへの参照になる(yへの参照の参照ではない)
```

#### 関数の返り値としての参照

- 関数の返り値を参照にすることも可能
- ただし、関数内のローカル変数への参照を返すと危険(変数のライフタイムが終了するため)

```cpp
int &f() {
    int x = 5;
    return x; // 危険：xのライフタイムが終了する
}
```

#### 参照の配列

- C++では参照の配列を作ることはできない
- 代わりに、ポインタの配列を使用することができる

```cpp
int a = 1, b = 2, c = 3;
int *arr[3] = {&a, &b, &c}; // ポインタの配列
```

#### 参照と値渡しの使い分け

- 大きなオブジェクトを渡す場合や、関数内で変更を加えたい場合は参照渡しを使用
- 小さなオブジェクトや、関数内で変更を加えたくない場合は値渡しを使用

### 再帰関数

#### 再帰関数の基本概念

- 再帰呼び出し：ある関数の中で同じ関数を呼び出すこと
- 再帰関数：再帰を行う関数
- ベースケース：再帰呼び出しを行わずに完了できる処理
- 再帰ステップ：再帰呼出しを行い、その結果を用いて行う処理

#### 再帰関数の実装方法(3ステップ)

1. 「引数」「返り値」「処理内容」を決める
2. 再帰ステップの実装
3. ベースケースの実装

#### 再帰関数の性質

- 正しく動作するための条件：再帰呼び出しの連鎖に終わりがある
- ベースケースと再帰ステップの両方が必要

#### 再帰関数の動作イメージ

- 関数呼び出しごとに新しい変数が作られる
- 呼び出し元の関数の処理は一時停止する
- 再帰呼び出しが終了すると、呼び出し元の関数の処理が再開される

#### 再帰関数の実装例

##### 例1:0からnまでの総和を計算する関数

```cpp
int sum(int n) {
    if (n == 0) {
        return 0;  // ベースケース
    }
    int s = sum(n - 1);  // 再帰ステップ
    return s + n;
}
```

##### 例2:n番目のフィボナッチ数を求める関数

```cpp
int fibo(int n) {
    if (n == 0) return 0;  // ベースケース
    if (n == 1) return 1;  // ベースケース
    return fibo(n - 1) + fibo(n - 2);  // 再帰ステップ
}
```

##### 例3:ユークリッドの互除法(最大公約数を求める関数)

```cpp
int GCD(int a, int b) {
    if (b == 0) return a;  // ベースケース
    return GCD(b, a % b);  // 再帰ステップ
}
```

##### 例4:文字列の回文判定

```cpp
bool is_palindrome(const string &s, int left, int right) {
    if (left >= right) return true;  // ベースケース
    if (s[left] != s[right]) return false;  // ベースケース
    return is_palindrome(s, left + 1, right - 1);  // 再帰ステップ
}
```

#### 注意点

- 再帰関数は強力だが、理解が難しい場合もある
- 再帰呼び出しの連鎖に終わりがないと無限ループになる
- 場合によってはループ構文の方が簡潔に書ける

#### 再帰関数とループ構文の比較

- 多くの場合、再帰関数はループ構文で書き換えられる
- 例：sumをループで実装

```cpp
int sum(int n) {
    int s = 0;
    for (int i = 0; i <= n; i++) {
        s += i;
    }
    return s;
}
```

#### 再帰関数とループ構文の使い分け

- 再帰関数
  - 問題を小さな問題に分割できる場合
  - コードが簡潔になる場合
- ループ構文
  - 単純な繰り返し処理の場合
  - 効率を重視する場合(再帰は関数呼び出しのオーバーヘッドがある)

#### 再帰関数の注意点

- スタックオーバーフロー
  - 再帰の深さが深くなりすぎると発生
  - 関数呼び出しごとにメモリを消費するため
- 無限ループ
  - ベースケースに到達しない場合に発生
  - 再帰の終了条件を適切に設定することが重要

#### 再帰関数の最適化

- 末尾再帰
  - 再帰呼び出しが関数の最後の操作である場合
  - コンパイラによっては最適化されループと同等の効率になる可能性がある

```cpp
int sum_tail(int n, int acc = 0) {
    if (n == 0) return acc;
    return sum_tail(n - 1, acc + n);
}
```

#### 再帰関数の効率

- 再帰関数は直感的に書けるが、効率が悪くなる場合がある
- 特に、同じ計算を何度も行う場合は非効率

##### 例：非効率なフィボナッチ数列の計算

```cpp
int fibo(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fibo(n - 1) + fibo(n - 2);
}
```

この実装では、nが大きくなると計算時間が指数関数的に増加する

#### 再帰関数の最適化

##### メモ化(動的計画法)

- 計算結果を記憶しておき、同じ計算を避ける手法

```cpp
vector<int> memo(50, -1);  // メモ用の配列

int fibo(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    if (memo[n] != -1) return memo[n];  // 計算済みならその値を返す
    memo[n] = fibo(n - 1) + fibo(n - 2);
    return memo[n];
}
```

#### 相互再帰

相互再帰とは、複数の関数が互いに呼び出し合う再帰のパターンです。

##### 特徴

1. 2つ以上の関数が互いに呼び出し合う
2. それぞれの関数が別々のベースケースを持つ
3. 問題を複数の部分問題に分割できる場合に有効

##### 例:偶数・奇数の判定

```cpp
bool is_even(int n) {
    if (n == 0) return true;  // ベースケース
    return is_odd(n - 1);     // 相互再帰
}

bool is_odd(int n) {
    if (n == 0) return false;  // ベースケース
    return is_even(n - 1);     // 相互再帰
}
```

##### 動作原理

1. `is_even(n)`は`n`が0なら真、そうでなければ`n-1`が奇数かどうかを判定
2. `is_odd(n)`は`n`が0なら偽、そうでなければ`n-1`が偶数かどうかを判定
3. これらの関数が交互に呼び出され、最終的にベースケースに到達する

##### 利点

1. 問題を自然な形で分割できる
2. コードが直感的で理解しやすい場合がある

##### 注意点

1. スタックオーバーフローの可能性がある(深い再帰の場合)
2. 両方の関数を事前に宣言(プロトタイプ宣言)する必要がある

#### 再帰関数の応用

- 木構造の探索
- バックトラッキング
- 分割統治法

### 計算量

- プログラム実行には処理に応じた時間がかかる
- メモリは有限で、変数使用に応じて消費される
- 時間計算量・空間計算量：入力に対する実行時間・メモリ使用量の変化
- オーダー記法：計算量の表記方法

#### アルゴリズム

- 計算手順のこと
- 同じ問題に対して複数のアルゴリズムが存在することがある
- 計算回数の少ないアルゴリズムを選ぶことで高速化が可能

#### オーダー記法

- O(・)で表記
- 係数を省略し、最も影響の大きい項のみを残す
- 例
    - 3N^2 + 7N + 4 → O(N^2)
    - 2N + 10 → O(N)

#### 計算量の例

##### O(1)の例

```cpp
int main() {
    int N;
    cin >> N;
    int sum = N * (N + 1) / 2;
    cout << sum << endl;
}
```

##### O(N)の例

```cpp
int main() {
    int N;
    cin >> N;
    vector<int> a(N);
    for (int i = 0; i < N; i++) {
        cin >> a.at(i);
    }
    int cnt = 0;
    for (int i = 0; i < N; i++) {
        if (a.at(i) % 2 == 0) {
            cnt++;
        }
    }
    cout << cnt << endl;
}
```

##### O(N^2)の例

```cpp
int main() {
    int N;
    cin >> N;
    vector<vector<int>> table(N, vector<int>(N));
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            table.at(i).at(j) = (i + 1) * (j + 1);
        }
    }
    // 出力省略
}
```

##### O(N log N)の例

マージソートなどの効率的なソートアルゴリズムの計算量。

```cpp
void merge_sort(vector<int>& arr, int left, int right) {
    if (left >= right) return;
    int mid = left + (right - left) / 2;
    merge_sort(arr, left, mid);
    merge_sort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}
```

##### O(2^N)の例

フィボナッチ数列の再帰的な計算(非効率な実装)

```cpp
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

#### 注意点

- 計算量は厳密な値ではなく、大まかな傾向を示す
- 同じ計算量でも、係数によって実際の実行時間は異なる
- 入力サイズが小さい場合、計算量の差が実行時間に大きく影響しないことがある

#### 計算量の比較

一般的に、計算量の大小関係は以下のようになる。

O(1) < O(log N) < O(N) < O(N log N) < O(N^2) < O(2^N) < O(N!)

#### 計算量の改善方法

- アルゴリズムの選択：より効率的なアルゴリズムを選ぶ
- データ構造の最適化：適切なデータ構造を使用する
- メモ化：計算結果を記憶して再利用する
- 不要な計算の削除：冗長な処理を避ける

## 第3章:競技プログラミングに役立つ知識

### 数値型

#### 整数型の範囲

- int型の範囲: -2,147,483,648 から 2,147,483,647
- int64_t型の範囲: -9,223,372,036,854,775,808 から 9,223,372,036,854,775,807

#### オーバーフロー

計算の途中で扱える範囲を超えることをオーバーフローといい、正しく計算が行えなくなる。

```cpp
int a = 2000000000;
int b = a * 2; // オーバーフロー発生
cout << b << endl; // -294967296 (誤った結果)
```

#### int64_t型の使用

int型より大きい値を扱いたいときはint64_t型を使う。

```cpp
int64_t a = 2000000000;
int64_t b = a * 2;
cout << b << endl; // 4000000000 (正しい結果)
```

#### リテラルの表記

int64_t型のリテラルには末尾に'LL'をつける。

```cpp
cout << 2000000000LL * 2LL << endl; // int64_t * int64_t -> int64_t
```

#### double型の出力精度指定

double型を出力する場合、通常通りcoutで出力してしまうと適当な桁で四捨五入されて表示されてしまう。途中の桁まで四捨五入せずに確実に表示したい場合、以下のように書く。

```cpp
cout << fixed << setprecision(桁数);
cout << 3.14159265358979 << endl;
```

- double型の精度は約16桁
- 情報落ちと桁落ちに注意(大きな数と小さな数の演算、近い値同士の引き算)

#### 型変換(キャスト)

- 明示的キャスト:`(型)値`
- 暗黙的キャスト:異なる型同士の演算時に自動的に行われる

```cpp
int a = 5;
cout << (double)a << endl; // int型をdouble型に変換

double b = 3.141592;
cout << (int)b << endl; // double型をint型に変換(小数点以下切り捨て)
```

#### 暗黙的キャストのルール

- int型とdouble型 → double型
- int型とint64_t型 → int64_t型
- double型とint64_t型 → double型

#### double型の精度と誤差

##### 精度の限界

- double型は約16桁の数字の並びを保持できる
- 16桁を超える小数は正確に扱えない

###### 情報落ち

- 極端に差が大きい2つの数の足し算で発生
- 小さい方の数の情報が失われる
- 対策：なるべく小さい数から順に足し算を行う

```cpp
double x = 1000000000;
double y = 0.000000001;
// 1000000000.000000001 を表現するには19桁分必要 → 扱えない
double z = x + y; // yの情報が失われる


cout << fixed << setprecision(16);
cout << "x: " << x << endl;
cout << "y: " << y << endl;
cout << "z: " << z << endl;
```

実行結果

```
x: 1000000000.0000000000000000
y: 0.0000000010000000
z: 1000000000.0000000000000000
```

##### 桁落ち

- 極端に差が小さい2つの数の引き算で発生
- 計算結果の精度が落ちる
- 対策
  - 引き算の差が大きくなるように計算順序を工夫
  - 引き算をなるべく行わないように工夫

#### printfでの出力

- coutの代替として使用可能
- 精度指定や多数の値の出力に便利

```cpp
int x = 12345;
double pi = 3.141592653589793;
printf("x = %d, pi = %.10f\n", x, pi);
```

- printf関数の主な書式指定子
    - %d：int型
    - %ld(%lld)：int64_t型
    - %lf：float型、double型
    - %c：char型
    - %s：string型(C言語形式の文字列)

#### scanfでの入力

- `scanf`関数を使用して入力を受け取ることができる
- `cin`よりも高速だが、安全性に欠ける面がある

```cpp
int x;
scanf("%d", &x);
```

書式指定子は基本的にはprintf関数と同じ。

- 注意点
    - `&`をつけ忘れないよう注意
    - string型の変数に入力する場合は特別な処理が必要

#### 文字列との変換

##### 数値から文字列への変換

`to_string`関数を使用する。

```cpp
int num = 123;
string s = to_string(num);  // "123"
```

##### 文字列から数値への変換

- 整数型への変換：`stoi`関数(string to integer)
- 浮動小数点型への変換：`stod`関数(string to double)

```cpp
string s1 = "123";
int num1 = stoi(s1);  // 123

string s2 = "3.14";
double num2 = stod(s2);  // 3.14
```

#### 数値の範囲を表す定数

`<limits>`ヘッダを使用して、各数値型の最大値と最小値を取得できる。

```cpp
#include <limits>
cout << numeric_limits<int>::max() << endl;  // intの最大値
cout << numeric_limits<int>::min() << endl;  // intの最小値
```

### pair/tupleとauto

#### pair

pair型は2つの値の組を表す。

```cpp
// 宣言・初期化
pair<string, int> p("abc", 3);

// アクセス
cout << p.first << endl;  // "abc":1つ目の値
cout << p.second << endl;  // 3:2つ目の値

// 生成
p = make_pair("*", 1);

// 分解
string s;
int a;
tie(s, a) = p;
cout << s << endl;  // *
cout << a << endl;  // 1
```

#### tuple

tuple型は複数個の値の組を表す。

```cpp
// 宣言・初期化
tuple<int, string, bool> data(1, "hello", true);

// アクセス
cout << get<1>(data) << endl;  // "hello":1番目にアクセス

// 生成
data = make_tuple(2, "WORLD", true);

// 分解
int a;
string s;
bool f;
tie(a, s, f) = data;
cout << a << " " << s << " " << f << endl;  // 2 WORLD 1
```

#### pair/tupleの比較

比較は1番目の要素から順に行われる。

```cpp
pair<int, int> a(3, 1);
pair<int, int> b(2, 10);
if (a < b) {
    cout << "a < b" << endl;
} else {
    cout << "a >= b" << endl;
}
// 出力:a >= b
```

pairやtupleの配列をソートする場合も上記の比較順序でソートされる。

```cpp
vector<tuple<int, int, int>> a;
a.push_back(make_tuple(3, 1, 1));
a.push_back(make_tuple(1, 2, 100));
a.push_back(make_tuple(3, 5, 1));
a.push_back(make_tuple(1, 2, 3));
sort(a.begin(), a.end());

for (tuple<int, int, int> t : a) {
    int x, y, z;
    tie(x, y, z) = t;
    cout << x << " " << y << " " << z << endl;
}
```

```
// 出力
1 2 3
1 2 100
3 1 1
3 5 1
```

#### auto

型推論を行い、変数宣言を簡略化する。変数宣言、範囲for文、参照で使える。

```cpp
vector<int> c = {1, 2, 3};
for (auto elem : c) {
    cout << elem << endl; // elemはint型
}
```

#### 参照とauto

```cpp
int a = 12345;
auto &ref = a;  // aへの参照 `int &ref = a;`と書くのと同じ
vector<int> b = {1, 2, 3};
for (auto &elem : b) {
    elem *= 2;
}
```

#### ignore

pairやtupleを分解する際に、不要な要素を捨てることができる。

```cpp
pair<int, int> p(3, 5);
int right;
tie(ignore, right) = p; // 2番目の値だけ取り出す
cout << right << endl;  // 5

tuple<int, string, bool> tpl(2, "hello", false);
int x;
string s;
tie(x, s, ignore) = tpl; // 1番目の値、2番目の値だけ取り出す
cout << x << " " << s << endl;  // 2 hello
```

#### 型エイリアス

型に別の名前をつけることができる。

```cpp
using pii = pair<int, int>; // pair<int, int>型に pii という別名をつける
pii p = make_pair(1, 2);
cout << "(" << p.first << ", " << p.second << ")" << endl;  // (1, 2)

using vi = vector<int>; // intの1次元の型に vi という別名をつける
using vvi = vector<vi>; // intの2次元の型に vvi という別名をつける
int N = 10, M = 20;
vvi data(N, vi(M));  // N * M の2次元配列
```

#### 多次元配列での活用

型エイリアスを使用して、多次元配列の宣言を簡略化できる。

```cpp
using vi = vector<int>;
using vvi = vector<vi>;
using vvvi = vector<vvi>;

vvvi space(10, vvi(20, vi(30)));  // 10x20x30の3次元配列
```

#### typedef(古い方法)

型エイリアスの古い書き方。

```cpp
typedef pair<int, int> pii;
pii p = make_pair(1, 2);
cout << "(" << p.first << ", " << p.second << ")" << endl;  // (1, 2)
```

#### 注意点

- `auto`を過度に使用すると、コードの可読性が低下する場合がある
- 型エイリアスは適切な名前を付けることが重要
- `typedef`よりも`using`を使用することが推奨されている

### STLのコンテナ(標準テンプレートライブラリ)

- map
- queue
- priority_queue
- set
- multiset
- stack
- deque
- unordered_map
- unordered_set

#### map

- 連想配列や辞書と呼ばれるデータ構造
- キーと値のペアを保存

#### 宣言

```cpp
map<Keyの型, Valueの型> 変数名;
```

#### 主な操作

```cpp
map<string, int> score;

// 値の追加
score["Alice"] = 100;

// 値の削除
score.erase("Bob");

// 値へのアクセス
cout << score.at("Alice");

// 存在判定
if (score.count("Charlie")) {}

// 要素数の取得
cout << score.size();
```

#### ループ

```cpp
// Keyの値が小さい順にループ
for (pair<Keyの型, Valueの型> p : 変数名) {
  Keyの型 key = p.first;
  Valueの型 value = p.second;
  // key, valueを使う
}
```

autoを用いて簡潔に書くことができる。

```cpp
for (auto p : score) {
    cout << p.first << " => " << p.second << endl;
}
```

#### mapの[]演算子の注意点

- 意図しない要素の追加を避けるため、基本的には`.at()`を使用することが推奨される

```cpp
map<string, int> score;
cout << score["Alice"] << endl;  // 0(新しい要素が作成される)
```

#### queue

- キューや待ち行列と呼ばれるデータ構造
- 先入れ先出し(FIFO)の原則で動作

#### 宣言

```cpp
queue<型> 変数名;
```

#### 主な操作

```cpp
queue<int> q;

// 要素の追加
q.push(10);

// 先頭要素へのアクセス
cout << q.front();

// 先頭要素の削除
q.pop();

// 要素数の取得
cout << q.size();

// キューが空であるかを調べる
q.empty(); // キューが空ならtrueを返す
```

### priority_queue

- 優先度付きキューと呼ばれるデータ構造
- 最大の要素を効率的に取り出せる

#### 宣言

```cpp
priority_queue<型> 変数名;
```

#### 主な操作

```cpp
priority_queue<int> pq;

// 要素の追加
pq.push(10);

// 最大要素の取得
cout << pq.top();

// 最大要素の削除
pq.pop();

// 要素数の取得
cout << pq.size();

// キューが空であるかを調べる
pq.empty(); // キューが空ならtrueを返す
```

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    priority_queue<int> pq;
    pq.push(10);
    pq.push(3);
    pq.push(6);
    pq.push(1);

    // 空でない間繰り返す
    while (!pq.empty()) {
        cout << pq.top() << endl;  // 最大の値を出力
        pq.pop();  // 最大の値を削除
    }
}
```

```
// 出力
10
6
3
1
```

queueとpriority_queueは、要素を追加したり削除したりすることはできるが、途中の要素に直接アクセスすることはできない。

#### 最小値を取り出す優先度付きキュー

デフォルトでは最大値を取り出すが、最小値を取り出すように設定することもできる。

```cpp
priority_queue<型, vector<型>, greater<型>> 変数;
```

#### 使い分け

- map:キーと値のペアを管理する必要がある場合
- queue:データを追加した順序で処理する必要がある場合
- priority_queue:常に最大値(または最小値)を取り出す必要がある場合

#### queueとpriority_queueの制約

- 要素の追加と削除は可能だが、途中の要素に直接アクセスすることはできない
- 常に先頭(queueの場合)や最大値(priority_queueの場合)の要素にのみアクセス可能

#### priority_queueのカスタム比較関数

- デフォルトでは最大値を取り出すが、カスタム比較関数を使用して動作を変更できる

```cpp
auto comp = [](int a, int b) { return a > b; };
priority_queue<int, vector<int>, decltype(comp)> pq(comp);
```

#### 計算量の重要性

- コンテナの選択は、必要な操作の計算量を考慮して行うべき
- 例えば、最大値を頻繁に取り出す必要がある場合は、vectorよりもpriority_queueの方が効率的

#### その他のSTLコンテナ

- set:重複を許さない要素の集合
- multiset:重複を許す要素の集合
- stack:後入れ先出し(LIFO)のデータ構造

#### set

- 重複を許さない要素の集合を管理するコンテナ
- 要素の追加、削除、存在確認が高速(O(log N))

#### 宣言

```cpp
set<値の型> 変数名;
```

#### 主な操作

```cpp
// 値の追加
変数.insert(値);

// 値の削除
変数.erase(値);

// 所属判定
if (変数.count(値)) {
  //「値」が含まれる
}
else {
  //「値」は含まれない
}

// 要素数の取得
変数.size()

// 空であるかを調べる
変数.empty()  // 空ならtrueを返す

// 最小値の取得
*begin(変数)

// 最大値の取得
*rbegin(変数)
```

#### ループ

```cpp
for (auto value : 変数名) {
  // valueを使う
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    set<int> S;
    S.insert(3);
    S.insert(7);
    S.insert(8);
    S.insert(10);
    S.erase(7);

    cout << S.size() << endl;  // 3
    if (S.count(7)) {
        cout << "7 is in S" << endl;
    } else {
        cout << "7 is not in S" << endl;
    }

    for (auto x : S) {
        cout << x << " ";  // 3 8 10
    }
    cout << endl;
}
```

#### multiset

- setと似ているが、重複する要素を許容する
- 要素の個数を管理できる

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    multiset<int> MS;
    MS.insert(3);
    MS.insert(7);
    MS.insert(7);
    MS.insert(8);
    MS.insert(10);
    MS.erase(7);  // 7をすべて削除

    cout << MS.size() << endl;  // 3
    cout << MS.count(7) << endl;  // 0

    for (auto x : MS) {
        cout << x << " ";  // 3 8 10
    }
    cout << endl;
}
```

#### stack

- 後入れ先出し(LIFO)のデータ構造
- 最後に追加した要素のみにアクセス可能

#### 宣言

```cpp
stack<値の型> 変数名;
```

#### 主な操作

```cpp
// 値の追加
変数.push(値);

// 次の値へのアクセス
変数.top();

// 値の削除
変数.pop();

// 要素数の取得
変数.size();

// 空であるかを調べる
変数.empty();  // 空ならtrueを返す
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    stack<int> S;
    S.push(3);
    S.push(7);
    S.push(1);

    while (!S.empty()) {
        cout << S.top() << " ";  // 1 7 3
        S.pop();
    }
    cout << endl;
}
```

#### 使い分け

- set:重複を許さない集合が必要な場合
- multiset:重複を許す集合が必要な場合、または要素の個数を管理したい場合
- stack:最後に追加した要素のみを扱う必要がある場合

#### deque(デック)

- 両端キュー(double-ended queue)
- 先頭と末尾の両方から要素の追加・削除が可能

#### 宣言

```cpp
deque<値の型> 変数名;
```

#### 主な操作

```cpp
// 値の追加
変数.push_back(値);   // 末尾への値の追加
変数.push_front(値);  // 先頭への値の追加

// 値のアクセス
変数.front()  // 先頭の値へのアクセス
変数.back()   // 末尾の値へのアクセス
変数.at(i)  // i番目へのアクセス

// 値の削除
変数.pop_front();  // 先頭の要素の削除
変数.pop_back();   // 末尾の要素の削除

// 要素数の取得
変数.size();

// 空であるかを調べる
変数.empty();  // 空ならtrueを返す
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    deque<int> d;
    d.push_front(10);  // 先頭に追加
    d.push_back(20);   // 末尾に追加
    d.pop_front();     // 先頭を削除
    d.pop_back();      // 末尾を削除

    d.push_back(30);
    d.push_front(40);

    for (int x : d) {
        cout << x << " ";  // 40 30
    }
    cout << endl;
}
```

#### unordered_map

- ハッシュテーブルを使用した連想配列
- mapより高速だが、キーの順序は保持されない

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    unordered_map<string, int> um;
    um["apple"] = 5;
    um["banana"] = 3;
    
    cout << um["apple"] << endl;  // 5
    cout << um.count("cherry") << endl;  // 0
}
```

#### unordered_set

- ハッシュテーブルを使用した集合
- setより高速だが、要素の順序は保持されない

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    unordered_set<int> us;
    us.insert(5);
    us.insert(3);
    us.insert(5);  // 重複は無視される
    
    cout << us.size() << endl;  // 2
    cout << us.count(3) << endl;  // 1
}
```

#### lower_bound / upper_bound(STLの関数)

- ソート済みの範囲で二分探索を行う関数
- lower_bound:指定した値以上の最初の要素を返す
- upper_bound:指定した値より大きい最初の要素を返す

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  vector<int> a = {0, 10, 13, 14, 20};
  // aにおいて、12 以上最小の要素は 13
  cout << *lower_bound(a.begin(), a.end(), 12) << endl; // 13

  // 14 以上最小の要素は 14
  cout << *lower_bound(a.begin(), a.end(), 14) << endl; // 14

  // 10 を超える最小の要素は 13
  cout << *upper_bound(a.begin(), a.end(), 10) << endl; // 13
}
```

#### 使い方

```cpp
*lower_bound(配列.begin(), 配列.end(), 値)  // 「値」以上の最小の値
*upper_bound(配列.begin(), 配列.end(), 値)  // 「値」を超えるの最小の値
```

#### 空のコンテナに対する操作

- 多くの操作は空のコンテナに対しても安全
- ただし、front(), back(), pop()などは未定義動作を引き起こす可能性がある

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v;
    cout << v.size() << endl;  // 0
    v.push_back(1);  // OK
    
    queue<int> q;
    if (!q.empty()) {
        q.pop();  // 空でない場合のみpop
    }
    
    // 注意:以下は未定義動作
    // cout << v.front() << endl;  // 空のvectorのfrontにアクセス
    // q.pop();  // 空のqueueに対してpop
}
```

### 構造体

#### 構造体の概要

- 複数の型をまとめた新しい型を作成できる
- STLのpair/tupleも構造体を使って実装されている

#### 構造体の定義

```cpp
struct 構造体名 {
    型1 メンバ変数名1;
    型2 メンバ変数名2;
    // ...
};
```

#### 構造体の宣言と初期化

```cpp
構造体名 変数名;
構造体名 変数名 = {メンバ変数1の値, メンバ変数2の値, ...};
```

#### メンバ変数へのアクセス

```cpp
オブジェクト.メンバ変数;
```

#### メンバ関数の定義

```cpp
struct 構造体名 {
  返り値の型 メンバ関数名(引数の型1 引数名1, 引数の型2 引数名2, ...) {
    // 関数の内容
    //   (ここではメンバ変数に直接アクセスすることができる)
  }
};
```

#### メンバ関数の呼び出し

```cpp
オブジェクト.メンバ関数(引数1, 引数2, ...);
```


#### サンプルプログラム

```cpp
#include <bits/stdc++.h>
using namespace std;

struct MyPair {
    int x;
    string y;
    
    void print() {
        cout << "x = " << x << endl;
        cout << "y = " << y << endl;
    }
};

int main() {
    MyPair p = {12345, "Hello"};
    p.print();
    
    MyPair q = {67890, "APG4b"};
    q.print();
}
```

#### コンストラクタ

- オブジェクト作成時に自動的に呼ばれる特殊な関数
- 初期化処理を行うために使用
- 引数を取ることも可能
- 複数のコンストラクタを定義可能(オーバーロード)

#### コンストラクタの定義

```cpp
struct 構造体名 {
    構造体名() { /* 初期化処理 */ }
    構造体名(int x) { /* 引数を使った初期化処理 */ }
};
```

#### コンストラクタの呼び出し

- 通常の宣言：`構造体名 オブジェクト名;`
- 引数付きコンストラクタ：`構造体名 オブジェクト名(引数1, 引数2, ...);`
- 初期化リスト使用：`構造体名 オブジェクト名 = {引数1, 引数2, ...};`

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

struct MyPair {
  int x;
  string y;
  // コンストラクタ
  MyPair() {
    cout << "constructor called" << endl;
  }
};

int main() {
  MyPair p;  // ここでコンストラクタが呼ばれる
  p.x = 12345;
  p.y = "hello";
  cout << "p.x = " << p.x << endl;
  cout << "p.y = " << p.y << endl;
}
```

#### コピーコンストラクタ

-  関数の引数としてオブジェクトを渡す場合などの条件を満たした場合、コピーコンストラクタが呼ばれる
- 明示的に定義しない場合、デフォルトのコピーコンストラクタが自動生成される
- デフォルトのコピーコンストラクタは全てのメンバ変数を単純にコピーする

#### コピーコンストラクタの定義

```cpp
struct 構造体名 {
  // コピーコンストラクタ
  構造体名(const 構造体名 &old) {
    // コンストラクタの内容
    // (oldの内容を使って初期化などを行う)
  }
};
```

#### コピーコンストラクタが呼ばれる場合

- 関数の引数としてオブジェクトを渡す場合
- `構造体名 新オブジェクト = 既存オブジェクト;` の形で初期化する場合
- `構造体名 新オブジェクト(既存オブジェクト);` の形で初期化する場合

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

struct MyPair {
  int x;
  string y;
  // コンストラクタ
  MyPair() {
    cout << "normal constructor called" << endl;
  }
  // コピーコンストラクタ
  MyPair(const MyPair &old) {
    cout << "copy constructor called" << endl;
    x = old.x + 1;
    y = old.y + " new";
  }
};

int main() {
  MyPair p;  // ここでコンストラクタが呼ばれる
  p.x = 12345;
  p.y = "hello";
  cout << "p.x = " << p.x << endl;
  cout << "p.y = " << p.y << endl;

  MyPair q(p);  // コピーコンストラクタが呼ばれる
  cout << "q.x = " << q.x << endl;
  cout << "q.y = " << q.y << endl;

  MyPair r = q;  // コピーコンストラクタが呼ばれる
  cout << "r.x = " << r.x << endl;
  cout << "r.y = " << r.y << endl;
}
```

#### 構造体のネスト

- 構造体の中に別の構造体を含めることができる

```cpp
struct OuterStruct {
    int x;
    struct InnerStruct {
        string y;
    } inner;
};

OuterStruct obj;
obj.x = 10;
obj.inner.y = "Hello";
```

#### 構造体の配列

- 構造体の配列を作成することができる

```cpp
struct Point {
    int x, y;
};

Point points[3] = {{1, 2}, {3, 4}, {5, 6}};
```

#### 構造体のポインタ

- 構造体へのポインタを使用できる
- アロー演算子(->)を使ってメンバにアクセスする

```cpp
struct MyStruct {
    int x;
    void print() { cout << x << endl; }
};

MyStruct* ptr = new MyStruct;
ptr->x = 10;
ptr->print();
delete ptr;
```

#### 演算子オーバーロード

- 構造体に対して演算子の動作を定義できる機能
- 例：`+`, `-`, `*`, `/`, `==`, `<`, `>`など

#### メンバ関数としての演算子オーバーロードの定義

```cpp
struct 構造体の型 {
  返り値の型 operator演算子(引数の型 引数) {
    // 処理内容
  }
};
```

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

struct MyPair {
  int x;
  string y;
  // 別のMyPair型のオブジェクトをとって、x, yにそれぞれ+したものを返す
  // +演算子をオーバーロード
  MyPair operator+(const MyPair &other) {
    MyPair ret;
    ret.x = x + other.x;  // ここではint型の+演算子が呼ばれる
    ret.y = y + other.y;  // ここではstring型の+演算子が呼ばれる
    return ret;
  }
};

int main() {
  MyPair a = {123, "hello"};
  MyPair b = {456, "world"};

  // MyPair型の+演算子が呼ばれる
  MyPair c = a + b;

  cout << "c.x = " << c.x << endl;
  cout << "c.y = " << c.y << endl;
}
```

#### フリー関数としての演算子オーバーロードの定義

```cpp
返り値の型 operator演算子(引数の型1 引数1, 引数の型2 引数2) {
  // 処理内容
}
```

#### サンプルコード

```cpp
#include <bits/stdc++.h>
using namespace std;

pair<int, int> operator+(pair<int, int> a, pair<int, int> b) {
  pair<int, int> ret;
  ret.first = a.first + b.first;
  ret.second = a.second + b.second;
  return ret;
}

int main() {
  pair<int, int> a = {1, 2};
  pair<int, int> b = {3, 4};
  auto c = a + b;
  cout << c.first << ", " << c.second << endl;  // 4, 6
}
```

### ビット演算

#### ビットとビット列

- ビット：「0」か「1」の2通りの状態を表現できるデータの単位
- ビット列：ビットを複数並べたもの

#### ビット演算の種類

- AND演算 (&)：両方のビットが1の場合のみ1
- OR演算 (|)：少なくとも一方のビットが1の場合に1
- XOR演算 (^)：どちらか一方のビットが1の場合のみ1
- NOT演算 (~)：ビットを反転
- 左シフト演算 (<<)：ビット列を左にずらす
- 右シフト演算 (>>)：ビット列を右にずらす

#### ビット演算の使用例

- 集合の操作：ビット列で集合を表現し、演算で集合操作を行う
- 高速化：複数のビットをまとめて処理できる

#### C++でのビット演算：bitsetの使用


#### 宣言・初期化

```cpp
bitset<ビット数> 変数名;  // すべてのビットが0の状態で初期化される
bitset<ビット数> 変数名("ビット列(長さはビット数に合わせる)");  // 指定したビット列で初期化される
```

#### ビットの操作

```cpp
// 全てのビットを1にする
変数.set();

// 特定のビットを1にする
変数.set(1にする位置);

// 特定のビットの値を変更する
変数.set(位置, 値);

// 全てのビットを0にする
変数.reset();

// 特定のビットを0にする
変数.reset(0にする位置);

// 全てのビットを反転する
変数.flip();

// 特定のビットを反転する
変数.flip(反転する位置);

// 特定のビットが1になっているかを調べる
変数.test(位置);

// 全てのビットが1になっているかを判定する
変数.all();

// いずれかのビットが1になっているかを判定する
変数.any();

// 1のビットの個数を数える
変数.count();

// ビット列を出力する
cout << 変数;

// ビット列を文字列化する
変数.to_string();

// ビットに対するアクセス
変数[位置];
```
   
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    bitset<8> a("00011011");
    bitset<8> b("00110101");

    cout << "AND: " << (a & b) << endl;
    cout << "OR:  " << (a | b) << endl;
    cout << "XOR: " << (a ^ b) << endl;
    cout << "NOT a: " << (~a) << endl;
    cout << "Left shift a by 2: " << (a << 2) << endl;
    cout << "Right shift a by 1: " << (a >> 1) << endl;
}
```

#### 注意点

- ビット演算の演算子の優先順位に注意(括弧を使用して明示的に指定することを推奨)
- bitsetのビット数は定数でなければならない

#### ビット全探索

- ビット全探索の概念
   - N個の要素からなる集合の部分集合を全て列挙する手法
   - 2^N 通りの部分集合を効率的に探索できる

- ビット列による集合の表現
   - 各要素の有無を1ビットで表現
   - N個の要素をN桁の2進数で表現

#### ビット全探索の基本的な実装

```cpp
for (int bit = 0; bit < (1 << ビット数); bit++) {
    bitset<ビット数> s(bit);
    // (ビット列sに対する処理)
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  // 3ビットのビット列をすべて列挙する
  for (int tmp = 0; tmp < (1 << 3); tmp++) {
    bitset<3> s(tmp);
    // ビット列を出力
    cout << s << endl;
  }
}
```

実行結果

```
000
001
010
011
100
101
110
111
```

- 使用例
   - 組み合わせの全探索
   - 最適な部分集合の探索
   - 動的計画法との組み合わせ

#### bitsetと整数の相互変換

```cpp
// 整数からbitsetへの変換
bitset<ビット数> 変数名(整数);
```

```cpp
// bitsetから整数への変換
bitsetの変数.to_ullong();
```

#### 整数リテラルの2進数・16進数表記

- 2進数:`0b`プレフィックスを使用(例：`0b1010`)
- 16進数:`0x`プレフィックスを使用(例：`0xA`)

### その他の有用な機能

#### 文字コード

- コンピュータ内部では文字を数値として扱う
- ASCII文字コードが一般的に使用される

```cpp
cout << (int)'A' << endl;  // 65
cout << (char)65 << endl;  // A
```

#### char型の演算

- 四則演算や比較が可能

```cpp
for (int i = 0; i <= ('Z' - 'A'); i++) {
    cout << (char)('A' + i);
}
```

```
// 出力
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

- 比較の例

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  char c = 'X';
  if ('A' <= c && c <= 'Z') {
    cout << "YES" << endl;
  }
  else {
    cout << "NO" << endl;
  }
}
```

STLの関数を使うこともできる。

```cpp
isupper(文字); // 大文字の判定を行う
islower(文字); // 小文字の判定を行う
isdigit(文字); // 10進数の数字かどうかをチェックする
```

#### 大文字と小文字の変換

```cpp
(char)('x' + ('A' - 'a')); // 'X' 小文字→大文字
(char)('X' - ('A' - 'a')); // 'x' 大文字→小文字
```

STLの関数を使うこともできる。

```cpp
(char)toupper(文字); // 小文字→大文字
(char)tolower(文字); // 大文字→小文字
```

#### グローバル変数

- 関数の外で宣言された変数
- プログラム全体がスコープ

```cpp
#include <bits/stdc++.h>
using namespace std;

//グローバル変数
int number = 10;

int main() {
  cout << number << endl;
}
```

#### グローバル変数のスコープ

- プログラム全体
- 複数の関数をまたいで使うことができる

#### グローバル変数名の衝突

- 同じ名前のグローバル変数は宣言できない
- まれにSTLで定義しているグローバル変数と衝突することもあるので注意

#### const修飾子

- 変数を定数として扱う
- 「const修飾子を付けた変数」を使えば直接数値を書くこと無く、楽かつ安全にbitsetのビット数を指定できる

```cpp
const int MAX_SIZE = 100;
bitset<MAX_SIZE> bs;
```

#### 条件演算子(三項演算子)

- if文を短く書ける

```cpp
int min_value = (a < b) ? a : b;
```

#### 論理演算の実行順序

- `&&`と`||`は左から評価し、結果が確定したら中断

```cpp
if (x != 0 && 100 / x > 5) {
    // xが0の場合、100/xは評価されない
}
```

#### &&と||の展開

&&に関して以下の二つのプログラムはほとんど同じ意味になる。

```cpp
if (条件1 && 条件2) {
  処理1
}
else {
  処理2
}
```

```cpp
if (条件1) {
  if (条件2) {
    処理1
  }
  else {
    処理2
  }
}
else {
  処理2
}
```

||に関して以下の二つのプログラムはほとんど同じ意味になる。

```cpp
if (条件1 || 条件2) {
  処理1
}
else {
  処理2
}
```

```cpp
if (条件1) {
  処理1
}
else if (条件2) {
  処理1
}
else {
  処理2
}
```

#### マクロ

- プリプロセッサによるコード置換

#### 単純なマクロの記法

```cpp
#define マクロ名 置き換えるプログラム
```

```cpp
#define rep(i, n) for (int i = 0; i < (int)(n); i++)
```

マクロは引数を受け取ることもできる。

#### ラムダ式

- 関数内で関数を定義

#### ラムダ式の記法

```cpp
auto 関数名 = [](引数の型1 引数名1, 引数の型2, 引数名2, ...) { 関数の処理 };
```

```cpp
int main(){
    auto sum = [](int a, int b) { return a + b; };
    cout << sum(3, 4) << endl;  // 7   
}
```

#### ラムダ式の外の変数の利用

`[&]`と書くことでラムダ式の外の変数を利用できる。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {

  // 最大値を保持する変数
  int max_num = 0;

  // 今まで受け取った値の中から最も大きな値を返す関数
  auto update_max = [&](int n) {
    if (max_num < n) {
      max_num = n;
    }
    return max_num;
  };

  cout << update_max(5) << endl;
  cout << update_max(2) << endl;
  cout << update_max(10) << endl;
  cout << update_max(4) << endl;
}
```

```
// 出力
5
5
10
10
```

#### ラムダ式による再帰関数

ラムダ式で再帰呼び出しのある関数を定義する場合、autoではなくfunctionを型として指定する必要がある。次のプログラムは、0～Nの和を求める再帰関数sumをラムダ式で定義している。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  // 再帰関数の定義
  function<int(int)> sum = [&](int n) {
    if (n == 0) {
      return 0;
    }
    int s = sum(n - 1);
    return s + n;
  };

  cout << sum(3) << endl;
}
```

#### ラムダ式による再帰関数の記法

```cpp
function<返り値の型(引数の型1, 引数の型2, ...)> 関数名 = [&](引数の型1 引数名1, 引数の型2, 引数名2, ...) { 関数の処理 };
```

#### do-while文とnext_permutation

- 順列の全列挙
- next_permutation関数:「順列の全列挙」を行うための関数

#### next_permutation関数の使い方

```cpp
sort(配列変数.begin(), 配列変数.end());
do {
  // 順列に対する処理
} while (next_permutation(配列変数.begin(), 配列変数.end()));
```

```cpp
vector<int> v = { 2, 1, 3 };
sort(v.begin(), v.end());
do {
    // 1行で今の並び方を出力
    for (int x : v) {
        cout << x << " ";
    }
    cout << endl;
} while (next_permutation(v.begin(), v.end()));
```

```
// 出力
1 2 3 
1 3 2 
2 1 3 
2 3 1 
3 1 2 
3 2 1
```

#### goto文

- 多重ループからの脱出に便利

```cpp
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        if (condition) goto LOOP_END;
    }
}
LOOP_END:
// ループを抜けた後の処理
```

#### 注意点

多重ループからの脱出など一部の状況では使っても良いが、goto文が必要になるケースはほとんどないので、基本的には使わないほうが良い。

## 第4章:今まで説明していなかったこと




## 参考

- [AtCoder Programming Guide for beginners (APG4b)](https://atcoder.jp/contests/APG4b)