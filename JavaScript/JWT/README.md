# JSON Web Token (JWT) 2020/05/11

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
>xxxxx.yyyyy.zzzzz

### Header
典型由兩個部分組成：
    + **alg**：對JWT進行簽章的演算法(如HMAC SHA256 or RSA)，對於未加密的JWT值必須設置為none。
    + <span style="color:red;">到底支不支援</span>
    + `<span style="color:red;">到底支不支援</span>`
## 參考來源
1. https://jwt.io/introduction/
