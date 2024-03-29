# URL除外文字によるAndroidアプリへの悪性リンク挿入の話

## はじめに
本記事ではAndroidアプリについて知識がない状態で、脆弱性を探してやろうと挑んだ末に見つけた危険な挙動をまとめる。
脆弱性と言えないこともなく、おそらくBugBountyProgramなどを行っているアプリにも多く混入している実装であるため、報告は各自に任せる(が私は焼き肉が食べたい)。  

**各開発元への確認を行った後に公開しています。記事の内容を験する場合、法律により処罰される可能性があります。**

## 不思議な挙動の発見
国際化ドメイン名によるスパムチェック回避の論文を読み、URL中の特殊文字の挙動について調査しようとDiscordアプリ(Androidクライアント)の自分専用チャンネルに特殊文字を含むリンクを投げていた。
すると自動リンク部分に以下のような挙動が見られた。  
<img src="images/Discord1.png" alt="Discord1.png" width="300">  
ポップアップ中の`|`でリンクが切れているようだ。
前半をタップするとGoogleへ、後半をタップするとEvilへ飛ばされる。
URLに使用できる文字はRFC2396とRFC3986に定義されているらしく、`|`や`` ` ``はその中で除外されており使用不可能でエスケープされなければいけないとある。
これだけを見ると正常な挙動に思える。
しかし、ポップアップ外では一本のリンクになっている。  
<img src="images/Discord2.png" alt="Discord2.png" width="300">  
念のためPCクライアントでも確認しようと開くと、以下のようであった。  
<img src="images/Discord_PC.png" alt="Discord_PC.png" width="800">  
こちらもエンコードされて一本のリンクになっている。
こうして同じ投稿でも場所や環境によってリンクの解釈が異なるといった不思議な挙動を引き当てた。
以下のようなリンクで同様の現象が再現した。
```
https://www.google.com/search?q=satoki00|evil.com
https://www.google.com/search?q=satoki00`evil.com
https://www.google.com/search?q=satoki00０evil.com
https://www.google.com/search?q=satoki00愛evil.com
```

## URL自動リンク処理
アプリのURL自動リンク処理がどのように行われているか調査すると、Linkifyが利用されるようだ。  
Linkify  
[https://developer.android.com/reference/android/text/util/Linkify](https://developer.android.com/reference/android/text/util/Linkify)  
Linkifyを用いることでtext中の指定した部分をリンク化することができる。
指定方法によってはURLすべてをリンクにすることや、パターンマッチすることもできる。
試しにアプリを作成してみたところ、URLすべてをリンクする設定にすると`|`で分割が発生した。  
<img src="images/PoC1.png" alt="PoC1.png" width="300">  
このことからもわかる通り、他の環境では発生しない挙動だといえる。

## 危険性
環境によってリンクが分割されることで、意図せずフィッシングサイトなどに誘導される危険性がある。
以下のようにURLクエリパラメータを長くした場合、その部分をタップする確率が上がる。
```
https://www.google.com/search?q=satoki00%7Cevil.com?a=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
```
<img src="images/PoC2.png" alt="PoC2.png" width="300">  
Discordの場合はリンクの色が変化するため、注意深く確認すればリンクが分割されていることがわかるが、後述するアプリの中にはリンクの色が変化しないものもある。
この場合URLの分割をユーザが見分けることは難しい。
また、ユーザが該当するURLを他の端末で過去に開いたことがある場合、そのアドレスは信用できると認識してしまう。
ユーザから見るとPCなどでは正規リンクに、Androidでは悪性リンクとなる。

## 実際のアプリたち
Discord特有の問題であるか確認したところ、以下に挙げるアプリで同様の現象を確認できた。

### Instagram
リンクの色が変化しないため、ユーザが見分けることが出来なくなっている。  
**アプリ版**  
<img src="images/Instagram.png" alt="Instagram.png" width="300">  
**PC版**  
<img src="images/Instagram_PC.png" alt="Instagram_PC.png" width="500">  

### LINE
文字色で分割が判断できるが、多数のリンクとテキストが混在する場合は注意が必要である。
Note機能中にも同様の現象が確認できた。  
**アプリ版**  
<img src="images/LINE.png" alt="LINE.png" width="300">  
**PC版**  
<img src="images/LINE_PC.png" alt="LINE_PC.png" width="600">  

### Messenger
分割後のURLにクエリパラメータを含めるとテキストと認識された。
悪性サイトにリンクされる部分が少ないため、危険性は低い。  
**アプリ版**  
<img src="images/Messenger.png" alt="Messenger.png" width="300">  
**PC版**  
<img src="images/Messenger_PC.png" alt="Messenger_PC.png" width="300">  

## おわりに
アプリの仕様に依存するが、ユーザの入力を信用しそのまま自動リンク処理に渡すことは避けたほうがよさそうだ。
環境によって異なるリンクとなるのは望ましくなく、ユーザが悪性リンクをAndroid以外の環境で開き、信用してしまう原因となる。
また、パターンマッチ、パーセントエンコーディング、置換でのある程度の対策が可能となる。