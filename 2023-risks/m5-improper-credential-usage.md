---

layout: col-sidebar
title: "M5: 不適切なクレデンシャルの使用 (Improper Credential Usage)"
---

# 脅威エージェント

**アプリケーション依存**

Threat agents exploiting hardcoded credentials and improper credential usage in mobile applications can include automated attacks using publicly available or custom-built tools. Such agents could potentially locate and exploit hardcoded credentials or exploit weaknesses due to improper credential usage.

# 攻撃手法

**悪用難易度 容易**

Adversaries can exploit vulnerabilities in both hardcoded credentials and improper credential usage. Once these vulnerabilities are identified, an attacker can use hardcoded credentials to gain unauthorized access to sensitive functionalities of the mobile app. They can also misuse credentials, for instance by gaining access through improperly validated or stored credentials, thereby bypassing the need for legitimate access.

# セキュリティ上の弱点

**普及度 普通**

**検出難易度 容易**

Poor implementation of credential management, such as using hardcoded credentials and improper handling, can lead to severe security weaknesses. A comprehensive security testing process should aim to identify these issues. For instance, security testers should attempt to identify hardcoded credentials within the mobile app's source code or within any configuration files.

# 技術的影響

**影響度 深刻**

Poor credential management can lead to several significant technical impacts. Unauthorized users might gain access to sensitive information or functionality within the mobile app or its backend systems. This can lead to data breaches, loss of user privacy, fraudulent activity, and potential access to administrative functionality.

# ビジネスへの影響

**影響度 深刻**

The business impact of poor credential management, including hardcoded credentials and improper credential usage, can be substantial:

* Reputation Damage;
* Information Theft;
* Fraud;
* Unauthorized Access to Data.

# 「不適切なクレデンシャルの使用」の脆弱性があるか？

Insecure credential management can occur when mobile apps use hardcoded credentials or when credentials are misused. Here are some indicators that your mobile app may be vulnerable:

* **Hardcoded Credentials** - If the mobile app contains hardcoded credentials within the app's source code or any configuration files, this is a clear indicator of vulnerability.
* **Insecure Credential Transmission** - If credentials are transmitted without encryption or through insecure channels, this could indicate a vulnerability.
* **Insecure Credential Storage** - If the mobile app stores user credentials on the device in an insecure manner, this could represent a vulnerability.
* **Weak User Authentication** - If user authentication relies on weak protocols or allows for easy bypassing, this could be a sign of vulnerability.

# 「不適切なクレデンシャルの使用」を防ぐには？

Avoiding insecure credential management involves not using hardcoded credentials and properly handling user credentials.

**Avoid Using Hardcoded Credentials**

Hardcoded credentials can be easily discovered by attackers and provide an easy access point for unauthorized users. Always avoid using hardcoded credentials in your mobile app's code or configuration files.

**Properly Handle User Credentials**

User credentials should always be stored, transmitted, and authenticated securely:

* Encrypt credentials during transmission.
* Do not store user credentials on the device. Instead, consider using secure, revocable access tokens.
* Implement strong user authentication protocols.
* Regularly update and rotate any used API keys or tokens.

# 攻撃シナリオの例

The following scenarios showcase improper credentials usage in mobile apps:

**シナリオ #1:** Hardcoded Credentials: An attacker discovers hardcoded credentials within the mobile app's source code. They use these credentials to gain unauthorized access to sensitive functionality within the app or backend systems.

**シナリオ #2:** Insecure Credential Transmission: An attacker intercepts insecurely transmitted credentials between the mobile app and its backend systems. They use these intercepted credentials to impersonate a legitimate user and gain unauthorized access.

**シナリオ #3:** Insecure Credential Storage: An attacker gains physical access to a user's device and extracts stored credentials from the mobile app. The attacker uses these credentials to gain unauthorized access to the user's account.

# 参考資料

- OWASP
    - [OWASP](https://www.owasp.org/index.php/OWASP_Top_Ten)
- その他
    - [External References](http://cwe.mitre.org/)
