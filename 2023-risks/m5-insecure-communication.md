---
layout: col-sidebar
title: "M5: 安全でない通信 (Insecure Communication)"
---

# 脅威エージェント

**アプリケーション依存**

最近のモバイルアプリケーションのほとんどは一つ以上のリモートサーバーとデータをやり取りします。データ伝送が行われる際、一般的にモバイルデバイスのキャリアネットワークとインターネットを経由しますが、平文や非推奨の暗号プロトコルを使用して送信した場合、回線上で盗聴する脅威エージェントがそのデータを傍受して変更する可能性があります。脅威エージェントは機密情報の窃取、諜報行為、なりすましなどのさまざまな動機を持っているかもしれません。以下のような脅威エージェントが存在します。

- ローカルネットワーク (侵害された Wi-Fi や監視された Wi-Fi) を共有する敵対者
- 不正な通信業者やネットワークデバイス (ルーター、携帯電話基地局、プロキシなど)
- モバイルデバイス上のマルウェア

# 攻撃手法

**悪用難易度 容易**

最近のアプリケーションは SSL/TLS などの暗号プロトコルで応答しますが、その実装には以下のような欠陥が時折みられます。

* 非推奨なプロトコルや不適切なコンフィグレーション設定の使用
* 不正な SSL 証明書 (自己署名、失効、期限切れ、正しくないホストなど) の受け入れ
* 非一貫性 (認証などの特定のワークフローでのみの SSL/TLS の使用)


# セキュリティ上の弱点

**普及度 普通** 

**検出難易度 普通**

最近のモバイルアプリケーションはネットワークトラフィックの保護を目的としていますが、その実装には一貫性がないことがよくあります。このような非一貫性はデータやセッション ID を傍受にさらす脆弱性につながる可能性があります。アプリがトランスポートセキュリティプロトコルを使用しているからといって、それが正しく実装されているとは限りません。基本的な欠陥を特定するには、携帯電話のネットワークトラフィックを観察します。しかし、より微細な欠陥を検出するには、アプリケーションの設計と構成を詳しく調べる必要があります。

# 技術的影響

**影響度 深刻**

この欠陥によりユーザーデータがさらされ、アカウント乗っ取り、ユーザーなりすまし、個人情報データ漏洩などにつながる可能性があります。たとえば、攻撃者はユーザー認証情報、セッション、二要素認証トークンを傍受して、より手の込んだ攻撃の扉を開く可能性があります。

# ビジネスへの影響

**影響度 中**

少なくとも、通信チャネルを介した機密データの傍受はプライバシーの侵害につながります。

ユーザーの機密性を侵害すると以下のような結果を招く可能性があります。

* なりすまし
* 詐欺
* 風評被害

# 「安全でない通信」の脆弱性があるか？

このリスクはポイント A からポイント B へのデータ転送のあらゆる側面をカバーしますが、それを安全に行うことはありません。これにはモバイル間通信、アプリからサーバーへの通信、モバイルから他のものへの通信が含まれます。このリスクにはモバイルデバイスが使用する可能性のあるすべての通信テクノロジ (TCP/IP, Wi-Fi, Bluetooth/Bluetooth-LE, NFC, オーディオ, 赤外線, GSM, 3G, SMS など) が含まれます。

TLS 通信の問題はすべてここにあります。NFC, Bluetooth, Wi-Fi に関する問題はすべてここにあります。

顕著な特徴としては、ある種の機密データをパッケージ化してデバイスの内外に送信することが挙げられます。機密データの例としては、暗号鍵、パスワード、個人ユーザー情報、アカウント情報、セッショントークン、ドキュメント、メタデータ、バイナリなどがあります。機密データはサーバーからデバイスに送信されることや、アプリからサーバーに送信されることや、デバイスと他のローカルなもの (NFC 端末や NFC カードなど) の間で送信されることがあります。このリスクを定義付ける特徴は二つのデバイスが存在し、その間を何らかのデータがやり取りされることです。

データがデバイス自体のローカルに保存される場合、それは #Insecure Data です。セッション情報が安全に (強力な TLS 接続を介するなどで) 通信されているが、セッション識別子自体が不適切 (予測可能であったり、エントロピーが低いなど) である場合、それは #Insecure Authentication の問題であり、通信の問題ではありません。

安全でない通信の通常のリスクはデータ完全性、データ機密性、オリジン完全性に関するものです。転送中に (中間者攻撃を介するなどで) データが変更される可能性があり、その変更が検出できない場合、それがこのリスクの良い例です。通信の様子を観察 (すなわち盗聴) したり、会話の様子を記録し後から攻撃 (オフライン攻撃) することによって、機密データが開示、学習、導出される可能性がある場合、それも安全でない通信の問題です。TLS 接続の適切な設定とバリデートの失敗 (証明書チェック、弱い暗号、その他の TLS 構成の問題など) もすべてこの安全でない通信となります。

