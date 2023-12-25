---

layout: col-sidebar
title: "M7: 不十分なバイナリ保護 (Insufficient Binary Protection)"
---

# 脅威エージェント

**アプリケーション依存**

アプリバイナリを狙う攻撃者の動機はさまざまです。

バイナリには商用 API 鍵やハードコードされた暗号シークレットなど、攻撃者が悪用できる貴重なシークレットが含まれる可能性があります。さらに、バイナリ内のコードには重要なビジネスロジックや事前訓練された AI モデルが含まれているなど、それ自体に価値がある可能性があります。また、攻撃者の中にはアプリ自体を狙うのではなく、アプリを使用して対応するバックエンドの潜在的な弱点を探り、攻撃に備えているかもしれません。

攻撃者は情報収集だけでなく、アプリバイナリを操作して有料機能に無料でアクセスしたり、他のセキュリティチェックを回避する可能性もあります。最悪の場合、人気のあるアプリが悪意のあるコードを含むように改変されて、サードパーティのアプリストア経由で配布されたり、新しい名前で配布されて、疑いを持たないユーザーを搾取します。よくある攻撃例としては、アプリ内の決済識別子を再構成し、再パッケージ化し、アプリストア経由で配布するものがあります。それから、ユーザーがこの不正コピーをアプリストアからダウンロードすると、元のプロバイダではなく攻撃者が支払いを受け取ります。


# 攻撃手法

**悪用難易度 容易**

通常、アプリバイナリはアプリストアからダウンロードしたり、モバイルデバイスからコピーできるため、バイナリ攻撃を仕組むのは簡単です。

アプリバイナリは以下の二種類の攻撃を受ける可能性があります。

- リバースエンジニアリング: アプリバイナリを逆コンパイルし、秘密鍵、アルゴリズム、脆弱性などの貴重な情報をスキャンします。
- コード改竄: アプリバイナリを操作して、ライセンスチェックを削除したり、ペイウォールを回避したり、ユーザーとして他の利益を得るなどします。あるいは、アプリを操作して、悪意のあるコードを含めることもできます。

# セキュリティ上の弱点

**普及度 普通**

**検出難易度 容易**

すべてのアプリはバイナリ攻撃に対して脆弱であり、多くはいつかは何らかの形で攻撃の対象になるでしょう。機密データやアルゴリズムがバイナリにハードコードされているアプリは、バイナリ攻撃に対して特に脆弱です。このようなアプリには、保護を突破することに成功した場合のコストのほうがその成功による利益よりも高くつくように、攻撃者が諦めるのに十分長い時間、潜在的な攻撃者を防御するための対策を採用する必要があります。多くの場合、たとえばコピープロテストの場合など、アプリ販売による目標収益に達するまでクラッキングプロセスを長引かせるだけで十分です。

一般的に、iOS アプリのような完全にコンパイルされたアプリは Android アプリにみられる高レベルのバイトコードよりもリバースエンジニアリングやコード改竄の影響を受けにくくなります (これは PWA や Flutter などのクロスプラットフォームテクノロジで開発されたアプリには当てはまらないかもしれないことに注意してください) 。

特に人気のあるアプリは操作され、アプリストアを通じて再配布されやすくなります。このような操作されたコピーの検出と削除は専門会社によって提供されていますが、アプリ自体内での特定の検出および報告メカニズムでも可能です。

バイナリ攻撃を防ぐ完全に信頼できるメカニズムは存在しないことに注意してください。それらに対する防御は、対策に投資する開発者と、このような対策を破る攻撃者との激しい競争になります。そのため、それぞれのアプリで答えるべき質問が次のようになります。バイナリ攻撃対策にどの程度の労力を注ぐべきですか？


# 技術的影響

**影響度 中**

前述したように、バイナリ攻撃はリバースエンジニアリングでアプリバイナリから情報を漏洩するか、コード改竄でアプリの動作を改変するかのいずれかで発生する可能性があります。

シークレットが漏洩した場合は、システム全体で迅速に置き換える必要がありますが、アプリにシークレットがハードコードされている場合は困難です。バイナリからの情報漏洩によってバックエンドのセキュリティ脆弱性が明らかになる可能性もあります。

しかし、操作はシステムの技術的な健全性にさらに影響をあたえます。攻撃者はバイナリを操作することで、たとえば、悪意のあるリクエストに対して十分に堅牢化されていない場合、自分たちの利益を得たりバックエンドを妨害するなど、アプリの動作を任意に変更できます。


# ビジネスへの影響

**影響度 中**

商用 API などの API キーの漏洩は、大規模に悪用されると多大なコストが発生する可能性があります。改竄されてライセンスチェックを削除されたり競合アプリで機能を公開されたアプリも同様です。いずれの場合も、個人使用のために個人がアプリをクラックしたり API キーを盗んでもおそらく気付かれないでしょう。しかし規模が大きくなると、たとえば API キーや機能が他のアプリで組織的に使用される場合、悪意のある競合のほうがコストが大幅に低いために大きな優位性を得る可能性があります。

多大な労力を払って開発されたアルゴリズムや AI モデルなどの知的財産が公になったり悪意のある競合に盗まれると、アプリ開発者のビジネスモデルはさらに脅かされるかもしれません。

特に人気のあるアプリが悪意のあるコードとともに再配布されると、大きな風評被害が生じる可能性があります。アプリプロバイダが改竄されたアプリのコピーの再配布を防ぐことはほとんどできませんが、ネガティブな評判はおそらくオリジナルのプロバイダに向けられるでしょう。したがって、不正コピーの再配布は攻撃者にとって可能な限り困難にして、このリスクの可能性を減らすべきです。


