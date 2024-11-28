##  プログラミングII　2024　課題レポート（第3回） 

### レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|A| 202124020 | 佐藤大聖 |
ゆるふわコース

### 選択する回答コース:  「〇〇」コース

- **骨太コース：SA級**：生成AIを使わず，ノーヒントで自力で解く骨太な勇者・猛者・トリックスターコース
- **庶民コース：AB級**：生成AIを使わず，ヒントにしたがってアプローチする一般的コース
- **ゆるふわコース：CD級**：生成AIや他力本願を前提とする ゆとりコース


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

### **問題1: ジェネレータを使ったコルーチンの設計と実装**
- **概要**: Pythonジェネレータを使って生産者-消費者問題を解決するコードを設計せよ
- **課題内容**:
  1. 要件：生産者コルーチンがデータを生成し、消費者コルーチンがデータを消費するコード
  2. `send`と`receive = yield`を用いた協調的並列処理の実装
  3. **分析**: なぜこの設計が必要か？実行結果の確認と検証
  4. **考察**: コルーチンを用いることで得られる効率性や設計上の利点を論じる
  5. **応用（チャレンジ）** 　ジェネレータに対する`StopIteration`例外を使うことで、生産者が生産を終了した後、消費者も消費を停止するコードに進化せよ

---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

import time
import random

# 生産者Coroutine: アイテムを生産し、消費者に渡す
def producer(consumer_coroutine):
    print("[生産者]: 生産開始...")
    consumer_coroutine.send(None)  # 消費者コルーチンの準備を開始
    for i in range(5):  # アイテムを5つ生産
        duration = random.uniform(0.5, 1.2)  # 生産にかかる時間をランダムに設定
        time.sleep(duration)  # 生産時間をシミュレート
        item = f"製品-{i + 1}"
        print(f"[生産者]: {duration:.2f}秒で {item} を生産")
        consumer_coroutine.send(item)  # 生産物を消費者に送る
    consumer_coroutine.close()  # 消費者のコルーチンを終了
    print("[生産者]: 生産完了")

# 消費者Coroutine: 生産者からアイテムを受け取り、消費処理を行う
def consumer():
    print("<消費者>: 準備完了...")
    try:
        while True:
            item = yield  # 生産物を受け取る
            print(f"<消費者>: {item} を受領。消費中...")
            duration = random.uniform(0.5, 1.2)  # 消費にかかる時間をランダムに設定
            time.sleep(duration)  # 消費時間をシミュレート
            print(f"<消費者>: {duration:.2f}秒で {item} を消費完了")
    except GeneratorExit:
        print("<消費者>: 消費を終了します。お疲れ様でした！")

# 実行部分
if __name__ == "__main__":
    consumer_coroutine = consumer()  # 消費者コルーチンのインスタンスを作成
    next(consumer_coroutine)  # コルーチンを準備状態にする
    producer(consumer_coroutine)  # 生産者を起動して消費者と連携

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

<消費者>: 準備完了...
[生産者]: 生産開始...
<消費者>: None を受領。消費中...
<消費者>: 0.51秒で None を消費完了
[生産者]: 1.19秒で 製品-1 を生産
<消費者>: 製品-1 を受領。消費中...
<消費者>: 1.12秒で 製品-1 を消費完了
[生産者]: 1.13秒で 製品-2 を生産
<消費者>: 製品-2 を受領。消費中...
<消費者>: 0.66秒で 製品-2 を消費完了
[生産者]: 0.62秒で 製品-3 を生産
<消費者>: 製品-3 を受領。消費中...
<消費者>: 0.77秒で 製品-3 を消費完了
[生産者]: 1.20秒で 製品-4 を生産
<消費者>: 製品-4 を受領。消費中...
<消費者>: 1.20秒で 製品-4 を消費完了
[生産者]: 0.79秒で 製品-5 を生産
<消費者>: 製品-5 を受領。消費中...
<消費者>: 1.13秒で 製品-5 を消費完了
<消費者>: 消費を終了します。お疲れ様でした！
[生産者]: 生産完了

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-
-複数のタスクを効率的に処理する際や非同期処理の基本を学ぶため
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-
-コルーチンを使用して、生産者と消費者が連携して処理を行う仕組みを表している。
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-
-他の技術を使ってもっと結果を見やすくできたらいいと思う。
-

---
---

