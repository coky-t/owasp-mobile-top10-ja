---

layout: col-sidebar
title: "M9: リバースエンジニアリング"
---

# 脅威エージェント

**アプリケーション依存**

攻撃者は一般的にアプリストアから対象のアプリをダウンロードしてから、ローカル環境内でさまざまなツールを使用して解析します。

# 攻撃手法

**悪用難易度 容易**

攻撃者はアプリに埋め込まれたオリジナルの文字列テーブル、ソースコード、ライブラリ、アルゴリズム、リソースを見つけ出すために、最終的なコアバイナリの解析を行う必要があります。攻撃者は IDA Pro, Hopper, otool, strings, その他のバイナリ検査ツールなどの比較的手頃な価格のよく理解されているツールを攻撃者の環境内で使用します。

# セキュリティ上の弱点

**普及度 中** <br />
**検出難易度 容易**

概して、すべてのモバイルコードはリバースエンジニアリングに脆弱です。一部のアプリは他のアプリよりも脆弱です。実行時に動的なイントロスペクションを可能にする言語/フレームワーク (Java, .NET, Objective C, Swift) で書かれたコードは特にリバースエンジニアリングのリスクがあります。リバースエンジニアリングの脆弱性を検出することはとても簡単です。まず、(バイナリ暗号化が適用されている場合) アプリストアバージョンのアプリを復号化します。次に、このドキュメントの "攻撃手法" セクションに記載されているツールをバイナリに対して使用します。これらのコードにより生成されたアプリのコントロールフローパス、文字列テーブル、疑似コード/ソースコードを理解することが非常に容易である場合、コードは脆弱となります。

# 技術的影響

**影響度 中程度**

攻撃者はリバースエンジニアリングを悪用して以下のいずれかを達成できます。
- バックエンドサーバーに関する情報を開示する
- 暗号化定数と暗号を開示する
- 知的財産を盗む
- バックエンドシステムに対する攻撃を実行する
- 後続するコード改変を実行するために必要な情報を取得する

# ビジネスへの影響

**アプリケーション / ビジネス依存**

リバースエンジニアリングによるビジネスへの影響は非常に多様です。以下が含まれます。
- 知的財産の漏洩
- 風評被害
- 個人情報漏洩
- バックエンドシステムの侵害

# 'リバースエンジニアリング' の脆弱性はあるか？

概して、ほとんどのアプリケーションはコード固有の性質によりリバースエンジニアリングの対して脆弱です。今日アプリを書くために使用されるほとんどの言語はプログラマがアプリをデバッグする際に大いに役立つメタデータが豊富にあります。この同じ機能は攻撃者がアプリの仕組みを理解する際にも大いに役立ちます。
攻撃者が以下のいずれかを実行できる場合、アプリはリバースエンジニアリングに脆弱であるといわれています。

- バイナリの文字列テーブルの内容を明確に理解する
- 関数間解析を正確に実行する
- バイナリからソースコードをある程度正確に再現する
ほとんどのアプリはリバースエンジニアリングに脆弱ですが、リバースエンジニアリングの潜在的なビジネスへの影響を調べるには、このリスクを軽減するかどうかを検討することが重要です。リバースエンジニアリングで何ができるかについては以下の例を参照ください。

# 'リバースエンジニアリング' を防ぐには？

効果的にリバースエンジニアリングを防ぐには、難読化ツールを使用する必要があります。市場には多くのフリーおよび商用の難読化ツールがあります。反対に、市場には多くのさまざまな難読化解読ツールがあります。選択した難読化ツールの有効性を測定するには、IDA Pro や Hopper などのツールを使用してコードの難読化解読を試みます。

よい難読化ツールは以下の能力を持ちます。

- 難読化するメソッド/コードセグメントを絞り込む
- パフォーマンスへの影響をバランスさせるために難読化の程度を調整する
- IDA Pro や Hopper などのツールによる難読化解読に耐える
- メソッドと同様に文字列テーブルも難読化する

# 攻撃シナリオの例

**シナリオ #1**: 文字列テーブル解析:

攻撃者は暗号化されていないアプリに対して 'strings' を実行します。文字列テーブル解析の結果として、攻撃者はバックエンドデータベースへの認証資格情報を含むハードコードされた接続文字列を発見します。攻撃者はこれらの資格情報を使用してデータベースにアクセスします。攻撃者はアプリのユーザーに関する膨大な量の PII データを盗みます。

**シナリオ #2**: 関数間解析:

攻撃者は暗号化されていないアプリに対して IDA Pro を使用します。文字列テーブル解析と関数の相互参照を組み合わせた結果として、攻撃者は脱獄検出コードを発見します。攻撃者はこの知識を後続のコード改変攻撃に使用して、モバイルアプリ内の脱獄検出を無効にします。その後、攻撃者はメソッドスウィズリングを悪用するバージョンのアプリを展開して顧客情報を盗みます。

**シナリオ #3**: ソースコード解析:

銀行 Android アプリケーションを考えます。APK ファイルは 7zip/Winrar/WinZip/Gunzip を使用して簡単に抽出できます。一旦抽出されると、攻撃者はマニフェストファイル、アセット、リソース、および最も重要な classes.dex ファイルを手に入れています。

それから Dex to Jar コンバータを使用すると、攻撃者は簡単に jar ファイルに変換できます。次のステップでは、(JDgui などの) Java デコンパイラがコードを提供します。

# 参考資料

- OWASP
  - [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project)
- その他

