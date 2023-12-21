---
layout: col-sidebar
title: "M6: 不適切なプライバシーコントロール (Inadequate Privacy Controls)"
---

# 脅威エージェント

**アプリケーション依存**

プライバシーコントロールは、氏名と住所、クレジットカード情報、電子メールと IP アドレス、健康、宗教、性的志向、政治的意見などの個人を識別できる情報 (PII) を保護することに関係します。

この情報は攻撃者にとっていくつかの理由で価値があります。たとえば、攻撃者は以下のようなことができる可能性があります。
- 被害者になりすまして詐欺を行います。
- 被害者の支払いデータを悪用します。
- 機密情報で被害者を脅迫します。
- 被害者の重要なデータを破壊または操作して、被害者に損害を与えます。

一般的に、PII は漏洩 (機密性の侵害)、操作 (完全性の侵害)、破壊/遮断 (可用性の侵害) のいずれかの可能性があります。


# 攻撃手法

**悪用難易度 普通**

PII の一般的なソースは、アプリのサンドボックス、サーバーとのネットワーク通信、アプリのログやバックアップなど、十分に保護されています。URL クエリパラメータやクリップボードコンテンツなど、保護が十分でないものもありますが、依然としてアクセスは困難です。

そのため、PII を取得するには、攻撃者はまず別のレベルでセキュリティを突破する必要があります。攻撃者はネットワーク通信を盗聴したり、トロイの木馬でファイルシステム、クリップボード、ログにアクセスしたり、モバイルデバイスを手に入れて解析用のバックアップを作成する可能性があります。PII はモバイルデバイスで利用可能なあらゆる手段で保存、処理、転送可能なデータに過ぎないため、それを抽出または操作する可能性は多岐にわたります。


# セキュリティ上の弱点

**普及度 普通**

**検出難易度 容易**

ほぼすべてのアプリは何らかの PII を処理します。多くの場合、その目的を果たすために必要以上に収集および処理するため、ビジネス上にニーズがなくてもターゲットとしてより魅力的になります。

開発者による PII の不注意な取扱いにより、プライバシー侵害のリスクは増大します。PII は攻撃者が通信や記憶メディアにアクセスできる可能性を常に念頭に置いて処理すべきです。

したがって、アプリが収集する個人データの一部が、不十分に保護されたストレージや伝送メディアを介して、攻撃者にそのようなデータを操作したり悪用する動機を与えるのであれば、アプリはプライバシー侵害に対して脆弱になります。


# 技術的影響

**影響度 低**

通常、プライバシー侵害はシステム全体に技術的影響はほとんど与えません。PII に認証データなどの情報が含まれている場合にのみ、追跡可能性などの特定のグローバルセキュリティプロパティに影響を与える可能性があります。

ユーザーデータが操作されると、そのユーザーはシステムを使用できなくなる可能性があります。適切なサニタイゼーションや例外処理が行われていない場合、不正なデータによりバックエンドが妨害される可能性もあります。


# ビジネスへの影響

**影響度 深刻**

プライバシー侵害がビジネスに与える影響の程度と深刻度は、影響を受けるユーザー数、影響を受けるデータの重要性、侵害が発生した場所で適用されるデータ保護規制によって大きく異なります。プライバシー侵害によるビジネスへの影響は一般的に少なくとも以下のような結果をもたらします。

**法的規制の違反:** 規制がプライバシーコントロールに関する最大の問題です。関連法規の例としては GDPR (欧州), CCPA (カリフォルニア, 米国), PDPA (シンガポール), PIPEDA (カナダ), LGPD (ブラジル), Data Protection Act 2018 (米国), POPIA (南アフリカ), PDPL (中国) があり、ユーザーのデータを保護しない企業に対する制裁措置が知られています。

**被害者の訴訟による経済的損害:** プライバシー侵害によって個人的な影響を受けた人は、侵害が起きたアプリプロバイダを訴える可能性があります。このような訴訟は適用される法的規制と、適切かつ最新の保護メカニズムを導入していること示すプロバイダの能力によっては勝訴する可能性があります。

**風評被害:** プライバリー侵害が大規模にユーザーに影響を与える場合、おそらくメディアに掲載され、アプリのプロバイダに否定的な評判がもたらされます。その結果、そのアプリや同じプロバイダの他の無関係な製品の売上や利用が減少するかもしれません。

**PII の紛失や窃取:** 実際に盗まれた情報はアプリのプロバイダへの攻撃にも悪用されるかもしれません。たとえば、特定のユーザーデータを使用して、被害者になりすましてプロバイダに対してソーシャルエンジニアリング攻撃を行う可能性があります。


# 「不適切なプライバシーコントロール」の脆弱性があるか？

アプリが不適切なプライバシーコントロールに対して脆弱になる可能性があるのは、何らかの形で個人を識別できる情報を処理する場合のみです。これはほとんどの場合に当てはまります。サーバーから見えるクライアントアプリの IP アドレス、アプリの使用状況のログ、クラッシュレポートやアナリティクスで送信されるメタデータはほとんどのアプリに適用される PII です。通常、アプリはユーザーからアカウント、支払いデータ、位置情報など、さらに機密性の高い PII を収集して処理します。

