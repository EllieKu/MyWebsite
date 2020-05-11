# JSON Web Token(JWT)-JSON Web Signature 2020/05/11

## JSON Web Token 
JWT 的全名是JSON Web Token，是一種基於開放標準(RFC 7519)，它定義了一種簡潔(compact)且自包含(self-contained)的方式，用於在雙方之間安全地將訊息作為 JSON 物件傳輸。而這個訊息是經過數位簽章(Digital Signature)，因此可以被驗證及信任。可以使用密碼(經過 HMAC 演算法) 或用一對公鑰/私鑰(經過 RSA 或 ECDSA 演算法) 來對 JWT 進行簽章。<br>
儘管JWT可以加密為雙方提供保密性，但重點將放在*已簽章*token。可以驗證已簽章token包含的聲明的完整性，加密可以將聲明在其他方前隱藏。當使用公鑰/私鑰對token進行簽章時，簽名還證明只有持有私鑰的一方才是對其進行簽名的一方。<br>
> 註
> + RFC：記錄網際網路規範、協定、過程等的標準檔案。
> + 簡潔(compact)：體積非常的小，可放在 URL 、 POST 參數或 HTTP Header 內發送請求，體積小意味著傳輸速度快。
> + 自包含(self-contained)：payload 裡面就有所需要的資訊，不需要再重新 query database 的資料。
> + [數位簽章(Digital Signature)](https://zh.wikipedia.org/wiki/%E6%95%B8%E4%BD%8D%E7%B0%BD%E7%AB%A0)

## 使用時機
+ **授權(Authorization)**：這是很常見 JWT 的使用方式，例如使用者從 Client 端登入後，該使用者再次對 Server 端發送請求的時候，會夾帶著 JWT，允許使用者存取該 token 有權限的資源。單一登錄(Single Sign On)是當今廣泛使用 JWT 的功能之一，因為它的成本較小並且可以在不同的domain中輕鬆使用。
+ **訊息交換(Information Exchange)**：JWT 可以透過公鑰/私鑰來做簽章，讓我們可以知道是誰發送這個 JWT，此外，由於簽章是使用 header 和 payload 計算的，因此還可以驗證內容是否遭到篡改。

## 結構
JWT由三個部分組成並用( . )連接：
1. Header
2. Payload
3. Signature
JWT典型樣子：
    `xxxxx.yyyyy.zzzzz`

### Header
典型由兩個部分組成：<br>
+ **alg**：對JWT簽章的演算法(如HMAC SHA256 or RSA)，對於未加密的JWT值必須設置為none。
+ **typ**(optimal)：JWT本身的媒體類型。此參數僅助於將JWT與帶有JOSE header的其他對象混合使用的情況。實際上這種情況很少發生。如果存在則此聲明應設置值JWT。
+ **cty**(optimal)：內容類型。大多數 JWT 攜帶特定的聲明以及任意數據作為其 payload 的一部分，在這種情況下，不得設置內容類型聲明。對於 payload 本身是 JWT 自己（巢狀 JWT）的實例，此聲明必須存在並帶有值 JWT，用來表示需要進一步處理巢狀的 JWT。而巢狀 JWT 很少見，因此 cty 聲明很少出現在 header 中。
舉例：
```JS
{
    "alg": "HS256",
    "typ": "JWT"
}
```
### Payload
包含聲明-有關實體(通常是用戶)與其他資訊。有三種聲明類型如下：
+ **Registered claims**：
    + **iss**(optimal)：(issueer)JWT的發行方<br>
        值：區分大小寫string / URL
    + **sub**(optimal)：(subject)JWT的主題(用戶)<br>
        值：區分大小寫string / URL
    + **aud**(optimal)：(audience)JWT的目標收件人<br>
        值：區分大小寫string / URL / array
    + **exp**(optimal)：(expiration)JWT的到期時間<br>
        值：NumericDate([UNIX時間](https://zh.wikipedia.org/wiki/UNIX%E6%97%B6%E9%97%B4))
    + **nbf**(optimal)：(not before time)JWT的開始時間(exp的相反)<br>
        值：NumericDate([UNIX時間](https://zh.wikipedia.org/wiki/UNIX%E6%97%B6%E9%97%B4))
    + **iat**(optimal)：(issued at time)JWT的發行時間，可用於確定JWT的年齡<br>
        值：NumericDate([UNIX時間](https://zh.wikipedia.org/wiki/UNIX%E6%97%B6%E9%97%B4))
    + **jti**(optimal)：(JWT ID)唯一標識符，可用於防止JWT衝突<br>
        值：區分大小寫string
+ **Public Claims**：聲明名稱可以由使用JWT的人員隨意定義。但為防止衝突，任何新的Claim Name應該在IANA "JSON Web Token Claims"註冊，或是抗衝突名稱命名
+ **Private Claims**：JWT使用者可以同意使用聲明名稱，可能會發生衝突，因此應謹慎使用
### Signature
要創建簽名需要指定演算法對encoded header,encoded payload, a secret結合簽章<br>
以HMAC 使用 SHA-256為例：
```JS
HMACSHA256(
base64UrlEncode(header) + "." +
base64UrlEncode(payload),
secret)
```


## 參考來源
1. https://jwt.io/introduction/

3. https://tools.ietf.org/html/rfc7519#section-4.1 