- [1] Arxan Research: [State of Security in the App Economy, Volume 2](https://www.arxan.com/assets/1/7/State_of_Security_in_the_App_Economy_Report_Vol._2.pdf), November 2013:

> “Adversaries have hacked 78 percent of the top 100 paid Android and iOS apps in 2013.”

  - [2] HP Research: [HP Research Reveals Nine out of 10 Mobile Applications Vulnerable to Attack](http://www8.hp.com/us/en/hp-news/press-release.html?id=1528865#.UuwZFPZvDi5), 18 November 2013:

> "86 percent of applications tested lacked binary hardening, leaving applications vulnerable to information disclosure, buffer overflows and poor performance. To ensure security throughout the life cycle of the application, it is essential to build in the best security practices from conception."

  - [3] North Carolina State University: [Dissecting Android Malware: Characterization and Evolution](http://www.csc.ncsu.edu/faculty/jiang/pubs/OAKLAND12.pdf), 7 September 2011:

> “Our results show that 86.0% of them (Android Malware) repackage legitimate apps to include malicious payloads; 36.7% contain platform-level exploits to escalate privilege; 93.0% exhibit the bot-like capability.”

  - [4] Tech Hive: [Apple Pulls Ripoff Apps from its Walled Garden](http://www.techhive.com/article/249310/apple_pulls_ripoff_apps_from_its_walled_garden.html) Feb 4th, 2012:

> “While Apple is known for screening apps before they are allowed to sprout up in its walled garden, clearly fake apps do get in. Once they do, getting them out depends on developers who raise a fuss.”

  - [5] Tech Crunch: [Developer Spams Google Play With RipOffs of Well-Known Apps… Again](http://techcrunch.com/2014/01/02/developer-spams-google-play-with-ripoffs-of-well-known-apps-again/), January 2 2014:

> “It’s not uncommon to search the Google Play app store and find a number of knock-off or “fake” apps aiming to trick unsuspecting searchers into downloading them over the real thing.”

  - [6] Extreme Tech: [Chinese App Store Offers Pirated iOS Apps Without the Need To Jailbreak](http://www.extremetech.com/mobile/153849-chinese-app-store-offers-pirated-ios-apps-without-the-need-to-jailbreak), April 19 2013:

> “The site offers apps for free that would otherwise cost money, including big-name titles.”

  - [7] OWASP: [Architectural Principles That Prevent Code Modification or Reverse Engineering](https://www.owasp.org/index.php/Architectural_Principles_That_Prevent_Code_Modification_or_Reverse_Engineering), January 11th 2014.

  - [8] Gartner report: Avoiding Mobile App Development Security Pitfalls, 24 May 2013:

> "For critical applications, such as transactional ones and sensitive enterprise applications, hardening should be used."

  - [9] Gartner report: Emerging Technology Analysis: Mobile Application Shielding, March 26th, 2013:

> "As more regulated and sensitive data applications move to mobile platforms the need to increase data protection increases. Mobile application shielding presents the opportunity to security providers to offer higher data protection standards to mobile platforms that exceed mobile OS security."

  - [10] Gartner report: Proliferating Mobile Transaction Attack Vectors and What to Do About Them, March 1st, 2013:

> "Use mobile application security testing services and self-defending application utilities to help prevent hacking attempts."

  - [11] Gartner report: Select a Secure Mobile Wallet for Proximity, March 1st, 2013:

> "Application hardening can fortify sensitive business code against hacking attempts, such as reverse engineering”

  - [12] Forrester paper: Choose The Right Mobile Development Solutions For Your Organization, May 6th 2013:

> “5 Key Protections: Data Protection, App Compliance, App-Level Threat Defense, Security Policy Enforcement, App Integrity”

  - [13] John Wiley and Sons, Inc: [iOS Hacker's Handbook](http://www.amazon.com/iOS-Hackers-Handbook-Charlie-Miller/dp/1118204123), Published May 2012, [ISBN 1118204123](https://wiki.owasp.org/index.php/Special:BookSources/1118204123).

  - [14] McGraw Hill Education: [Mobile Hacking Exposed](http://mobilehackingexposed.com/), Published July 2013, [ISBN 0071817018](https://wiki.owasp.org/index.php/Special:BookSources/0071817018).

  - [15] Publisher Unannounced: [Android Hacker's Handbook](http://www.amazon.com/Android-Hackers-Handbook-Joshua-Drake/dp/111860864X), To Be Published April 2014.

  - [16] Software Development Times: [More than 5,000 apps in the Google Play Store are copied APKs, or 'thief-ware'](http://sdt.bz/66393#ixzz2sHa7dFMp), November 20 2013:

> “In most cases, the 2,140 copycat developers that were found reassembled the apps almost identically, adding new advertising SDKs to siphon profits away from the original developers.

  - [17] InfoSecurity Magazine: [Two Thirds of Personal Banking Apps Found Full of Vulnerabilities](http://www.infosecurity-magazine.com/view/36376/two-thirds-of-personal-banking-apps-found-full-of-vulnerabilities/), January 3 2014:

> “But one of his more worrying findings came from disassembling the apps themselves ... what he found was hardcoded development credentials within the code. An attacker could gain access to the development infrastructure of the bank and infest the application with malware causing a massive infection for all of the application’s users.”

  - [18] InfoSecurity Magazine: [Mobile Malware Infects Millions; LTE Spurs Growth](http://www.infosecurity-magazine.com/view/36686/mobile-malware-infects-millions-lte-spurs-growth/), January 29 2014:

> "Number of mobile malware samples is growing at a rapid clip, increasing by 20-fold in 2013... It is trivial for an attacker to hijack a legitimate Android application, inject malware into it and redistribute it for consumption. There are now binder kits available that will allow an attacker to automatically inject malware into an existing application"
