# 第二回レポート課題(10/12出題，10/18解答)
## 課題内容(Cbenchのボトルネック調査)
Rubyのプロファイラを用いて，CbenchやTremaのボトルネック部分を
発見し，遅い理由を解説せよ．
## 解答
ruby-profを用いて，Cbenchプログラムのプロファイリングを行った．
プロファイリングの結果を以下に示す．なお，全体時間のパーセンテージが上位
10件以内のメソッドについての結果を記載している．
```
 %self      total      self      wait     child     calls  name
  2.72      6.798     2.995     0.000     3.803   123066   Kernel#clone
  2.67      8.198     2.944     0.000     5.254   231506  *BinData::BasePrimitive#_value
  2.61     26.885     2.881     0.000    24.004   119178   BinData::Base#new
  2.37      2.681     2.612     0.000     0.069   381930   Kernel#respond_to?
  2.17      6.898     2.388     0.000     4.510   198543  *BinData::BasePrimitive#snapshot
  2.00      3.652     2.210     0.000     1.442   123066   Kernel#initialize_clone
  1.91     23.689     2.106     0.000    21.583   105553   BinData::Struct#instantiate_obj_at
  1.91      2.103     2.103     0.000     0.000   127489   BasicObject#!
  1.52      1.680     1.680     0.000     0.000    98290   BinData::BasePrimitive#initialize_instance
  1.52      6.028     1.671     0.000     4.357    81839   Kernel#dup
```


## 課題3
### 課題内容
HelloTrema が起動したら次のメッセージを表示するようにしてみよう:

```
HelloTrema started.
```

ただし、次の回答ではダメ (なぜダメか？も考察しよう)

```ruby
class HelloTrema < Trema::Controller
  def start(_args)
    logger.info 'HelloTrema started.'
  end
  ...
```

### 解答
self.classによって，カレントオブジェクトのクラス(Classクラス)を取得することができる．
また，Classクラスの親クラスであるModuleクラスのnameメソッドを用いて，
クラス名を文字列で取得することができる．
つまり，self.class.nameで，自クラス名を取得することができる．
また，元のソースコードでは，文字列がシングルクォーテーションで囲まれているが，
このままでは，文字列に埋め込まれた式を展開することができないため，
式を含んだ文字列を表示する場合は，文字列をダブルクォーテーションで囲む必要がある．
これらを考慮して，hello_trema.rbのHelloTremaクラス内のstart関数の中身を以下の内容に変更し，
課題を解決した．
```ruby
class HelloTrema < Trema::Controller
  def start(_args)
    logger.info "#{self.class.name} started."
  end
  ...
```