### **問題2: 基本的なオブジェクト指向の例題**
- **概要**: 図形クラスとその派生クラスを設計し、オブジェクト指向の原則の理解度を確認する
- **課題内容**:
  1. 抽象基底クラス`Shape`を定義し、以下のクラスを継承して設計実装せよ
     - 四角形クラス`Rectangle`
     - 三角形クラス`Triangle`
     - 楕円クラス`Ellipse`
     - 五角形クラス`Pentagon`
  2. 各クラスに`rotate`メソッドを実装し、「指定角度（degree）だけ時計回りに回転させる」機能を追加しなさい（シミュレーションでよい、厳密な行列・ベクトルを用いた幾何学的回転の実装は不要）
  3. ポリモーフィズムの概念を用いた操作を記述せよ
  4. **考察**: 継承、抽象基底クラスによるインターフェースの強制、ポリモーフィズムのメリットと、設計上の効果を分析しなさい



---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

from abc import ABC, abstractmethod

# 抽象基底クラス Shape: rotate()メソッドを強制する
class Shape(ABC):
    @abstractmethod
    def rotate(self, angle):
        pass

# 2次元図形の基底クラス Shape2D
class Shape2D(Shape):
    def rotate(self, angle):
        print(f"{self.__class__.__name__} @ angle({self.angle}) rotated by ({angle}) degrees ->", end="")
        self.angle += angle
        self.angle %= 360
        print(f" to angle({self.angle})")

# 長方形クラス
class Rectangle(Shape2D):
    def __init__(self, width, height, angle=0):
        self.width = width
        self.height = height
        self.angle = angle

    def rotate(self, angle):
        print(f"Calculating rotation for Rectangle (width, height) = ({self.width}, {self.height}) @ angle({self.angle})")
        super().rotate(angle)

# 三角形クラス
class Triangle(Shape2D):
    def __init__(self, base, height, angle=0):
        self.base = base
        self.height = height
        self.angle = angle

    def rotate(self, angle):
        print(f"Calculating rotation for Triangle (base, height) = ({self.base}, {self.height}) @ angle({self.angle})")
        super().rotate(angle)

# 楕円クラス
class Ellipse(Shape2D):
    def __init__(self, major_axis, minor_axis, angle=0):
        self.major_axis = major_axis
        self.minor_axis = minor_axis
        self.angle = angle

    def rotate(self, angle):
        print(f"Calculating rotation for Ellipse (major, minor) = ({self.major_axis}, {self.minor_axis}) @ angle({self.angle})")
        super().rotate(angle)

# 五角形クラス
class Pentagon(Shape2D):
    def __init__(self, side_length, angle=0):
        self.side_length = side_length
        self.angle = angle

    def rotate(self, angle):
        print(f"Calculating rotation for Pentagon (side length) = {self.side_length} @ angle({self.angle})")
        super().rotate(angle)

# 図形インスタンスをリストにまとめる
shapes = [
    Rectangle(10, 5, angle=270),
    Triangle(6, 8, angle=90),
    Ellipse(5, 3, angle=330),
    Pentagon(7, angle=-180)
]

# ポリモーフィズムを活用して、図形を一括操作
for shape in shapes:
    shape.rotate(45)  # すべての図形を45度回転

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

Calculating rotation for Rectangle (width, height) = (10, 5) @ angle(270)
Rectangle @ angle(270) rotated by (45) degrees -> to angle(315)
Calculating rotation for Triangle (base, height) = (6, 8) @ angle(90)
Triangle @ angle(90) rotated by (45) degrees -> to angle(135)
Calculating rotation for Ellipse (major, minor) = (5, 3) @ angle(330)
Ellipse @ angle(330) rotated by (45) degrees -> to angle(15)
Calculating rotation for Pentagon (side length) = 7 @ angle(-180)
Pentagon @ angle(-180) rotated by (45) degrees -> to angle(225)

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-
-オブジェクト指向プログラミングの基本的なスキルだけでなく、実際のアプリケーション設計を想定した拡張性のあるコードを書く力を試している
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-
-抽象基底クラス (ABC) を用いて、共通のインターフェースを提供し、各図形クラスで具体的な実装を行っています。ポリモーフィズム の概念を利用して、異なる図形の型を意識せずに一括で操作している
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-
-複数回の回転や極端な入力値を含めたテストを追加する
-

---
---

### **問題3: **コマンド(Command)** デザインパターンの実装**
- **概要**: テキストエディタに対する編集操作と`Undo`/`Redo`機能をコマンドデザインパターンで実装せよ
- **課題内容**:
  1. 基本的なコマンドクラス`Command`を設計
  2. 具体的なコマンドとして、`InsertText`、`DeleteText`を実装しなさい（シミュレーションでよい）
  3. `Undo`/`Redo`機能を有効にする履歴管理を追加しなさい
  4. **考察**: コマンドパターンがもたらす柔軟性と拡張性について分析

---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