# 「安全でない通信」を防ぐには？

**General Best Practices**

* Assume that the network layer is not secure and is susceptible to eavesdropping.
* Apply SSL/TLS to transport channels that the mobile app will use to transmit data to a backend API or web service.
* Account for outside entities like third-party analytics companies, social networks, etc. by using their SSL versions when an application runs a routine via the browser/webkit. Avoid mixed SSL sessions as they may expose the user’s session ID.
* Use strong, industry standard cipher suites with appropriate key lengths.
* Use certificates signed by a trusted CA provider.
* Never allow bad certificates (self-signed, expired, untrusted root, revoked, wrong host..).
* Consider certificate pinning.
* Always require SSL chain verification.
* Only establish a secure connection after verifying the identity of the endpoint server using trusted certificates in the key chain.
* Alert users through the UI if the mobile app detects an invalid certificate.
* Do not send sensitive data over alternate channels (e.g, SMS, MMS, or notifications).
* If possible, apply a separate layer of encryption to any sensitive data before it is given to the SSL channel. In the event that future vulnerabilities are discovered in the SSL implementation, the encrypted data will provide a secondary defense against confidentiality violation.
* During development cycles, avoid overriding SSL verification methods to allow untrusted certificates, instead try using self-signed certificates or a local development certificate authority (CA)
* During security assessments, it is advised to analyze application traffic to see if any traffic goes through plaintext channels  

**iOS Specific Best Practices**

Default classes in the latest version of iOS handle SSL cipher strength negotiation very well. Trouble comes when developers temporarily add code to bypass these defaults to accommodate development hurdles. In addition to the above general practices:

* Ensure that certificates are valid and fail closed.
* When using `CFNetwork`, consider using the Secure Transport API to designate trusted client certificates. In almost all situations, `NSStreamSocketSecurityLevelTLSv1` should be used for higher standard cipher strength.
* After development, ensure all `NSURL` calls (or wrappers of `NSURL`) do not allow self signed or invalid certificates such as the `NSURL` class method `setAllowsAnyHTTPSCertificate`.
* Consider using certificate pinning by doing the following: export your certificate, include it in your app bundle, and anchor it to your trust object. Using the NSURL method `connection:willSendRequestForAuthenticationChallenge`: will now accept your cert.

**Android Specific Best Practices**

* Remove all code after the development cycle that may allow the application to accept all certificates such as org.apache.http.conn.ssl.AllowAllHostnameVerifier or SSLSocketFactory.ALLOW_ALL_HOSTNAME_VERIFIER. These are equivalent to trusting all certificates.
* If using a class which extends SSLSocketFactory, make sure checkServerTrusted method is properly implemented so that server certificate is correctly checked.
* Avoid overriding `onReceivedSslError` to allow invalid SSL certificates

# 攻撃シナリオの例

There are a few common scenarios that penetration testers frequently discover when inspecting a mobile app's communication security:

**Lack of certificate inspection**

 The mobile app and an endpoint successfully connect and perform a TLS handshake to establish a secure channel. However, the mobile app fails to inspect the certificate offered by the server and the mobile app unconditionally accepts any certificate offered to it by the server. This destroys any mutual authentication capability between the mobile app and the endpoint. The mobile app is susceptible to man-in-the-middle attacks through a TLS proxy.

**Weak handshake negotiation**

 The mobile app and an endpoint successfully connect and negotiate a cipher suite as part of the connection handshake. The client successfully negotiates with the server to use a weak cipher suite that results in weak encryption that can be easily decrypted by the adversary. This jeopardizes the confidentiality of the channel between the mobile app and the endpoint.

**Privacy information leakage**

 The mobile app transmits personally identifiable information to an endpoint via non-secure channels instead of over SSL/TLS. This jeopardizes the confidentiality of any privacy-related data between the mobile app and the endpoint.

**Credential information leakage**

 The mobile app transmits user credentials to an endpoint via non-secure channels instead of over SSL/TLS. This allows an adversary to intercept those credentials in cleartext.

**Two-Factor authentication bypass**

 The mobile app receives a session identifier from an endpoint via non-secure channels instead of over SSL/TLS. This allows an adversary to bypass two-factor authentication by using the intercepted session identifier.


# 参考資料

- OWASP
  - [OWASP](https://www.owasp.org/)
- その他
  - [External References](http://cwe.mitre.org/)
