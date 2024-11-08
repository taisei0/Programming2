
##  プログラミングII　2024　課題レポート（第2回）

# 解答用紙 → 提出ファイルはこちら　
- 問題用紙をよく読み、この回答用紙にレポート記述して提出すること
- マークダウン記法を、しっかりプレビューして、記述ミスはすべて修正して完成させること


レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|A or B| 202124020 |  佐藤大聖 |

------

# 解答編

- それぞれの問題をよく読み、以下の項目に自分の言葉でしっかり記述する
- マークダウン記法を、しっかりプレビューして、記述ミスはすべて修正して完成させる
- 生成AIに頼らず、自分で考えて、自分の言葉で書くことに重要な意味がある

------

## **課題1. 関数の作成とスコープルールの理解**

### **問題 1-1: 温度変換関数**

**作成したpythonコード**

```python

ここにコードを書く
# 絶対零度の定義
absolute_zero_celsius = -273.15 # 摂氏
absolute_zero_fahrenheit = -459.67 # 華氏
# 摂氏 → 華氏 (Celsius to Fahrenheit)
def celsius_to_fahrenheit(celsius: float) -> float:
   return celsius * 1.8 + 32

# 華氏 → 摂氏 (Fahrenheit to Celsius)
def fahrenheit_to_celsius(fahrenheit: float) -> float:
   return (fahrenheit  - 32) / 1.8

# 関数合成: 摂氏 → 華氏 → 摂氏
def c_2_f_2_c(c: float) -> float:
   return  fahrenheit_to_celsius (celsius_to_fahrenheit(c))

# 合成: 華氏 → 摂氏 → 華氏
def f_2_c_2_f(f : float) -> float:
   return celsius_to_fahrenheit(fahrenheit_to_celsius(f))
  
```

**動作確認結果**
```
摂氏 → 華氏 → 摂氏: -273.15
華氏 → 摂氏 → 華氏: -459.66999999999996

動作確認：成功
動作確認：成功
```
**分析** 
摂氏と華氏の計算公式を使って変換して元の数値に戻す。

<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
データを入れずに計算や管理することができる。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
四捨五入をしてもっとわかりやすくすればいいと思った。
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

---

### **★チャレンジ問題 (1-1-aux)　長さ・重さの単位変換**

**作成したpythonコード**

```python

ここにコードを書く

```

**動作確認結果**
```

ここに実行結果を書く

```

**分析** 

<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  

<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

----

### **問題 1-2: スコープルールの確認**

**作成したpythonコード**

```python

ここにコードを書く

# グローバルスコープの変数
x = 24
def outer():
# outer関数内のローカル変数
    x = 12
    def inner():
        nonlocal x  # どの 'x'を意味するか？
        x += 1 # どの 'x' を 1 増加するか？
        print(f"Inner: {x}")  
    inner() # inner関数を実行
    print(f"Outer: {x}") # どの 'x'を意味するか？
    return inner # inner関数をリターンする：クロージャ（関数閉包）
# outer関数を実行
o = outer() # 何が出力されるか? それはなぜか？ 
o() # 何が出力されるか? それはなぜか？
print(f"Global: {x}") # どの 'x'を意味するか？
p = outer() # 何が出力されるか? それはなぜか？
p() # 何が出力されるか? それはなぜか？
print(f"Global: {x}") # どの 'x'を意味するか？
o() # 何が出力されるか? それはなぜか？
o() # 何が出力されるか? それはなぜか？
p() # 何が出力されるか? それはなぜか？
print(f"Global: {x}") # どの 'x'を意味するか？
```
**動作確認結果**
```
Inner: 13
Outer: 13
Inner: 14
Global: 24
Inner: 13
Outer: 13
Inner: 14
Global: 24
Inner: 15
Inner: 16
Inner: 15
Global: 24

```

**分析** 
プログラム全体からアクセスできる変数や関数のこと。

<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
スコープのなかで定義された変数はプログラムの中ならどこもで使うことができる。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  Globalxとlocalxをもっとわかりやすくしたらいいと思った。

<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

----


### **★チャレンジ問題 (1-2-aux)**　グローバルコンテキスト、ローカルコンテキストの仕組み


