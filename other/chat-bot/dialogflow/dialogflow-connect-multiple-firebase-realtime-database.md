# 🌈 Dialogflow Connect Multiple Firebase Realtime Database

{% hint style="info" %}
หลังจากที่เราได้ลองทำ Chatbot ด้วย Dialogflow ต่อกับ Firebase Realtime Database กันไปแล้ว โดยสามารถต่อแบบ Multiple Database ได้ด้วย ซึ่งเราจะมาลองต่อแบบ Multiple Database กัน
{% endhint %}

## **Get Started**

* ทำการ Import [Firebase Admin SDK](https://firebase.google.com/docs/admin/setup)

```
const admin = require('firebase-admin');
```

* ทำการ Connect Firebase แบบ Single Database

<pre><code>admin.initializeApp({
  credential: admin.credential.applicationDefault(),
<strong>  databaseURL: 'ws://abc-def.firebaseio.com/'
</strong>});

var db = admin.database();
var ref = db.ref("restricted_access/secret_document");
ref.once("value", function(snapshot) {
  console.log(snapshot.val());
});
</code></pre>

* ทำการ Connect Firebase แบบ Multiple Database

<pre><code>const app = admin.initializeApp({
  credential: admin.credential.applicationDefault(),
});

<strong>const db1 = app.database('ws://abc-def.firebaseio.com/');
</strong><strong>const db2 = app.database('ws://abc-def-ghi.firebaseio.com/');
</strong></code></pre>

**อ่านเพิ่มเติม** : [http://bit.ly/3jYO1BA](http://bit.ly/3jYO1BA)
