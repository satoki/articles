# 【文学】Flagを読む

Proもすなる**あどかれ**といふものを、Yowaもしてみむとてするなり。  
ということで[CTF Advent Calendar 2021 - Adventar](https://adventar.org/calendars/6914)の24日目の記事です。  
前日は、kusano_kさんの「[SECCON CTF 2021作問者writeup](https://kusano-k.hatenablog.com/entry/2021/12/23/014312)」でした。  
開催したCTFで問題をすべて粉砕された記憶も残っておりますが、競技者としてだけでなく恐怖の作問マシーン([出典](https://project-euphoria.dev/blog/29-seccon-2021/#atogaki))としても知られていますね。  
裏話が聞けるのも作問者のWriteUp特有のものではないでしょうか。  
明日はガチプロmitsuさんの「Babai is you」の予定です。  
クリスマスということもあり、寂しい夜を記事を枕に寝たいと思います。  

## はじめに
ここまで読んでいただきありがとうございます。  
この記事には技術的な話は一切出てきませんので、申し訳ありませんがそちらをお求めの方は明日に飛んでください😭。  
ちなみにFlagを読む(Guessする)との意味合いでの記事でもありません。ただFlagを読むだけです。  

私のことを知らない方が多いと思いますので自己紹介をしておくと、情報系院生の[Satoki](https://twitter.com/satoki00)と申します。  
[SECCON Beginners CTF 2021](https://www.seccon.jp/2021/)でよくわからないMiscやWebを作問したり、ローカルですがOSINTをメインとしたTsukuCTF 2021や大学サークルでのIMCTF 2021などの運営にも携わらせていただいております。  
今年の終わりも近いということもあり、技術的な話から離れて脳を休めて読んでいただける記事にしました。  

## Flagはどうやってできるのか？
<span style="font-size: 500%;">🚩</span>  
CTFプレイヤーの皆さんはFlagがなんであるかはご存じかと思いますが念のため説明すると、FlagとはCTFにて問題を攻略した際に取得できる文字列のことです。  
通常CTFの略称などを先頭に用いて、語句をつなげてスネークケースにて記述します。  
例: `satokictf{h1m0_n1_n4r1741_ny4n}`  
このFlagはもともと`Himo_ni_naritai_nyan`という願望をLeet変換したものになります(Leet変換については、あとで説明します)。  
このようにFlagは作問者が疲れていない場合、何らかの意味のある文から作成されます。  
疲れている場合は適当なハッシュ値になります。  
例: `karouctf{82cc637fdbabedd8d82aea8898284a165feb52e47f7f6e407a66a6daec7125ae}`  
このFlag作成はCTF作問者しか味わうことのできない作業です。  

### Leet変換とは
いきなりLeet変換したと書きましたが、Leet (leetspeak)とは主にネット上で使われる文の表記法になります。  
eliteがeleetになり、eが取れてleetになったといわれています([Wikipedia学士より](https://ja.wikipedia.org/wiki/Leet))。  
Leet変換は要約すると、アルファベット`A`などを似た別の文字`4`などに置き換える変換のことです。  
`SATOKI`は`5470k1`などになります。  

### 問題を解かずにCTFを全完する方法
完全に余談なのですが、問題を解かずにCTFを全完する方法があります(大嘘)。  
この銀の弾丸たる方法を知る前に、まずはCTFの作問者として以下の文章をLeet変換してみてください。  

```text

I_love_CTF_but_I_cant_keep_up_with_the_difficulties_these_days

I_am_a_pwn_cat_As_yet_I_have_no_name

```

leetpassなどを導入している方以外は、「leet converter」などでググって[Universal Leet (L337, L33T, 1337) Converter](http://www.robertecker.com/hp/research/leet-converter.php)のようなオンラインツールを利用したかと思います。  
勘の良い方は気付いたかもしれませんが、オンラインツールにFlagが流れ出ています。  
日本語のオンラインLeet変換器を作ればいくつかのCTFのFlagが取得できるでしょう。  
VirusTotalの情報流出などご存じの方も多いかと思いますが、翻訳作業や変換作業でも同様の注意が必要です(Base64とかも)。  
以上CTFの運営兼作問者として気付いた、人間の脆弱性でした。  
記事に学びがないとkillされそうであったので少しためになりそうなことを書きました。  
ちなみにLeet使っていない人は関係ありません、ごめんなさい。  

## Flagは文学
<span style="font-size: 500%;">📖</span>  
余談はここまでで本題に入ります。  
突然ですが、あなたは覚えているCTFの良問はあるでしょうか？  
きっとCTFプレイヤーは特殊な脆弱性や天才的発想を用いた数多の良問が思い浮かんだでしょう。  
では、覚えているFlagはあるでしょうか？  
前節で述べた通り、Flagは作問者が作っているため、何らかのメッセージが含まれているはずです。  
しかし、実際の競技者はFlagを手に入れ、Submitしてしまったらクリップボードから消してしまうのではないでしょうか。  
WriteUpには解法が含まれており、技術的に非常にためになりますが、Flagを味わっているものが少ないです。  
俳句のようにきっと問題を作った人が表現したかったものが埋め込まれているはずです(俳句作っている人に怒られそう)。  
少しもったいないとは思いませんか？  
今回はそんなFlagを読んでいこう、いうなればWriteUpのFlag編という記事です。  

## Flagを読む
<span style="font-size: 500%;">👀</span>  
それではFlagを読んでいきたいと思います。  
大仰に文学と言ってはいるものの、実際は問題に関連する小ネタや雑学が含まれているだけです。  
それを読み取って一緒にクスりとしようというのが今日の目標です。  
英弱なので翻訳などはDeepL修士ということをご理解ください。  

### ctf4b{b3_c4r3ful_0f_fl135_wh3n_73l3p0r71n6}
初めにSECCON Beginners CTF 2021に私が出題して誰にも触れられなかったFlagのひとつです。  
これはflyというGUIゲームのチート問題でのFlagになります。  
動作時のメモリを変更して主人公の位置を変更し、テレポートすることでFlagにたどり着けるといった解法でした。  
Leetを戻してやると`Be careful of flies when teleporting`となり、日本語では`テレポート時のハエに注意`となります。  
ハエなど問題内に出てきてはいませんので、おかしいですね。  
実はこれは[1986年公開のバイオホラー「The Fly」](https://www.amazon.co.jp/dp/B003ZX8FYM)をネタにしたものです。  
テレポートする男性がハエと混ざってしまうといった物語になっています。  

### ctf4b{r36ul4r_3xpr35510n_f0r_4ny_51n6l3_ch4r4c73r}
次も同じくSECCON Beginners CTF 2021にて出題したwritemeという問題です。  
問題文は`writeme.`となっていました。  
FlagのLeetを戻すと`r36ul4r_3xpr35510n_f0r_4ny_51n6l3_ch4r4c73r`が`regular expression for any single character`になります。  
これは`任意の1文字に対する正規表現`と日本語訳できます。  
一見すると意味が分かりませんが、実はこの問題の解法は`/proc/self/mem`を書き換えるものでした。  
ここで問題文をよく読むと、writeme`.`。  
正規表現としてみると、この最後のピリオドは任意の一文字とマッチします。  
つまり`writemem`(write mem)とマッチします。  
実は問題文に解法が隠れていましたよという作問者からのメッセージです。  

### HarekazeCTF{RSA_m34n5_Rin_Shiretoko_Ango}
[今日も開催](https://harekaze.com/ctf/2021-jp.html)される、Harekaze mini CTFの2020年度のFlagです。  
推しキャラシリーズですね。  
問題はRSAの比較的優しい問題ですが、`RSA_means_Rin_Shiretoko_Ango`とのことでRin Shiretokoの暗号だと主張しています(問題文でもそのような記述があります)。  
これはハイスクール・フリートのキャラクター、[知床 鈴](https://www.hai-furi.com/character/01_06/)のことですね。  
Harekaze自体がハイスクール・フリートのネタで満載なのも面白いです。  
ちなみに晴風自体、ハイスクール・フリートに登場する架空の軍艦らしいです。  

### Neko{S4EoMHlo608?t=2m30s}
推しキャラシリーズで続いて、動画でより強くアピールしてくるFlagもあります。  
BSides Ahmedabad CTF 2021のRodaという問題です。  
21 solvesという初心者には難しい解法の先に出てくるFlagですが[YouTubeのアドレス](https://youtu.be/S4EoMHlo608?t=2m30s)です。  
「アマガミSS シリーズ OP＆ED COLLECTION 桜井梨穂子編」のようですね。  
桜井梨穂子への強い想いが伝わってきますね。  

### MaidakeCTF{Kirito_is_said_to_be_able_to_go_720km/h_when_he_uses_his_sword_skill}
こちらもLeetではありませんが、Maidake CTF 2020のFlagです。  
Web問であり、高速でリダイレクトするページの中からFlagを探すといった問題でした。  
連想してからなのか、SAOのキリト君をFlagにしているようですが720km/hが謎ですね。  
実はこれAbemaTVが[世界最速無料アニメ配信数No.1のCM](https://abematv.co.jp/posts/5962286/)で導出したキリト君の推定時速のネタです。  
爆速ですね。  

このほかにも様々なCTFに面白Flagが隠れているかと思います。  
素敵なFlagを発見した方は、教えてください(これ以上探す気力が尽きました。クリスマス明日ですしね)。  
🎅🚩  

## おわりに
神記事に挟まれたネタ記事でしたが、楽しんでいただけたでしょうか？  
FlagをGuessする場合を除いて、競技者はFlagの中身をよく見ていないのではないかと考えたところから始まった記事です。  
実際に開催されたCTFのWriteUpをよく読むのですが、Flagのネタがスルーされているものが多くありました。  
CTFの楽しみ方の一つと言えるかどうかはわかりませんが、是非Flagの中身についても考える時間をとってやると新たな味を感じることができるかもしれません。  
そしてこの記事を読んでくれているあなたが作問する際に、Flagをニヤニヤしながら作って(詠んで)くれることを期待します。  
私もどこかでその問題を解いて、Flagを眺めニヤニヤしているかもしれません。  

本当にここまで読んでいただきありがとうございます。  
Capture The **Flag** !!!!  
<!-- flagwoyomu{fl46_70773m0_h170r1} -->