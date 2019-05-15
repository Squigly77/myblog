Title: Netlifyで独自ドメインを設定する
Date: 2018-07-01
Category: Pelican
Tags: Netlify,Python,Pelican
Slug: netlifydomain

Netlifyで独自ドメインを設定してみた

### ドメインを取得する
---

![Xdomain](../../../images/xdomaintop.jpg)  <br>

他サイトのドメインはムームードメインを利用していますが、今回はドメインをXdomain<a href="https://px.a8.net/svt/ejp?a8mat=356RAJ+GF7GHE+CO4+15PEXE" target="_blank" rel="nofollow">（リンク）</a><img border="0" width="1" height="1" src="https://www10.a8.net/0.gif?a8mat=356RAJ+GF7GHE+CO4+15PEXE" alt="">で取得することにしました。<br><br>

`ドメインの検索`→`会員登録`→`お支払い情報の入力`→`内容の確認・規約への同意`→`申込み完了`と進んで10～20分で簡単にドメインを取得できます。（クレカ払いの場合）<br>

### Netlifyにカスタムドメインを登録
---

Domain Setting→Add custom domainと進んで取得したドメインを入力`(www).xxx.com` を入力して`Verify`をクリック  
Netlifyはwww付きのドメインをプライマリードメインとして推奨しているようです。なのでwww付きで登録しました。<br>

### DNS設定
---

`Verify`をクリックした後はこんな画面になるので`Check DNS Configuration`をクリック。

![dns](../../../images/checkdns.jpg)<br>

すると、CNAMEをエックスドメインで編集するかNetlify DNSを使うか表示されるので`Set up Netlify DNS~~`をクリック。  
ベストパフォーマンスを得るにはNetlify DNSを必ず使ってねと書いてありますね。ALIASやCNAMEも気にしないでね、とも。<br>

![dnsconf](../../../images/dnsconf3.jpg)

<br>
wwwなしのドメインでAレコードをドメインプロバイダーのDNSレコードに記述するやり方だとNetlifyの強力なCDNを利用することができないので注意。
<br>

![dns](../../../images/dnsconf1.jpg)

「Netlify 独自ドメイン」でググるとAレコードを記述する方法ばかりがヒットしたので最初はその方法で設定していましたが、Aレコードを使用するとNetlifyの恩恵が得られなさそうなのでwwwの使用に抵抗がなければwwwありでNetlify DNSを利用しましょう。<br>

### ネームサーバーの変更
---
`Set up Netlify DNS~~`をクリックして進めていくとDNSレコードをNetlifyが勝手に設定してくれて、更に進むと4つのネームサーバーが表示されるのでコピーしてエックスドメインの「ネームサーバーの確認・変更」から４つのネームサーバーをペーストする。<br><br>


![nameserver](../../../images/nameservers.jpg)

<br>DNSが浸透すると独自ドメインでアクセスできるようになります。


![domainset](../../../images/domainset.jpg)<br>


### Let’s Encryptの証明書を取得
---
カスタムドメインを設定したらHTTPSの`Verify DNS configuration`→`Let's Encypt certificate`をクリック。しばらくすると証明書を取得できます。  
下の画面のような表示になれば成功。   


![https](../../../images/https.jpg)


### httpsを強制
---
Force HTTPSをクリックしてhttpでのアクセスをhttpsにリダイレクトさせる。

### DNS 設定 （2019年3月13日追記）
---

Netlify DNSを使用してDNSレコードを自動でセッティングした後にMXレコード等のレコードを追加する場合は、<br>`Domain Settings`からCustom Domainsの`Netlify DNS`をクリックして設定ページに移動、`Add new record`で追加できます。

### 感想
---
ドメインを設定するのは簡単なのですが、改めてドキュメンテーションを読んでもDNS関連は全然知識がないし、英語なので誤読していないか心配。時間があるときに辞書片手にしっかり読まないといけないかなあ～と思ったりしました。