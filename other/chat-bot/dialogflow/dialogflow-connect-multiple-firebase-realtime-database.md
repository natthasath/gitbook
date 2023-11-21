# ⛱ Dialogflow Connect Multiple Firebase Realtime Database

{% hint style="info" %}
หลังจากที่เราได้ลองทำ Chatbot ด้วย Dialogflow ต่อกับ Firebase Realtime Database กันไปแล้ว โดยสามารถต่อแบบ Multiple Database ได้ด้วย ซึ่งเราจะมาลองต่อแบบ Multiple Database กัน
{% endhint %}

## **Get Started**

* ทำการ Import [Firebase Admin SDK](https://firebase.google.com/docs/admin/setup)

```
const admin = require('firebase-admin');
```

* ทำการ Connect Firebase แบบ Single Database

```
admin.initializeApp({
  credential: admin.credential.applicationDefault(),
  databaseURL: 'ws://abc-def.firebaseio.com/'
});

var db = admin.database();
var ref = db.ref("restricted_access/secret_document");
ref.once("value", function(snapshot) {
  console.log(snapshot.val());
});
```

* ทำการ Connect Firebase แบบ Multiple Database

```
const app = admin.initializeApp({
  credential: admin.credential.applicationDefault(),
});

const db1 = app.database('ws://abc-def.firebaseio.com/');
const db2 = app.database('ws://abc-def-ghi.firebaseio.com/');
```

**อ่านเพิ่มเติม** : [http://bit.ly/3jYO1BA](http://bit.ly/3jYO1BA)