# 「不十分なバイナリ保護」の脆弱性があるか？

すべてのアプリはバイナリ攻撃に対して脆弱です。アプリがそのバイナリに機密データやアルゴリズムをハードコードしている場合やアプリが非常に人気がある場合、バイナリ攻撃は特に害を及ぼす可能性があります。難読化や、ネイティブコードでのシークレットのエンコード (Android の場合) など、追加の保護手段があれば、攻撃の成功はより困難になりますが、決して不可能ではありません。

アプリが十分に安全かどうかはさまざまなバイナリ攻撃が与える可能性があるビジネスへの影響によって異なります。攻撃者の動機付けが大きくなり、影響が大きくなるほど、保護に一層の労力を注ぐべきです。したがって、バイナリ攻撃への「脆弱性」は特定のアプリに非常に固有なものとなります。

簡単なチェックとして、開発者は攻撃者が使用するのと同じツールを使用して自分のアプリバイナリを検査できます。MobSF, otool, apktool, Ghidra などの無料または手頃な価格のツールは多数あり、非常に使いやすく、ドキュメントも充実しています。


# 「不十分なバイナリ保護」を防ぐには？

アプリごとに、バイナリに重要なコンテンツが含まれているかどうかや、その人気によりバイナリ保護を義務付けられているかどうかを評価すべきです。もしそうであれば、脅威モデリング分析は最も高いリスクと、そのリスクが発生した場合に予想される経済的影響を特定するのに役立ちます。最も関連性の高いリスクについては、対策を講じるべきです。

アプリは常に信頼できない環境で動作し、情報は常に漏洩や操作されるリスクにさらされるため、動作に必要となる最小限の情報のみを取得すべきです。しかし、特定のシークレット、アルゴリズム、セキュリティチェックなどがアプリのバイナリ内になければならないとすると、さまざまな攻撃をさまざまな手段で回避できます。

**Reverse engineering:** To prevent reverse engineering, the app binary should be made incomprehensible. This is supported by many free and commercial obfuscation tools. Compiling part of apps natively (iOS and Android) or using interpreters or nested virtual machines makes reverse engineering even harder, as many decompiling tools only support one language and binary format. This kind of obfuscation is a tradeoff between the complexity of the code and robustness against reverse engineering, as many libraries that rely on certain strings or symbols in the code will not work with full obfuscation. Developers could check the quality of their obfuscation by using the tools from the previous section.

**Breaking security mechanisms:** Obfuscation also helps against manipulation, as an attacker must understand the control flow in order to skip security checks and like. In addition, local security checks should also be enforced by the backend. For example, required resources for a protected feature should only be downloaded if a check succeeds locally and in the backend. Finally, integrity checks could detect code tampering and render the app installation unusable, e.g., by deleting some resources. However, such an integrity check could also be found and deactivated as any other local security check.

**Redistribution** (with malicious code): Integrity checks, e.g., on startup, could also detect redistribution and modification of app binaries. These violations could automatically be reported to find and remove the unauthorized copies of the app from the app stores before they become widespread. There are also specialized companies that support this use case.


# 攻撃シナリオの例

**シナリオ #1** Hardcoded API keys: Assume an app uses a commercial API where it must pay a small fee for each call. These calls would be easily paid for by the subscription fee the users pay for that app. However, the API key used for access and billing is hardcoded in the app's unprotected binary code. An attacker who wants access could reverse engineer the app with free tools and get access to the secret string. Since API access is only protected with the API key and no additional user authentication, the attacker can freely work on the API or even sell the API key. In the worst case, the API keys could be misused a lot, causing substantial financial damage to the provider of the app, or at least blocking legitimate users of the app if the API access is rate-limited. 

**シナリオ #2** Disabling payment and license checks: A mobile game might publish its app and the first levels for free. If the users like the game, they pay for full access. All the resources for the later levels are shipped with the app. They are only protected by a license check, where the license is downloaded when the user pays. An attacker could reverse engineer the app and try to understand how the verification of the payment happens. If the app binary is not sufficiently protected, it is easy to locate the license check and just replace it with a static success statement. The attacker can then recompile the app and play it for free or even sell it under another name in the app stores.

**シナリオ #3** Hardcoded AI models: Assume a medical app that features an AI to answer user requests given as speech or free text inputs needs. This app includes its specialized and quality-assured AI model in its source code to enable offline access and avoid hosting own download servers. This AI model is the most valuable asset of this app and took many person-years in development. An attacker might try to extract this model from the source code and sell it to competitors. If the app binary is insufficiently protected, the attacker could not only access the AI model, but also learn how it is used, selling this information along with the AI training parameters.


# 参考資料

- OWASP
  - [Tampering and Reverse Engineering (MASTG)](https://mas.owasp.org/MASTG/General/0x04c-Tampering-and-Reverse-Engineering/)
  - [Tampering and Reverse Engineering iOS (MASTG)](https://mas.owasp.org/MASTG/iOS/0x06c-Reverse-Engineering-and-Tampering/)
  - [Tampering and Reverse Engineering Android (MASTG)](https://mas.owasp.org/MASTG/Android/0x05c-Reverse-Engineering-and-Tampering/)
  - [OWASP Reverse Engineering and Code Modification Prevention Project](https://wiki.owasp.org/index.php/OWASP_Reverse_Engineering_and_Code_Modification_Prevention_Project)
  - [OWASP Top 10 for Large Language Models: LLM10: Model Theft](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

- その他
  - [External References](http://cwe.mitre.org/)
