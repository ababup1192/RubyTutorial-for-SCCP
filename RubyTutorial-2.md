# 課外プロジェクト 2015 実践的プログラミング
## ~ Ruby II ~
2015 11/30 渡部未来・齊藤智博
資料URL: https://github.com/tspider0176/RubyTutorial-for-SCCP

## 1 はじめに

前回まではRubyの基本的な考え方やよく使うコレクション(配列・Hash)などの使い方を勉強してきた。
今回は関数、そしてオブジェクト指向を通してアプリケーション作りのためのプログラミングを学んでいく。

## 2 関数

Rubyは、すべての値がオブジェクトな純粋なオブジェクト指向であるため、関数ではなくメソッドであるが、ここでは敢えて関数として話を進めていく。

まずはじめに与えた数値の二乗を返す関数は以下のように定義、呼び出し実行される。
```
def square(x)
  x * x
end

square(3)
=> 9
square(1.5)
=> 2.25
square('aaa')
=> TypeError: can't convert String into Integer
```
この時点でC言語と比べると、一見些細だが気をつけるべき点がいくつかある。大きくは型が明記されない点である。これはRubyがScript言語で動的型付け言語だからである。これは前回の資料でも同様だったので大丈夫だと思われる。以上の理由により戻り値と引数の型は存在しない。注意するべきは呼び出し時で型がないため、どんな値も渡すことが出来てしまう。ここでは整数・小数は掛け算をすることが出来るので問題なく計算が行われるが、文字列は掛け算をすることができないため、型の「実行時エラー」となってしまう。Rubyはコンパイルして型をチェックできないのが大きな欠点となる。

### 2.1 一般化

関数を一般化すると以下のようになる。

```
def 関数名(仮引数名, ...)
  式
  ...
end
```

いくつかの注意するべき点は先ほど述べた通りだが、関数の内部について着目すると式の集まり(集合)になっていることがわかる。Rubyの関数は最後に評価された式を戻り値として使うため*return*キーワードは存在しない。それを踏まえると以下の例は何を返すだろうか。

```
def even_double(x)
  if x % 2 == 0 then
    x * 2
  else
    x
  end
end

even_double(3)
=> 3
even_double(4)
=> 8
```

ifなどの制御式やmapなどの多くのイテレータが値を返す意味がわかっただろうか。Rubyの関数についてまとめると以下のようになる。

- 型は明記されない(実行時に決まる)
- 関数は式の集合である
- 最後に評価された式が戻り値となる

以上を抑えれば基本的な関数は作れるはずだ。

演習問題: 名前を入力したらイニシャル(文字列)を返す関数*initial*を作れ。
また、名前の配列の配列からイニシャルの配列を返すコードも書け。

```
name = {firstName: "John", familyName: "Kennedy"}
initial('John', 'Keneddy')
=> "J.K"
names = [["John", "Kennedy"], ["Barack", "Obama"], ["George", "Washington"], ...]
# コード
=> ["J.K", "B.O", "G.W", ...]
```

### 2.2 デフォルト引数

関数を利用するときに普段は省略したいが、あるときはオプションといて使いたい引数などがあるとする。そういう時はデフォルト引数を用いる。

```
def even_double_plus(x, t=0)
  if x % 2 == 0 then
    x * 2
  else
    x + t
  end
end

even_double_plus(3)
=> 3
even_double_plus(3, 5)
=> 8
```

演習問題: 名前を入力したらイニシャル(文字列)を返す関数*initial*を作れ。
ただし、ミドルネームも考慮せよ。

```
initial('Barack', 'Obama')
=> B.O
initial('John', 'F', 'Keneddy')
=> J.F.K
```

デフォルト引数ではどうにも上手く行かない場合は、前回やったハッシュを引数として使うと、
より柔軟に関数が書けるので覚えておこう。

## 3 クラス

### 3.1 メソッド

## 4 継承

## 5 モジュール