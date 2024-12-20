##  プログラミングII　2024　課題レポート（第4回） 

### レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|A| 20124020 | 佐藤大聖| 

### 選択する回答コース:  「ゆるふわ」コース

**コース選択：アプローチの違い（道筋の険しさ）によって難易度・努力値を考慮する**
- **骨太コース：SA級**：生成AIを使わず，ノーヒントで自力で解く骨太な勇者・猛者・トリックスターコース
- **庶民コース：AB級**：生成AIを使わず，ヒントにしたがってアプローチする一般的コース
- **ゆるふわコース：CD級**：生成AIや他力本願を前提とするゆったりコース


----

# 回答用紙 → 提出ファイルはこの様式を使うこと
- 問題用紙をよく読み、この回答用紙にレポート記述して提出すること
- マークダウン記法を、しっかりプレビューして、記述ミスはすべて修正して完成させること
レポート提出者：

# 学生による回答編
- それぞれの問題をよく読み、以下の項目に自分の言葉でしっかり記述する
- マークダウン記法を、しっかりプレビューして、記述ミスはすべて修正して完成させる
- 生成AIに頼らず、自分で考えて、自分の言葉で書くことに重要な意味がある

------

### **問題1: シングルトンと属性制約を保証するメタクラスの設計**
- **概要**: メタクラスを使い、下記要件を満たす「AppConfigクラス」を**空欄を埋めて**設計せよ:
- **要件**
  - シングルトンパターン: クラスのインスタンスは1つしか生成できない
  - 属性制約: クラス内の属性名に制約:「属性名はすべて小文字」を課す
  - デフォルト値: 属性が指定されていない場合にデフォルト値を自動設定
- **課題**:
  1. **コード設計**:  空欄を埋めて、コードを完成させよ
  2. **分析**: なぜこの設計が有用か？実行結果の確認と検証
  3. **考察**: メタクラスを用いることで得られる利点を論じる

---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

class SingletonMeta(type):   ## 空欄A
    """Singleton を強制するメタクラス"""
    _instances = {}　　　　　

    def __call__(cls, *args, **kwargs):  ## 空欄B 
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class AttributeConstraintMeta(type):  
    """属性名がすべて小文字で命名されることを保証するメタクラス"""
    def __new__(cls, name, bases, dct):
        for attr_name in dct:
            if not attr_name.islower() and not attr_name.startswith("__"):    ## 空欄C
                raise TypeError(f"Attribute '{attr_name}' in class '{name}' must be in lowercase.")
        return super().__new__(cls, name, bases, dct)

class DefaultValuesMeta(type):
    """属性のデフォルト値を自動設定するメタクラス"""
    DEFAULT_VALUES = {
        'database': 'sqlite'
    }
    def __call__(cls, *args, **kwargs):
        instance = super().__call__(*args, **kwargs)
        for attr, default in cls.DEFAULT_VALUES.items():
            if not hasattr(instance, attr) or getattr(instance, attr) is None:
                setattr(instance, attr, default)
        return instance

##  """Singleton, Attribute Constraints, and Default Valuesを合成したメタクラス""" 
class CombinedMetaClass(SingletonMeta,AttributeConstraintMeta,DefaultValuesMeta):  ## 空欄D
    pass

class AppConfig( metaclass = CombinedMetaClass ):   ## 空欄E
    app_name = "MyApplication"  # 有効（小文字）
    version = "1.0"     # 有効（小文字）
    Port = 8080         # 無効（小文字でないためエラー）
    database = None     # 有効

# インスタンス生成
configA = AppConfig()
configB = AppConfig()

# 同一インスタンス(シングルトン)を確認
assert configA is configB
print(configA,configB)

# 属性デフォルト値の設定を確認
print(configA.database)  # デフォルト値として "sqlite" を出力

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

<main.AppConfig object at 0x000002B39EA1E390> <main.AppConfig object at 0x000002B39EA1E390>
sqlite

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-メタクラスは、クラスの生成や振る舞いをカスタマイズするための仕組み
-
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-設定ファイル管理やリソース管理に役立つ
-
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-エラーメッセージをさらに詳しくして、どの属性が問題なのかを明確化する
-
-

---
---

