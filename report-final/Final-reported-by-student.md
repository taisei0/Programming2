#  プログラミングII　2024　最終課題レポート回答用紙

## レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|A| 20124020 | 佐藤大聖 |

##　作品のタイトル
### ショートプログラム：「〇〇〇〇〇」
### フリープログラム：「〇〇〇〇〇」

----
# 回答用紙 → 提出ファイルはこの様式を使うこと
- 要件を理解して、作品を作り、この回答用紙にレポート記述して提出すること
- マークダウン記法をしっかりプレビューして、記述ミスはすべて修正して完成させること
- 生成AIに頼らず、自分で考えて、自分の言葉で書くことが成長の糧となる

###  最終課題の概要
- これまで学修した技法・スキルを思う存分活用して
- 自由テーマで２つ作品をつくる
- (1) ショートプログラム
- (2) フリープログラム
- 活用した技法・手法の難易度・完成度を技術点として評価する
- 作品の設計思想、有用性、主張点、表現力を芸術点として評価する  
- 作品について、自分の言葉で丁寧に説明する：
  - どんな目的・想いで作ったか？
  - どんなユーザニーズに応えたいと考えたか？
  - 創意工夫を凝らした技法は何か？

### 技術点・芸術点の採点基準

- 関数の活用
- クロージャの活用
- 例外処理の活用 
- クラスの定義
- インヘリタンスの定義
- デコレ―タの活用
- ジェネレータ、コルーチンの活用
- 非同期処理の活用
- 非ブロックI/Oの活用
- メタクラスの定義、動的クラス生成
- デザインパターンの活用
- マルチスレッド並列処理
- 自作パッケージ、デプロイ



# 回答編
------
# ショートプログラム

### 作品名：例外処理

### **コード全体と、使用した技法の説明** 
```python
def divide_numbers():
    try:
        numerator = float(input("分子を入力してください: "))
        denominator = float(input("分母を入力してください: "))
        
        result = numerator / denominator
    except ZeroDivisionError:
        print("エラー: 0で割ることはできません！")
    except ValueError:
        print("エラー: 有効な数を入力してください！")
    else:

        print(f"結果: {result}")
    finally:
        print("プログラムを終了します。")

divide_numbers()

```


### **使った技法の説明**
このコードは分子、分母を入力して、その分子、分母を使って割り算を行うプログラムである。例外の場合は０で割ることはできません！というエラーを知らせるシステムを導入した。

### **実行結果** 

```
分子を入力してください: 1
分母を入力してください: 2
結果: 0.5
プログラムを終了します。

分子を入力してください: １
分母を入力してください: ０
エラー: 0で割ることはできません！
プログラムを終了します。
```

### **自己分析**


### **改善点、応用可能性について考察** 

-----
分数以外でもできるようにしたい
------

# フリープログラム

### 作品名：蛇ゲーム

