---

layout: col-sidebar
title: "M8: コード改竄"
---

# 脅威エージェント

**アプリケーション依存**

一般的に、攻撃者はサードパーティのアプリストアにホストされる悪意のある形式のアプリを介してコードを改竄します。また、攻撃者はフィッシング攻撃によってユーザーを騙してアプリをインストールする可能性もあります。

# 攻撃手法

**悪用難易度 容易**

一般的に、攻撃者はこのカテゴリを悪用するために以下のことを行います。
- アプリケーションパッケージのコアバイナリに対して直接バイナリ変更を行う
- アプリケーションパッケージ内のリソースに対して直接バイナリ変更を行う
- システム API をリダイレクトや置換で横取りし、悪意のある外部コードを実行する

# セキュリティ上の弱点

**普及度 中** <br />
**検出難易度 普通**

アプリケーションが改変されることはあなたが思うより驚くほど一般的です。セキュリティ業界全体がアプリストア内のモバイルアプリの不正バージョンの検出と削除を中心に構築されています。コード改変の検出の問題を解決するためのアプローチに応じて、組織は現在出回っている不正バージョンのコードを検出するための成功率の高い方法に限定することができます。
このカテゴリには、バイナリパッチ、ローカルリソースの変更、メソッドフック、メソッドスウィズリング、動的メモリの変更が含まれます。

アプリケーションがモバイルデバイスに配信されると、コードとデータリソースがそこに常駐します。攻撃者はコードを直接変更したり、メモリの内容を動的に変更したり、アプリケーションが使用するシステム API を変更もしくは置換したり、アプリケーションのデータやリソースを変更することができます。これにより、攻撃者は個人的もしくは金銭的利益のためにソフトウェアの意図された利用を妨害する直接的な方法を提供できます。

# 技術的影響

**影響度 深刻**

コード改変の影響は改変そのものの性質に応じて広域にわたります。典型的なタイプの影響は以下のとおりです。
- 不正な新機能
- 個人情報漏洩
- なりすまし

# ビジネスへの影響

**アプリケーション / ビジネス依存**


コード改変によるビジネスへの影響は一般的に以下のようになります。
- 著作権侵害による収益損失
- 風評被害

# 'コード改竄' の脆弱性はあるか？

技術的には、すべてのモバイルコードはコード改竄に対して脆弱です。モバイルコードはコードを生成する組織の管理下にない環境内で実行されます。同時に、コードが実行される環境を変更するさまざまな方法があります。これらの変更により攻撃者はコードに手を加えて自由に改変することができます。

モバイルコードは本質的に脆弱ですが、不正なコード改変を検出および防止する価値があるかどうかを自問することが重要です。(ゲームなどの) 特定のビジネス分野向けに作成されたアプリはコード改変の影響が (ホスピタリティなどの) 他のものより非常に脆弱です。したがって、このリスクに対処するかどうかを決定する前にビジネスへの影響を検討することが重要です。

# 'コード改竄' を防ぐには？

モバイルアプリはコンパイル時にコードの完全性について知っているコードから、コードが追加もしくは変更されたことを実行時に検出できる必要があります。アプリは実行時にコードの完全性の侵害に適切に対応できる必要があります。

このタイプのリスクに対する改善戦略は [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project) の中で技術的詳細についての概要が説明されています。

**Android ルート検出**
一般的に、改変されたアプリは脱獄化もしくはルート化された環境内で実行されます。そのため、実行時にこれらのタイプの侵害された環境の検出を試みて、それに応じて対処 (サーバーへの報告やシャットダウン) することが合理的です。ルート化された Android 端末を検出する一般的な方法があります: test-keys の確認

- build.prop に開発者ビルドや非公式 ROM であることを示す ro.build.tags=test-keys の行があるかどうかを確認する

OTA 証明書の確認

- /etc/security/otacerts.zip ファイルが存在するかどうかを確認する

既知のルート化 apk の確認

- com.noshufou.android.su
- com.thirdparty.superuser
- eu.chainfire.supersu
- com.koushikdutta.superuser

SU バイナリの確認

- /system/bin/su
- /system/xbin/su
- /sbin/su
- /system/su
- /system/bin/.ext/.su

SU コマンドの直接試行

- su コマンドを実行してみてからカレントユーザーの id を確認する、0 が返された場合は su コマンドが成功している

**iOS 脱獄検出**

# 攻撃シナリオの例

アプリストア全体で利用可能な偽造アプリケーションが多数あります。これらのなかにはマルウェアのペイロードを含むものもあります。改変されたアプリの多くは元のコアバイナリと関連するリソースの改変された形式が含まれています。攻撃者はこれを新しいアプリケーションとして再パッケージしてサードパーティストアにリリースします。

**シナリオ #1:**

ゲームはこの方式を使用して攻撃する対象として特に人気があります。攻撃者はゲームのフリーミアム機能にお金を支払うことに関心のない人々を惹きつけます。コード内で、攻撃者はアプリケーション内課金が成功したかどうかを検出する条件付きジャンプを短絡します。このバイパスにより犠牲者はゲームアイテムや新しい能力をお金を支払うことなく手に入れることができます。攻撃者はユーザーの情報を盗むスパイウェアも仕込んでいます。

**シナリオ #2:**

銀行アプリも攻撃対象として人気があります。これらのアプリは一般的に攻撃者にとって価値のある機密情報を処理します。攻撃者はユーザーの個人識別情報 (PII) やユーザー名/パスワードをサードパーティサイトに送信する偽造バージョンのアプリを作成する可能性があります。これはデスクトップで連想される Zeus マルウェアと同等のものです。これは一般的に銀行に対するなりすましにつながります。

# 参考資料

- OWASP
  - [OWASP Reverse Engineering and Code Modification Prevention Project](https://www.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project)
- その他
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