### **問題2: 「チューリングマシンの停止問題」「万能デバッガが存在しない理由」**
- **課題**:  
- メタ循環インタプリタに関係する「チューリングマシンの停止問題」について、
- 講義中に説明した比喩「どんなバグもみつける完璧なデバッガが存在しない」を交えて
- 理解したことを自分の言葉で説明せよ
- **考察**: 
- あわせて「ゲーデルの不完全性定理」をふまえてどんな教訓を示しているか分析・考察せよ
 
---

**説明・分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-すべてのプログラムを正確に判定することは論理的に不可能
-
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-「チューニングマシンの停止問題」と「ゲーテルの不完全性処理」は、人間の作るシステムには限界があるということを学ぶことができる
-
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-複雑な議論を直感的に理解できるようにする
-
-

---
---

### **問題3: オブザーバパターンを保証するメタクラスの設計**
- **概要**: メタクラスを使い、特定のクラスが「モデル（Observable）」として動作し、他の「オブザーバ（Observer）」に変更を通知する仕組みを確実に実施するサンプルコード設計を**空欄を埋めて**完成させよ
  
- **要件**
1. **`ObserverMeta` メタクラス**  
   - Observable クラスが必ず、 `add_observer`、`remove_observer`、`notify_observers` メソッドを持つことを強制し、実装されていない場合、例外をスローする

2. **`Observable` クラス**  
   - `ObserverMeta`メタクラスを適用した**基底クラス**で、観察される対象を管理する仕組みを提供、オブザーバを登録・解除し、状態変化時に通知する

3. **`Observer` クラス**  
   - `update` メソッドを持つ**抽象基底クラス**で、具体的なオブザーバクラスが継承して実装

4. **具体例（`TemperatureModel` と `TemperatureDisplay`）**  
   - `TemperatureModel` は(温度という)状態を持つモデルで、`temperature` プロパティが変更されると自動的にオブザーバへ通知
   - `TemperatureDisplay` はモデルから通知を受け取り、画面に表示を更新するオブザーバの具体例
   - 観察対象モデル（`TemperatureModel`）の状態変更がオブザーバ(`TemperatureDisplay`)に確実に通知される仕組みが可能
 
- **課題**:
  1. **コード設計**:  空欄を埋めて、コードを完成させよ
  2. **分析**: なぜこの設計が有用か？実行結果の確認と検証
  3. **考察**: メタクラスを用いることで得られる利点を論じる

---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

# **ObserverMeta メタクラス**  
class ObserverMeta(type):       #  
    """
    - Observable クラスが必ず、`add_observer`、`remove_observer`、`notify_observers` メソッドを持つことを強制する
    - 実装されていない場合、エラーをスローする
    """
    def __new__(cls, name, bases, dct):
        required_methods = { "add_observer", "remove_observer", "notify_observers" }
        implemented_methods = set(dct.keys()).union(*(set(dir(base)) for base in bases))
        if not required_methods.issubset(implemented_methods):
            missing = required_methods - implemented_methods
            raise TypeError(f"Class {name} is missing required methods: {','.join(missing)}")
        return super().__new__(cls, name, bases, dct)  

# **Observable クラス**  
class Observable(metaclass=ObserverMeta):     #  
    """
      - `ObserverMeta`メタクラスを適用した**基底クラス**: 観察される対象を管理する仕組みを提供
      - オブザーバを登録・解除し、状態変化時に通知する
    """
    def __init__(self):
        self._observers = []

    def add_observer(self, observer):
        if observer not in self._observers:
            self._observers.append(observer)    #  

    def remove_observer(self, observer):
        if observer in self._observers:
            self._observers.remove(observer)    #  

    def notify_observers(self):
        for observer in self._observers:
            observer.update(self)               

# **Observer クラス**  
class Observer:
    """
     - `update` メソッドを持つ**抽象基底クラス**で、具体的なオブザーバクラスが継承して実装
    """
    def update(self, observable):
        raise NotImplementedError("The 'update' method must be implemented by subclasses.")

## 観察者(View)の具体例
class TemperatureDisplay(Observer):
    def update(self, observable):
        if isinstance(observable, TemperatureModel):
            print(f"[Display] Model updated to {observable.temperature}°C [Display]")

class TemperatureBrowser(Observer):
    def update(self, observable):
        if isinstance(observable, TemperatureModel):
            print(f"<Web> Model updated to {observable.temperature}°C</Web>")

