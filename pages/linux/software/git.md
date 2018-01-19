
## gitの操作方法

### Tr,Dr

本当にぶっきらぼうですが

##### 作業の流れ

前提として、2つのブランチ(dev(開発ブランチ)とmaster(安定版のブランチ))があったとして、

ソースコード編集した後に、

```
#自分のローカルレポジトリに移動
cd TO-MY-ROCAL-REPOSITORY-ADRESS
#最新版を反映する(自分の変更分と競合するか)
git pull
#開発ブランチに切り替え
git checkout dev

〜コードを編集〜

#編集したところをindexに追加する（*ですべてを追加）
git add *
#[確認]indexと自分の変更分に抜け漏れがないかを見る
git diff --cached
#indexの内容をコミットする
git commit
#リモートリポジトリ（のdevブランチ）にコミットした内容を反映させる
git push
#ブランチmasterに切り替え
git　checkout master
#devブランチからmasterブランチにマージする
git merge dev
#masterブランチをpushする
git push
```

##### 頻繁に確認するもの

```
git status
git checkout
```

##### その他必要なコマンド

```
git config　--global core.editor 'エディタを実行するためのコマンド'
git config --list
```

### 個人的記述

- git pull

クローン元の最新のコードを、自分のローカルリポジトリに、自分がクローンした時から最新のコードに至るまでの変更分だけ変更して、「自分が変更した、最新版ではない古いコード」から、「自分の変更分以外は最新のコード」になるようにするコマンド。([ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E3%82%AF%E3%83%AD%E3%83%BC%E3%83%B3%E5%85%83%E3%81%AE%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%8B%E3%82%89%E6%9C%80%E6%96%B0%E3%81%AE%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E5%8F%96%E5%BE%97%E3%81%99%E3%82%8B)を参照)

自分の変更していた部分と、最新版のコードで同じ所を変更していた場合、修正しなければならない。（自動で競合部分のコードを調節してくれるわけではない。）その後、自分の変更分と最新版のコードを調整してコミットする。

リモートレポジトリから「引っ張ってくる」イメージ。

- git checkout [ブランチ名]

ブランチの切り替えができる([ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%82%92%E5%88%87%E3%82%8A%E6%9B%BF%E3%81%88%E3%82%8B)を参照)

#「ブランチの切り替え」って、そういう概念として捉えるしかないのだろうか...自分のいるところはこういうところだ、というふんわりした説明しか今は出来ない

- git add *

addで、一旦index(帳簿みたいなところ)に載せる。*にするとすべての変更ファイルをindexに乗せてしまうので注意。

（[ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E3%82%B9%E3%83%86%E3%83%BC%E3%82%B8%E3%83%B3%E3%82%B0)の図（参照先では「ステージング」という名前になっている）が一番イメージし易かった。

- git commit

コマンドを打つとエディタが表示され、コミットメッセージを記述されるよう要求される。1行目がそのままタイトルとなるので注意すること。2行目以降はコメントとなる。

- git config　core.editor 'エディタを実行するためのコマンド'

  コミット時のエディタを変更するコマンド
  https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E6%99%82%E3%81%AE%E3%82%A8%E3%83%87%E3%82%A3%E3%82%BF%E3%82%92%E5%A4%89%E6%9B%B4%E3%81%99%E3%82%8B
  を参照

  commit時にいつもnanoを使用したい時は下のように記述する。

```
git config --global core.editor 'nano'
```