### **コード全体と、使用した技法の説明** 
```python
import sys
import pygame

pygame.init()

screen = pygame.display.set_mode((600,400))

white = (0,0,255)
black = (0,0,0)

green = (0,255,0)
red = (255,0,0)

x1 = 300
y1 = 300

x1_change = 0
y1_change = 0

clock = pygame.time.Clock()

running = True
while running:
    screen.fill(black)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
           running = False
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
               x1_change = -10
               y1_change = 0
            elif event.key == pygame.K_RIGHT:
                x1_change = 10
                y1_change = 0
            elif event.key == pygame.K_UP:
                x1_change = 0
                y1_change = -10
            elif event.key == pygame.K_DOWN:
                x1_change = 0
                y1_change = 10
    x1 += x1_change
    y1 += y1_change

    pygame.draw.polygon(screen,green, [(x1, y1 - 200),(x1 - 50, y1 -100),(x1 + 50, y1 - 100)])
    pygame.draw.polygon(screen,green,[(x1 -50, y1 - 150),(x1 + 50, y1 - 150),(x1,y1)])
    

    pygame.display.update()
    
    clock.tick(30)
pygame.quit()
sys.exit()import sys


import pygame

pygame.init()

screen = pygame.display.set_mode((600,400))

white = (0,0,255)
black = (0,0,0)

green = (0,255,0)
red = (255,0,0)
dark_green = (0,200,0)
x1 = 300
y1 = 300

x1_change = 0
y1_change = 0

clock = pygame.time.Clock()

running = True
while running:
    screen.fill(black)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
           running = False
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
               x1_change = -10
               y1_change = 0
            elif event.key == pygame.K_RIGHT:
                x1_change = 10
                y1_change = 0
            elif event.key == pygame.K_UP:
                x1_change = 0
                y1_change = -10
            elif event.key == pygame.K_DOWN:
                x1_change = 0
                y1_change = 10
    x1 += x1_change
    y1 += y1_change

    pygame.draw.rect(screen,green, [x1, y1, 100, 10])
    pygame.draw.rect(screen,dark_green, [x1+100, y1-10, 20, 20])
    pygame.draw.rect(screen,green, [x1-15, y1, 15, 20])
    

    pygame.display.update()
    
    clock.tick(30)
pygame.quit()
sys.exit()

import pygame
import time
import random

pygame.init()

white = (255, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)
blue = (0, 0, 255)
green = (0, 255, 0)  
dark_green = (0, 200, 0) 

score = 0
 
dis_width = 800  
dis_height = 600  
 
dis = pygame.display.set_mode((dis_width, dis_height))
pygame.display.set_caption('ヘビゲーム')  
 
clock = pygame.time.Clock()
paused = False
 
food_block = 10  
snake_speed = 3  
 
font_style = pygame.font.SysFont(None, 30)  

eat_sound = pygame.mixer.Sound("sound.mp3")

def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width / 3, dis_height / 3])

def show_score():
    score_text = font_style.render(f"Score: {score}",True,black)
    dis.blit(score_text,[0,0])

def show_speed():
    speed_text = font_style.render(f"Speed: {snake_speed}",True,black)
    dis.blit(speed_text,[0,20])

def gameLoop():  
    global snake_speed
    global score
    global paused
    global speed
    game_over = False
    game_close = False
 
    x1 = dis_width / 2  
    y1 = dis_height / 2  
 
    x1_change = 0  
    y1_change = 0  
 
    foodx = round(random.randrange(0, dis_width - food_block) / 10.0) * 10.0 
    foody = round(random.randrange(0, dis_width - food_block) / 10.0) * 10.0 
 
    while not game_over:
 
        while game_close == True:
            dis.fill(white)  
            message("Click Q for Quit and C for Play again", red)  
            pygame.display.update()
 
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:  
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:  
                        gameLoop()
            for event in pygame.event.get():
                if event.type == pygame.QUIT: 

                    game_over = True
                if event.type == pygame.KEYDOWN:  
                    if event.key == pygame.K_LEFT:  
                        x1_change = -food_block
                        y1_change = 0
                    elif event.key == pygame.K_RIGHT: 
                        x1_change = food_block
                        y1_change = 0
                    elif event.key == pygame.K_UP:  
                         y1_change = -food_block
                         x1_change = 0
                    elif event.key == pygame.K_DOWN:  
                        y1_change = food_block
                        x1_change = 0
                    elif event.key == pygame.K_p:
                        paused  = not  paused
                    elif event.key == pygame.K_RIGHTBRACKET:
                        snake_speed = max(snake_speed + 10, max_speed)
                    elif event.key == pygame.K_LEFTBRACKET:
                        snake_speed = max(snake_speed + 10, max_speed)
        if not paused:
            if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
                game_close = True
            x1 += x1_change  
            y1 += y1_change  
            dis.fill(white)  

            show_score()
            show_speed()

            pygame.draw.rect(dis, blue, [foodx, foody, food_block, food_block])  
            pygame.draw.rect(dis, green, [x1, y1, 100, 10])  # [x_position, y_position, width, height] ([x位置, y位置, 幅, 高さ])
            pygame.draw.rect(dis, dark_green, [x1 + 100, y1 - 10, 20, 20])
            pygame.display.update()  
 
        #if x1+100 == foodx and y1-10 == foody: 
            if x1+100 == foodx and y1-10 == foody:  
                eat_sound.play()
                snake_speed += 10
                score += 1
                foodx = round(random.randrange(0, dis_width - food_block) / 10.0) * 10.0 
                foody = round(random.randrange(0, dis_width - food_block) / 10.0) * 10.0  
           
 
        clock.tick(snake_speed) 
 
    pygame.quit()  
    quit()  

gameLoop() 
```