## 観察対象(Model)の具体例
class TemperatureModel(Observable):     #  
    def __init__(self):
        super().__init__()
        self._temperature = 0

    @property
    def temperature(self):
        return self._temperature

    @temperature.setter
    def temperature(self, value):
        self._temperature = value
        self.notify_observers()     #  

def test():
    # 観察対象　Model
    model = TemperatureModel()
    # 観察者　View
    display = TemperatureDisplay()
    view = TemperatureBrowser()

    #  オブザーバの割り当て
    model.add_observer(display)
    model.add_observer(view)

    #  モデルのアップデート
    model.temperature = 25
    model.temperature = 30

    #  オブザーバの解除
    model.remove_observer(display)
    model.temperature = 35

    #  オブザーバの再割り当て
    model.add_observer(display)
    model.temperature = 44

test()

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

[Display] Model updated to 25°C [Display]
<Web> Model updated to 25°C</Web>
[Display] Model updated to 30°C [Display]
<Web> Model updated to 30°C</Web>
<Web> Model updated to 35°C</Web>
<Web> Model updated to 44°C</Web>
[Display] Model updated to 44°C [Display]

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-メゾット不足による設計ミスを防止
-通知機能を効率的に実現しており、柔軟性が高い
-観察者の実装が容易かつ統一的に行える設計を採用している
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-異なるモデルやビューに組み合わせにも対応可能
-過剰な責務を持たせずシンプルな構造をたもっている
-拡張時のエラーを防ぎやすい

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-すでに削除されたオブザーバーに通知を送らない仕組みを加える
-
-

-----
-----


### **問題4: メタクラスではなく、`__init_subclass__()`で代用する方法**
- **課題**: 問題３をシンプルに、`__init_subclass__()`で代用するコードを**空欄を埋めて**完成させよ



---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

class Observable:
    def __init__(self):
        self._observers = []  # 

    def add_observer(self, observer):
        if observer not in self._observers:
            self._observers.append(observer)

    def remove_observer(self, observer):
        if observer in self._observers:
            self._observers.remove(observer)

    def notify_observers(self):
        for observer in self._observers:
            observer.update(self)  # 

    @classmethod
    def __init_subclass__(cls, **kwargs):  # 
        super().__init_subclass__(**kwargs)
        required_methods = {"add_observer", "remove_observer", "notify_observers"}  # 
        for method in required_methods:
            if not callable(getattr(cls, method, None)):
                raise TypeError(f"Class {cls.__name__} is missing required method: {method}")

# Sample Observer Class
class Observer:
    def update(self, observable):
        raise NotImplementedError("The 'update' method must be implemented by subclasses.")

# Example Implementation
class TemperatureModel(Observable):  # 
    def __init__(self):
        super().__init__()
        self._temperature = 0

    @property
    def temperature(self):
        return self._temperature

    @temperature.setter
    def temperature(self, value):
        self._temperature = value
        self.notify_observers()

class TemperatureDisplay(Observer):  # 
    def update(self, observable):
        if isinstance(observable, TemperatureModel):
            print(f"Temperature updated to {observable.temperature}°C")

def test():
    temp_model = TemperatureModel()
    display = TemperatureDisplay()

    temp_model.add_observer(display)

    temp_model.temperature = 25
    temp_model.temperature = 30

    temp_model.remove_observer(display)
    temp_model.temperature = 35

test()

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

Temperature updated to 25°C
Temperature updated to 30°C