**作成したpythonコード**

```python

ここにコードを書く

```

**動作確認結果**
```

ここに実行結果を書く

```

**分析** 

<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  

<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

----
----

## **課題2. 関数プログラミング**

### **問題 2-1: 高階関数と部分関数**

**作成したpythonコード**

```python

ここにコードを書く

Three = 3
from functools import partial
# n が d の倍数かどうか
def divisible_by(n: int, d=Three) -> bool:
    return n % d == 0
# n の 10 進数表記に '3' が含まれるかどうか
def has_char(n: int, d=str(Three)) -> bool:
    return str(d) in str(n)
# n を m 倍する関数
def multiply_by(n: int, m=Three) -> int:
    return n * m
# m=3倍する部分関数
triples = partial (multiply_by, m=Three)
# 合成されたフィルタ関数：n が 3 の倍数かつ '3' を含む
def combined_filter(n: int) -> bool:
    return divisible_by(n) and has_char(n)
# 3の倍数かつ '3' を含む数を 3 倍する
def triple_three(numbers: list[int]) -> list[int]:
# 合成フィルタ関数を使用
    filtered_numbers = filter(combined_filter, numbers)
# 各要素を 3 倍する
    result = map (triples, filtered_numbers)
    return list(result)
# 動作確認
if __name__ == "__main__":
    numbers = list(range(1, 100))
    result = triple_three(numbers)
    print(f"Result: {result}")

**動作確認結果**
[9, 90, 99, 108, 117, 189, 279]

ここに実行結果を書く

```

**分析** 
partialやfilter,mapなどの関数を使い、関数を引数として渡すようにしている。
<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
自分自身を呼び出すことによって、コードが短くなる。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  例外処理を加える
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

----

### **問題 2-2: デコレータの実装**

**作成したpythonコード**

```python

ここにコードを書く

import time
from functools import wraps

def timer(func):
    @wraps(func)  # 関数メタデータを保持するためのデコレータ
    def wrapper(*args, **kwargs):  # 実装する
        start_time = time.time()  # 開始時刻
        result = func(*args, **kwargs)  # 関数の実行
        end_time = time.time()  # 終了時刻
        execution_time = end_time - start_time  # 実行時間
        print(f"{func.__name__}の実行時間は{execution_time}秒です。")
        return result  # 実行結果をリターン
    return wrapper  

# デコレータを適用した関数
@timer
def example(sec: int = 1) -> None:
    time.sleep(sec)  # sec秒間待機
    print("関数が実行されました")

# テスト実行
if __name__ == "__main__":
    example(sec=2)
```
**動作確認結果**
```
関数が実行されました
exampleの実行時間は2.0023107528686523秒です。
```

**分析** 
デコレーターのタイマーを使うことにより、コードの実行時間表示を出している。
<!--
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
デコレーターのタイマーを関数で実行することで実行時間をだすことができる。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  音なども追加してアラームみたいにしたかった。
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->


----
----

## **課題3. プロトコルの実装**

### **問題 3-1: イテレータの実装**


**作成したpythonコード**

```python


ここにコードを書く

class FibonacciIterator:
    def __init__(self, size: int):
        # 初期化
        self.size = size  # 生成するフィボナッチ数の個数
        self.count = 0 # 何個目かを追跡
        self.a, self.b = 0, 1 # フィボナッチ数列の初期値（ゼロ始まりと仮定）
    
    def __iter__(self):
        # イテレータを返す
        return self
    
    def __next__(self):
        # 次のfibonacci数を返す
        if self.count >= self.size:
            raise StopIteration  # 指定件数に達したら停止
        current = self.a  # 現在のフィボナッチ数を返す
        self.a, self.b = self.b, self.a + self.b  # 次のフィボナッチ数へ更新
        self.count += 1 # カウントを進める
        return current # currentを返す

fib_iter = FibonacciIterator(20) # 20個のフィボナッチ数
for num in fib_iter:
    print(num, end=',')

**動作確認結果**
0,1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,1597,2584,4181,

ここに実行結果を書く

```

**分析** 
class FibonacciIteratorを使うことによってフィボナッチ数列を作って表している。
<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
暗号化を実装することができる。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
他の関数や技術を使ってもう少し文を短くする。