class Command:
    """コマンドクラスの共通インターフェース"""
    def execute(self):
        raise NotImplementedError("executeメソッドを実装してください。")
    
    def undo(self):
        raise NotImplementedError("undoメソッドを実装してください。")

class InsertText(Command):
    """テキスト挿入コマンド"""
    def __init__(self, document, text, position):
        self.document = document
        self.text = text
        self.position = position
    
    def execute(self):
        self.document.insert(self.text, self.position)
    
    def undo(self):
        self.document.delete(self.position, len(self.text))
    
    def __repr__(self):
        return f"InsertText('{self.text}' at {self.position})"
class DeleteText(Command):
    """テキスト削除コマンド"""
    def __init__(self, document, position, length):
        self.document = document
        self.position = position
        self.length = length
        self.deleted_text = ""
    
    def execute(self):
        self.deleted_text = self.document.content[self.position:self.position + self.length]
        self.document.delete(self.position, self.length)
    
    def undo(self):
        self.document.insert(self.deleted_text, self.position)
    
    def __repr__(self):
        return f"DeleteText('{self.deleted_text}' from {self.position})"

class Document:
    """テキストを管理するドキュメントクラス"""
    def __init__(self):
        self.content = ""
    
    def insert(self, text, position):
        self.content = self.content[:position] + text + self.content[position:]
        print(f"Inserted '{text}' at position {position}. Current content: '{self.content}'")
    
    def delete(self, position, length):
        self.content = self.content[:position] + self.content[position + length:]
        print(f"Deleted {length} characters at position {position}. Current content: '{self.content}'")

class CommandManager:
    """コマンドを管理し、Undo/Redo機能を提供するクラス"""
    def __init__(self):
        self.undo_stack = []
        self.redo_stack = []
    
    def execute_command(self, command):
        command.execute()
        self.undo_stack.append(command)
        self.redo_stack.clear()
    
    def undo(self):
        if self.undo_stack:
            command = self.undo_stack.pop()
            command.undo()
            self.redo_stack.append(command)
        else:
            print("Nothing to undo.")
    
    def redo(self):
        if self.redo_stack:
            command = self.redo_stack.pop()
            command.execute()
            self.undo_stack.append(command)
        else:
            print("Nothing to redo.")
# 使用例
if __name__ == "__main__":
    doc = Document()
    manager = CommandManager()

    cmd1 = InsertText(doc, "Hello", 0)
    manager.execute_command(cmd1)

    cmd2 = InsertText(doc, " World", 5)
    manager.execute_command(cmd2)

    cmd3 = DeleteText(doc, 6, 5)
    manager.execute_command(cmd3)

    print("\n--- Undo actions ---")
    manager.undo()
    manager.undo()

    print("\n--- Redo actions ---")
    manager.redo()

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

Inserted 'Hello' at position 0. Current content: 'Hello'
Inserted ' World' at position 5. Current content: 'Hello World'
Deleted 5 characters at position 6. Current content: 'Hello '

--- Undo actions ---
Inserted 'World' at position 6. Current content: 'Hello World'
Deleted 6 characters at position 5. Current content: 'Hello'

--- Redo actions ---
Inserted ' World' at position 5. Current content: 'Hello World'

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-
-コマンドデザインパターンの理解と実装能力を確認すること
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-
-コマンドパターン を使用し、ドキュメントに対する編集操作を実行、取り消し（Undo）、やり直し（Redo）する仕組みを実装している
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-
-安全性向上のため例外や不正な操作の防止をする
-

-----
-----

### **問題4: オブザーバ(Observer) デザインパターンの実装**
- **概要**: Pythonのダックタイピングを活用して**オブザーバパターン**を実装し、MVCモデルについて論じよ
- **課題内容**:
  1. `Observer`と`Subject`を設計し、観察者-被観察者関係を構築
  2. サンプルアプリとして簡易的なMVCモデルを実装
  3. 各コンポーネントの役割を論述
  4. **考察**: ダックタイピングの利点と、オブザーバパターンによる柔軟なシステム設計についてパターンを使わない場合と比較し，効能・使い道，論じる

---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

class Model:
    """データを管理するModelクラス"""
    def __init__(self, name):
        self._name = name
        self._data = None

    def set_data(self, data):
        self._data = data

    def get_data(self):
        return self._data

    def get_name(self):
        return self._name

    def serialize(self):
        return {"data": self._data}

    def deserialize(self, data):
        self._data = data["data"]

class Observer:
    """更新を通知されるObserverインターフェース"""
    def update(self, model):
        pass

class HTMLView(Observer):
    def update(self, model):
        print(f"<div> HTMLView: {model.get_name()} updated to {model.get_data()} </div>")