```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-サブクラスが必須メゾット{"add_observer", "remove_observer", "notify_observers"}を持つことを__init_subclassでチェック
-通知する仕組みが簡潔に構築されている
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-メタクラスを使わずに__init_subclassを活用している点はシンプルで読みやすい
-他の用途や構成にも簡単に適応できる
-オブザーバーは変更箇所や内容を判断する柔軟性がない

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-変更内容を通知する仕組みを追加する
-オブザーバが特定のイベントを監視する仕組みを導入すると、効率的になると思った。
-

----
----

### **問題5: 自作パッケージとデプロイの実践
- **概要**: 自作パッケージを作って、デプロイし、他者が`pip insatll`や、`import`を使って活用できる状態にする
- 第12回の練習課題（プラクティスNo.1，No.2）を参考に、**自作パッケージを作ってデプロイするプラクティスNo.3**を実施する
- 簡単なユーティリティ関数を束ねたパッケージを自作する
- 例えば、次のような簡単な関数や、その他有用な関数を追加する：
- 

    - 1. BMI計算関数: 身長と体重を入力として受け取り、BMI（Body Mass Index）を計算して返す関数 : `calculate_bmi(weight, height)`
    - 2. 温度変換関数: 摂氏温度を華氏温度に変換する関数:`celsius_to_fahrenheit(celsius)`と、その逆変換:`fahrenheit_to_celsius(fahrenheit)`
    - 3. 単語カウント関数: テキスト内の単語数をカウントする関数:`count_words(text)`
    - 4. リストの平均値計算関数:`calculate_average(numbers)`
    - 5. 素数判定関数:`is_prime(number)`
    - 6. フィボナッチ数列生成関数:` generate_fibonacci(n)`
    - 7. 文字列の逆順関数:`reverse_string(s)`
    - 8. 最大公約数（GCD）計算関数:`gcd(a, b)`

----
---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

from datetime import datetime

# ==============================
# 文字列操作関連のユーティリティ
# ==============================

def reverse_string(s: str) -> str:
    """文字列を逆順にする"""
    return s[::-1]

def is_palindrome(s: str) -> bool:
    """文字列が回文かどうかを判定する"""
    s = s.lower().replace(" ", "").replace(",", "").replace(".", "")
    return s == s[::-1]

# ==============================
# 日付操作関連のユーティリティ
# ==============================

def get_current_date() -> str:
    """現在の日付を 'YYYY-MM-DD' の形式で取得する"""
    return datetime.now().strftime("%Y-%m-%d")

def days_between(date1: str, date2: str) -> int:
    """2つの日付の間の日数を計算する (日付は 'YYYY-MM-DD' の形式)"""
    d1 = datetime.strptime(date1, "%Y-%m-%d")
    d2 = datetime.strptime(date2, "%Y-%m-%d")
    return abs((d2 - d1).days)

# ==============================
# 数学計算関連のユーティリティ
# ==============================

def factorial(n: int) -> int:
    """nの階乗を計算する (n!)"""
    if n < 0:
        raise ValueError("n must be a non-negative integer.")
    return 1 if n == 0 else n * factorial(n - 1)

def fibonacci(n: int) -> int:
    """n番目のフィボナッチ数を計算する"""
    if n < 0:
        raise ValueError("n must be a non-negative integer.")
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

# ==============================
# エントリーポイント (動作確認用)
# ==============================

if __name__ == "__main__":
    # string_utils の動作確認
    print("==== String Utilities ====")
    print(reverse_string("hello"))  # 出力: "olleh"
    print(is_palindrome("A man a plan a canal Panama"))  # 出力: True

    # date_utils の動作確認
    print("\n==== Date Utilities ====")
    print(get_current_date())  # 現在の日付 (例: "2024-12-19")
    print(days_between("2024-01-01", "2024-12-31"))  # 出力: 365

    # math_utils の動作確認
    print("\n==== Math Utilities ====")
    print(factorial(5))  # 出力: 120
    print(fibonacci(10))  # 出力: 55


```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

==== Date Utilities ====
2024-12-19
365

==== Math Utilities ====
120
55

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-シンプルな引数と戻り値を持つため、再利用性が高い
-簡潔で分かりやすいDoctrngがつけられており、使用意図が明確
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-不正入力に対するエラーハンドリングがない
-コードの全体の動作確認用の出力が含まれているが、異常系や境界値のテストが不足している
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-各カテゴリごとにファイルを分割し機能が増えた際に保守性が向上する
-入力された場合にエラーを通知する仕組みを追加する
-正常系・異常系のテストを体力的に記述し、コードの品質を保証する

-----

### 所感・今後の目標課題 (自由記述欄、フィードバックご意見を尊重します)

- プログラミングに興味が湧かない原因
- プログラミングには興味がないが、それ以外で没頭していること
- 授業中に質問や意見が言えない理由
- コードや英語や文字、活字が好きにならない理由
- 私とプログラミング
- なぜプログラミングを学ぶのか？
- これまで学んだことを振り返り
- これからの学びに活かすべき知見
 
---




---