PII を使用するアプリでは、他の機密データと同様に公開するかもしれません。これは特に以下のようなものを通じて起こります。

- 安全でないデータストレージと通信 (参照 [M5](m5-insecure-communication.md), [M9](m9-insecure-data-storage.md))
- 安全でない認証と認可でのデータアクセス (参照 [M3](m3-insecure-authentication-authorization.md), [M1](m1-improper-credential-usage.md))
- アプリのサンドボックスに対するインサイダー攻撃 (参照 [M2](m2-inadequate-supply-chain-security.md), [M4](m4-insufficient-input-output-validation.md), [M8](m8-security-misconfiguration.md)).

他の OWASP モバイル Top 10 リスクはアプリがさまざまな攻撃ベクトルに対してどのように脆弱になるかについてより深い洞察を提供します。


# 「不適切なプライバシーコントロール」を防ぐには？

存在しないものは攻撃できないため、プライバシー侵害を防ぐための最も安全なアプローチは、処理される PII の量と種類を最小限に抑えることです。これには特定のアプリ内のすべての PII 資産を完全に認識する必要があります。その認識の上で、以下の質問を評価する必要があります。

- 処理されるすべての PII は本当に必要ですか？ (たとえば名前と住所、性別、年齢など)
- PII の一部を重要度の低い情報に置き換えることはできますか？ (たとえば詳細な位置情報を粗い位置情報に) 
- PII の一部を削減することはできますか？ (たとえば位置情報の更新を毎分ではなく毎時に)
- PII の一部を匿名化や不鮮明化することはできますか？ (たとえばハッシュ化、バケット化、ノイズ付加により)
- PII の一部を一定の有効期限後に削除できますか？  (たとえば先週の健康データのみ保持するなど)
- ユーザーはオプションの PII の使用に同意できますか？ (たとえばより良いサービスを受けたいが追加のリスクも承知して)

The remaining PII should not be stored or transferred unless absolutely necessary. If it must be stored or transferred, access must be protected with proper authentication and possibly authorization. Also defense in depth should be considered for particularly critical data. For example, health data may be encrypted with a key sealed in the device's TPM in addition to its storage in the app's sandbox. So, if an attacker manages to circumvent the sandbox restrictions, the data is still not readable. The other OWASP Mobile Top 10 risks suggest measures to securely store, transfer, access and otherwise handle sensitive data. 

Threat modeling can be used to determine the most likely ways that privacy violations may occur in a given app. The effort of securing PII could then be focused on these. 

Static and dynamic security checking tools might reveal common pitfalls, like logging of sensitive data or leakage to clipboard or URL query parameters.


# 攻撃シナリオの例

The following scenarios showcase inadequate privacy controls in mobile apps: 

**シナリオ #1:** Inadequate sanitization of logs and error messages. 

Reporting of logs and exceptions is essential for quality assurance of a productive app. Crash reports and other usage data helps developers to fix bugs and learn about how their app is used. However, logs and error messages might contain PII if the developers chose to include this data in log or error messages. Also, third party libraries might include PII in their error messages and logs as well. An example of a frequent issue are database exceptions that reveal part of the query or result. This will most likely be visible to any platform provider used for collecting and evaluating crash reports. It might also become visible to the user if the error is displayed on screen or to attackers who can read device logs. Developers should be especially careful in what they log and ensure that exception messages are sanitized before displaying them to the user or reporting them to a server. 

**シナリオ #2:** Using PII in URL query parameters. 

URL query parameters are often used to transmit request arguments to a server. However, URL query parameters are visible at least in the server logs, but often also in website analytics and possibly in the local browser history. So sensitive information should never be transmitted as query parameters. Instead, they should be sent as a header or part of the body. 

**シナリオ #3:** Exclusion of personal data in backups/not setting hasFragileUserData. 

Most PII processed by an app is stored in its sandbox. The app should explicitly configure what data to include in device backups. An attacker might obtain a device and create a backup or get a backup from another source, from which the sandbox content could be extracted. 

Alternatively, by setting hasFragileUserData to 'true' in Android, an app may preserve its data upon uninstallation. An attacker who manages to install a malicious app with the same package id later can access this data. 

Hence, both settings should be explicitly set for apps to make the developers' intent transparent and to control the information flow through backups or between subsequent installations of an app. 


# 参考資料

- OWASP
  - [User Privacy Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/User_Privacy_Protection_Cheat_Sheet.html)
  - [Testing User Privacy Protection (MASTG)](https://mas.owasp.org/MASTG/General/0x04i-Testing-User-Privacy-Protection/)
  - [OWASP Top 10 Privacy Risks](https://owasp.org/www-project-top-10-privacy-risks/)
  - [OWASP Top 10 for Large Language Models: LLM06: Sensitive Information Disclosure](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- その他
  - [EU General Data Protection Regulation](https://gdpr.eu/)
