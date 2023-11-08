# 🔵 ID Token vs Access Token

{% hint style="info" %}
หากพูดถึง Token ที่ใช้กันในปัจจุบัน หลายคนคงเคยใช้ JSON Web Token (JWT) กับ OAuth Token แต่เชื่อว่าคงมีหลายคนที่เคยสงสัยเหมือนกับผมว่า แล้วมันต่างกันยังไง ใช้กับกรณีใดบ้าง ก่อนอื่นต้องมาทำความรู้จักกับประเภทของ Token กันก่อน
{% endhint %}

## Type Token

<details>

<summary>Authentication Token</summary>

เป็น Token ที่ใช้ในการพิสูจน์ตัวตนของผู้ใช้ในระบบ เช่น [JSON Web Token ( JWT )](https://jwt.io/) ที่เป็นไปตามข้อกำหนด OpenID Connect

</details>

<details>

<summary>Access Token</summary>

เป็น Token ที่ใช้สำหรับ Application ที่ต้องการเข้าถึงข้อมูลทรัพยากรต่าง ๆ บน Server เช่น OAuth 2.0

</details>

<details>

<summary><strong>Session Token</strong></summary>

เป็น Token ที่ใช้ในการเก็บข้อมูล Session ของผู้ใช้ที่ Login เข้าสู่ระบบ และทำให้ระบบรู้ว่าผู้ใช้คือใครและต้องการเข้าถึงบริการหรือข้อมูลใด

</details>

<details>

<summary><strong>Communication Token</strong></summary>

เป็น Token ที่ใช้ในการเข้าถึงบริการหรือเครือข่าย เช่น CSRF Token ที่ใช้ในการป้องกันการโจมตีแบบ Cross-Site Request Forgery ( CSRF )

</details>

## **ID Token**

{% hint style="info" %}
ใข้ในการระบุตัวตนของผู้ใช้ในระบบเท่านั้น ซึ่งก็คือ Authentication Token นั่นแหละ โดยหลังจากที่เราทำการกรอก Username และ Password ระบบจะทำการ Authentication แล้วส่ง Token กลับมา เพื่อให้ Client สามารถทำการดึงข้อมูล User Profile
{% endhint %}

{% hint style="danger" %}
ไม่ควรใช้ ID Token เพื่อเข้าถึง API โดยตรง หรือ เข้าถึงทรัพยากรต่าง ๆ บนเครื่อง Server และควรทำตามมาตรฐานความปลอดภัย [Token Best Practices](https://auth0.com/docs/secure/tokens/token-best-practices)&#x20;
{% endhint %}

{% embed url="https://auth0.com/docs/secure/tokens/id-tokens" %}

### JWT Token ( Encode )

{% code overflow="wrap" %}
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
{% endcode %}

### JWT Token ( Decode )

{% code title="HEADER" %}
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```
{% endcode %}

{% code title="PAYLOAD" %}
```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```
{% endcode %}

<pre data-title="VERIFY SIGNATURE"><code>HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  <a data-footnote-ref href="#user-content-fn-1">your-256-bit-secret</a>
)
</code></pre>

## **Access Token**

{% hint style="info" %}
ใช้ในการเข้าถึงข้อมูลทรัพยากรต่าง ๆ บนเครื่อง Server ซึ่งก็คือ Authorization Token นั่นแหละ มักถูกส่งมาพร้อมกับ ID Token เพื่อ Allow Resource เหมาะกับการนำไปใช้กับการเข้าถึงพวก API หรือระหว่าง Service กับ Service คุยกัน
{% endhint %}

{% hint style="danger" %}
ไม่ควรกำหนด Scope ในการเข้าถึงทรัพยากรเกินความจำเป็น และในการ Implement จะต้องดูว่าจะนำไปใช้ในลักษณะใด นอกจากนี้ Access Token ไม่ใช่ Single Sign-On แต่สามารถนำไปประยุกต์ใช้ได้
{% endhint %}

{% code title="Request" %}
```
client_id + client_secret
```
{% endcode %}

{% code title="Response" %}
```json
{
  "access_token":"MTQ0NjJkZmQ5OTM2NDE1ZTZjNGZmZjI3",
  "token_type":"Bearer",
  "expires_in":3600,
  "refresh_token":"IwOGYzYTlmM2YxOTQ5MGE3YmNmMDFkNTVk",
  "scope":"create"
}
```
{% endcode %}

{% embed url="https://www.oauth.com/oauth2-servers/access-tokens/" %}

[^1]: 