### **使った技法の説明**
2Dゲームやマルチメディアアプリケーションの作成を手軽にするライブラリです。pygame.init() で初期化し、pygame.display.set_mode() で描画ウィンドウを設定しています。
ゲームループ内で pygame.event.get() によりイベント(キー入力、ウィンドウを閉じる等)を処理しています。
pygame.draw.rect() などで図形を描画します。
変数・定数をまとめた管理

例えば white, black, red, ... などのカラーコードを変数にまとめています。
dis_width, dis_height のように画面サイズを定数として定義し、他の処理と混在しないように整理しています。
関数の定義

message(msg, color) 関数で画面にテキストを表示する処理をまとめています。
show_score()、show_speed() も同様に、スコアや速度の表示ロジックを別関数に切り出すことでコードの見通しを良くしています。
グローバル変数の活用

score、snake_speed などを関数内で変更する必要があるため、global キーワードで参照しています。設計上はクラス化するとより見通しが良くなりますが、このサンプルではシンプルにグローバルで共有しています。
乱数生成 (random モジュール)

餌 (food) の位置や色をランダムで決定しています。random.randrange() や random.choice() を使って座標やカラーを変化させています。
サウンド再生

pygame.mixer.Sound("explosion.mp3") でサウンドを読み込み、eat_sound.play() で再生します。
ゲームループ

while not game_over: というメインループがあり、内部でプレイヤーの操作や物理座標の更新、画面描画、終了判定等を行います。
clock.tick(snake_speed) でフレームレート制御を行い、ゲーム進行速度を一定に保っています。

### **実行結果** 

```

```

### **自己分析**
コードは、初心者向けにシンプルな書き方でゲームが成り立つように書かれています。描画処理や衝突判定、スコア表示など、ゲームの基本要素をほぼ網羅しており、入門としては十分機能します。
一方で、スネークの体の成長(パーツの追従)などは実装されておらず、「見た目が蛇らしくない」という課題があります(今回は右上に長方形が描画される形で表現)。
グローバル変数の多用は、プログラムが大きくなるにつれて可読性や保守性を下げる原因にもなります。今後規模拡大や機能追加をする場合は、オブジェクト指向にするなどの設計変更が望ましいです。

### **改善点、応用可能性について考察** 
score や snake_speed などのゲーム状態を一元的に管理するクラス (GameState など) を用意すると、複雑化した際にコードが見やすくなるでしょう。
蛇や餌などもクラス化して、それぞれの描画・更新ロジックを持たせると拡張しやすくなります。
蛇の本格的な実装

多くの「スネークゲーム」では、プレイヤーが餌を食べると「体が伸びて列状になる」仕様です。こちらを実装する場合は、蛇の位置を (x, y) のリスト(またはデック)で管理し、先頭を更新・末尾を更新などのロジックを組む必要があります。
サウンドやグラフィックの強化

画像ファイルをロードしてスネークの頭や食べ物をアイコンで表示したり、BGM を流したりすると、ゲームの雰囲気が増します。
難易度設定や新要素の追加

壁の設置や、画面端でループさせるトンネル効果など、さまざまな仕掛けを追加することでゲーム性が向上します。
スコアに応じて難易度を自動上昇させるなどの工夫も考えられます。
オンライン対応や複数人プレイ

Pygame はローカルでの描画が前提ですが、Python のネットワーク機能と組み合わせることで、ネットワーク対戦やスコアランキング機能をつけることも可能です。
構造化の工夫

メインループが長くなると可読性が下がるので、イベント処理・ゲーム更新・描画処理をそれぞれ関数に分けると拡張しやすくなります。
実行時のオプションを受け取れるようにして、スピードや画面サイズを変更できるようにするなど、再利用性を高めることも考えられます。

----
### 所感・今後の目標課題 (自由記述欄、フィードバック意見を尊重)

- なぜプログラミングを学ぶか
- これまで学んで得た知見
- これからの学びに活かすべき知見


----