class CSVView(Observer):
    def update(self, model):
        print(f"CSVView,{model.get_name()},updated,to,{model.get_data()},")

class PDFView(Observer):
    def update(self, model):
        print(f"@PDFView: {model.get_name()} {model.get_data()} updated")

class GUIView(Observer):
    def update(self, model):
        print(f"□●GUIView: TEXT_FIELD:{model.get_name()} updated to {model.get_data()} CheckBox ✓")

class Subject:
    """モデルとビューを結びつけるSubjectクラス"""
    def __init__(self):
        self._observers = []

    def register_observer(self, observer):
        self._observers.append(observer)

    def unregister_observer(self, observer):
        self._observers.remove(observer)

    def notify_observers(self, model):
        for observer in self._observers:
            observer.update(model)

class Controller(Subject):
    """イベント処理を行うControllerクラス"""
    def __init__(self, model):
        super().__init__()
        self.model = model

    def set_data(self, data):
        self.model.set_data(data)
        self.notify_observers(self.model)

if __name__ == "__main__":
    # モデルの作成
    model1 = Model("Hero")
    model2 = Model("Ally")

    # 各種ビューの作成
    html_view = HTMLView()
    csv_view = CSVView()
    pdf_view = PDFView()
    gui_view = GUIView()

    # コントローラの作成
    controller1 = Controller(model1)
    controller2 = Controller(model2)

    # コントローラにビューを登録
    controller1.register_observer(html_view)
    controller1.register_observer(csv_view)
    controller2.register_observer(pdf_view)
    controller2.register_observer(gui_view)

    # データの変更と通知
    controller1.set_data("Attack Mode")
    controller2.set_data("Defense Mode")

    # ビューの登録解除後の動作
    controller1.unregister_observer(csv_view)
    controller1.set_data("Stealth Mode")

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

<div> HTMLView: Hero updated to Attack Mode </div>
CSVView,Hero,updated,to,Attack Mode,
@PDFView: Ally Defense Mode updated
□●GUIView: TEXT_FIELD:Ally updated to Defense Mode CheckBox ✓
<div> HTMLView: Hero updated to Stealth Mode </div>

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-
-実際のアプリケーション設計にも応用可能なスキルを身につける狙い
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-
-Observerデザインパターンの基本的な動作をシンプルに示している
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-
-安全性を高めるために、エラーを未然に防ぐ処理を加える
-

----
----

### **チャレンジ問題5: 非同期処理の実装と分析**　（骨太コース必須）
- **概要**: `async`と`await`を使用した非同期処理の設計と実装を通じて、非同期プログラミングを理解する
- **課題内容**:
  1. `async`と`await`を使用して複数の非同期タスクを並列実行するコード（例：Webスクレイピング、ファイル入出力）のサンプル例を実行し、動作原理を理解する
  2. 実行時間の比較実験を行い、同期処理との差を示す
  3. 非同期処理の利点、欠点、適用例を分析し、同期処理との違いを考察して，自分の言葉で説明せよ

----
---
**作成したpythonコード、特に空欄やポイントの説明**
<!--
   - 動作するコードを完成させて、変数・関数・クラスの役割やロジックを簡潔に説明する
   - 意図的な例外処理・失敗コードはその旨、説明すること
-->

```python

ここにコードを書く

```


**動作確認結果、確認ポイントの説明**
<!--
   - 実行結果の記述、正常に動作した証跡をもって確認する
   - コードや、コメントテキストはプレインテキストで記述し、
   - 必要に応じて、スクリーンキャプチャを添付してよい
-->

```

ここに実行結果を書く

```

  
**分析**

<!--
   - 出題者の意図を察知し、どんな概念・技法を理解し、修得する問題か、自分の言葉で簡潔にまとめる
-->

-
-
-
  
**考察**  
<!--
   - 問題解決の考え方・攻略法を自分の言葉で簡潔にまとめる
   - 用いた技法、例えば、関数プログラミング、プロトコル、オブジェクト指向等の技法の効果、活用場面について、応用シーンを考察する
-->

-
-
-

**改善点**
<!--
   - この課題を通して、まだ改善できると感じた点や他の解法のアイデアを自分の言葉で論じる
-->

-
-
-

-----

### 所感・今後の目標課題
 (自由記述欄、多様なご意見を尊重します)

- プログラミングに興味が湧かない原因
- プログラミングには興味がないが、それ以外で没頭していること
- 授業中に質問や意見が言えない理由
- いいねツールに期待すること
- コードや英語や文字、活字が好きにならない理由
- 私とプログラミング
- なぜプログラミングを学ぶのだろうか？
- これまで学んだことを振り返り
- これからの学びに活かすべき知見
 
---




---

