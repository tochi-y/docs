# WebDAV モデル

### WebDAVとは
* WebDAVは、Webサーバに対して直接ファイルのコピーや削除を行ったり、ファイル所有者や更新日時などのファイル情報を  
クライアント(Webブラウザ)から取得・設定するといった機能を持つ分散ファイルシステムで、HTTP 1.1を拡張したプロトコルで実現される。

### 概要
* PersoniumのBoxは、それ自体がRFC4918:WebDAV空間であり、ファイルやコレクションを作成することができます。  
Personiumでは、通常のWebDAVコレクション以外の特殊なコレクション（OData, Service)の作成や、ACLによるコレクションのアクセス制御が可能です。

### WebDAVのロック
* WebDAVはファイル・コレクションの登録・更新・削除中の状態でBox配下に排他ロックがかかります。

* 上記状態の場合、他のユーザは取得は可能ですが、登録・更新・削除の処理はロックが解除されるまで実行を待機します。

* また、一定時間を超過してもロックが解消されていない場合、以下のレスポンスが返却されます。

* 以下のレスポンスが返却された場合、しばらく時間を置いてからリクエストを実行するようにして下さい。

* エラーコード：503

* エラーメッセージ：Too many concurrent requests.

### MKCOLの拡張
* Personiumでは、RFC5689に準拠した形で、ODataやサービス等の特殊なコレクションの作成をサポートしています。

* これにより、ファイル以外にも様々なデータモデルを扱うことができます

### 特殊コレクション
#### &nbsp;ODataコレクション
* Personiumでは、リレーショナルデータを扱うためにODataコレクションをサポートしています。

* MKCOLでBox配下にODataコレクションを作ることで、そのコレクション以下のパスはOData空間となります。  
その空間にスキーマ等の適切な設定をすることで、リレーショナルデータを格納することができます。

* 詳細な内容については、ODataモデルを参照。


#### &nbsp;サービスコレクション
* Personiumでは、ユーザが定義したサーバサイドロジックを実行するためのインターフェースとして、  
サービスコレクションをサポートしています。

* MKCOLでサービスコレクションを作った上で、適切な設定を行う事によって、  
そのコレクション以下のパスでユーザ定義のサービスを自由に提供することができます。

* 詳細な内容については、サービスのモデルを参照。

#### Streamコレクション
* Personiumでは、永続的なODataに加えて、データをStreamとして扱うために、Streamコレクションをサポートしています。

* MKCOLでStreamコレクションを作ったうえで、適切な設定を行うことによって、
そのコレクション以下のパスで、データをStreamに送信したり、Streamからデータを受信することができます。

* 詳細な内容については、Streamのモデルを参照。
