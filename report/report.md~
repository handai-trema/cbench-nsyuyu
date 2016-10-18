# 第一回レポート課題(10/5出題，10/11解答)
## 課題2
### 課題内容
仮想スイッチを停止したら、コントローラで次のメッセージを表示するようにしてみよう:

```
Bye 0xabc
```

### 解答
ヒントに書かれていたリンク先のページを参考に，スイッチが切断した際に
呼び出される，switch_disconnectedハンドラに関する記述を追加した．
具体的には，hello_trema.rbのHelloTremaクラス内に以下の内容を追加した．

```ruby
class HelloTrema < Trema::Controller
  ...
  def switch_disconnected(dpid)
    logger.info "Bye #{dpid.to_hex}"
  end
end
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