　　- --global

  --globalをつけると、そのPCの現在のOS、現在のユーザーでgitを使用した時のデフォルトの値になる。レポジトリ単位で設定したい時（レポジトリ毎に切り替えたい時等）は付けないこと。（[ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E6%99%82%E3%81%AE%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E5%90%8D%E3%83%A1%E3%83%BC%E3%83%AB%E3%82%A2%E3%83%89%E3%83%AC%E3%82%B9%E3%82%92%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B)を参照）

  --global設定を変更したいときは→を参照([ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#global-%E8%A8%AD%E5%AE%9A%E3%81%8C%E4%BF%9D%E5%AD%98%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%82%8B%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB)と[ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E8%A8%AD%E5%AE%9A%E5%80%A4%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B)と[ここ](https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d#%E8%A8%AD%E5%AE%9A%E5%80%A4%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B))

  #その時だけ設定値を切り替える方法もあるんだろうなぁ・・・

  - コミットってどういう意味？
  
  https://teratail.com/questions/25297
  
  上記が分かりやすいかも
  
  >変更内容が正しいことが編集者自身が確認済であり、後戻りすることはないという意味
  
  その他参考：[kray.jp - Git初心者に捧ぐ！Gitの「これなんで？」を解説します。 - なんでcommitする前にaddしなきゃいけないの？]（http://kray.jp/blog/git-why-explanation/#commit-add）
  
  （イラストがゆるくて好き、他にも疑問解決出来る記述あり、HEADとか読んでおきたい）
  
  addした後に、確認の意味で'git diff --cached'すると、indexと最新コミットとの変更点を見ることができる（抜け漏れがあったら随時addする）
  
  （参考サイト：[qiita.com - 忘れやすい人のための git diff チートシート - git addした後に変更点を見る](https://qiita.com/shibukk/items/8c9362a5bd399b9c56be#git-add%E3%81%97%E3%81%9F%E5%BE%8C%E3%81%AB%E5%A4%89%E6%9B%B4%E7%82%B9%E3%82%92%E8%A6%8B%E3%82%8B)）
  
  （↑のサイトは他にもdiffについて載っているので参考になるかも）
  
- git merge (反映元ブランチ名)

まず、

mergeとは、[併合する、溶け合わせる、(…を)(…に)溶け込ませる、没入させる、(…を)(…と)合併する](https://ejje.weblio.jp/content/merge)の意。

ちなみにmerginalとは、[［形動］周辺にあるさま。境界にあるさま。また、限界であるさま。](https://dictionary.goo.ne.jp/jn/206611/meaning/m0u/)(...分かりにくくなった)

もとは自動詞なのかな？と

参考：rebase

個人的に一番わかりやすかったサイトは[ここ（quita.com - git rebaseを初めて使った際のまとめ）](https://qiita.com/panti310/items/e0ec74b47c6c219f2a8b)

一番最後から見て（最終更新したところから見て）、「どういうふうに色の違う積み木を組み上げたか」の違い、と表現したほうが分かり良いのかな、と

だからこそ、最終更新をした時点で「最後として残る方」のブランチを選択(checkout)して、タイプすれば良いのではないかと考えました（むつかしい＞＜）。

参考：[techacademy.jp - git mergeを使ってブランチをマージする方法【初心者向け】](https://techacademy.jp/magazine/10264)

ここの、「コミットが済んでいない状態で'git merge'・'git checkout'しない」というのは心がけておくこと、苦労して変更したものがパーになるので。また、衝突が発生した場合も読んでおくと良いかも。

- git push

現在選択しているブランチを、commitした記述で更新する。（リモートレポジトリに変更分を「押す」イメージ）

- git status

自分のローカルリポジトリで今どんなことをしていたのか確認できる。

- git config --list

自分(のリポジトリ)の設定を確認できる。


----

### 以下は編集途中です

//今後書き加えあり

##### 基本的な流れ

1. ソースコードをダウンロード

[Level 1]

githubの該当ページにアクセスし、「Clone or download」からzipファイルをダウンロードする

か、

```
git clone https://github.com/USER-ACCOUNT/REPOSITORY-NAME.git
```

USER-ACCOUNTは各ユーザー等、REPOSITORY-NAMEはリポジトリの名称に読み替える。





##### 参考にしたページ

https://qiita.com/opengl-8080/items/451c5967cbbc262f4f0d