<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

---

### **問題 3-2: コンテキストマネージャの作成**

**作成したpythonコード**

```python

ここにコードを書く

class FileManager:
    def __init__(self, filename: str, mode: str):
        self.filename = filename
        self.mode = mode
        self.file = None # ファイルオブジェクトを初期化
    def __enter__(self):
        self.file = open(self.filename, self.mode) # ファイルを開く
        return self.file # ファイルオブジェクトを返す
    def __exit__(self, exc_type, exc_value, traceback):
        if self.file:
            self.file.close() # ファイルを閉じる

with FileManager('test.txt', 'w') as f:
    f.write('Hello, World!')

**動作確認結果**
test01.pyのファイルを作って実行したら、test.txtフォルダーができた。

ここに実行結果を書く

```

**分析** 
コンテキストマネージャーを実装することによって処理をしたことをテキストベースで報告するということ。
<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
_exit_メゾットの引数にはexc_type,exc_value,tracebackがあることによって例外を処理することができる。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
途中で実装することによって、エラーをテキストベースを出せると思った。
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

----
----

## **課題4. 再帰,lambda式**

### **問題 4-1: クイックソートの再帰的実装**
**作成したpythonコード**

```python

ここにコードを書く

def quiksort(arr: list[int]) -> list[int]:
    if len(arr) <= 1:
        return arr
   
    pivot = arr[0]
    les = [] # Initialize les as an empty list
    greater = []
    for x in arr[1:]:
        if x < pivot:
            les.append(x)
        else:
            greater.append(x)
    
    return quiksort(les) + [pivot] + quiksort(greater)
# 動作確認コード
import random
randoms = [random.randint(-20, 80) for _ in range(15)]
print(randoms)
# [44, 52, 70, -19, 8, -15, 37, 60, 52, 67, 47, 46, -19, 1, -9]
qs = quiksort(randoms)
print(qs)
# [-19, -19, -15, -9, 1, 8, 37, 44, 46, 47, 52, 52, 60, 67, 70]

**動作確認結果**
[67, 73, -7, 42, 43, 78, 56, 6, 11, 17, 79, 26, 52, 22, 31]
[-7, 6, 11, 17, 22, 26, 31, 42, 43, 52, 56, 67, 73, 78, 79]

ここに実行結果を書く

```

**分析** 
指定した大きい数、小さい数に分けることによって数字をきれいに並べ替えることができる。
<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
できるだけ真ん中の数を指定する

<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
端の方を選ばないように工夫する
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

----

### **問題 4-2: ハノイの塔の動作原理**
**作成したpythonコード**

```python

ここにコードを書く

def hanoi(n: int, source: str, target: str, auxiliary: str) -> None:
    if n == 1:
        print(f"ディスク {n} を {source} から {target}へ移動")
        return
    
    hanoi(n - 1, source, auxiliary, target)
    print(f"ディスク {n} を {source} から {target}へ移動")
    hanoi(n - 1, auxiliary, target, source)

hanoi(3, 'A', 'C', 'B')

**動作確認結果**
ディスク 1 を A から Cへ移動
ディスク 2 を A から Bへ移動
ディスク 1 を C から Bへ移動
ディスク 3 を A から Cへ移動
ディスク 1 を B から Aへ移動
ディスク 2 を B から Cへ移動
ディスク 1 を A から Cへ移動

ここに実行結果を書く

```

**分析** 
再帰的、自分で自分を呼び出すこと
<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  
端の方に移して、数の低い方から高い方に移し替えること。
<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
見てもう少し分かりやすい工夫をできたらいいと思った
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->


----

### **★チャレンジ問題 (4-2-aux)　lambdaを使った関数プログラミング**
**多数の英単語をカウント、ソートするlambda関数プログラミング**

**作成したpythonコード**

```python

ここにコードを書く

```

**動作確認結果**
```

ここに実行結果を書く

```

**分析** 

<!-- 
出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

**考察**  

<!-- 
  - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
  - 用いた技法、例えば、関数プログラミングの利点、プロトコルの活用場面について、応用シーンを考察する
-->

**改善点**  
<!-- 
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->


----

## 所感、自由記述欄


