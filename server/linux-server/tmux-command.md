# 👿 TMUX Command

{% hint style="info" %}
หลายคนคงเคยใช้งาน Terminal เพื่อพิมพ์คำสั่ง Command ต่าง ๆ หรืออาจจะเข้าผ่าน SSH เช่น Putty, SecureCRT ซึ่งหากใครต้อง SSH ไปหลาย ๆ เครื่องแล้วพิมพ์คำสั่งเหมือนกันขอแนะนำ Terminal Multiplexer ( TMUX ) ทำให้เราไม่ต้องเสียเวลา SSH ไปพิมพ์ทีละเครื่อง สำหรับคนที่ใช้ Windows 10 สามารถทำการติดตั้งบน Windows Subsystem for Linux ( WSL ) ได้เลย
{% endhint %}

![GifMaker\_20190728123617893.gif](https://codeinsane.files.wordpress.com/2019/07/gifmaker\_20190728123617893.gif?w=1100)

## **Basic TMUX**

* Show Session

{% code title="#" %}
```
tmux list-sessions
```
{% endcode %}

* Create Session

{% code title="#" %}
```
tmux new -s session_name
```
{% endcode %}

* Attach Session

{% code title="#" %}
```
tmux attach -t session_name
```
{% endcode %}

* Kill Session

{% code title="#" %}
```
tmux kill-session -t session_name
```
{% endcode %}

* Kill All Session

{% code title="#" overflow="wrap" %}
```
tmux ls | grep : | cut -d. -f1 | awk '{print substr($1, 0, length($1)-1)}' | xargs kill
```
{% endcode %}

* Show Pane

{% code title="#" %}
```
tmux list-panes
```
{% endcode %}

## **Pane ( Split ) – **_**prefix ( ctrl + b )**_

```
% : vertical split
 " : horizontal split
 o : swap pane
 q : show pane number
 x : kill pane
 + : break pane into window
 - : restore pane from window
 :setw synchronize-panes : sync pane
 :setw synchronize-panes off : stop sync pane
```

## **Windows ( Tab ) – **_**prefix ( ctrl + b )**_

```
 c : create window
 w : list windows
 n : next window
 p : previous window
 f : find window
 , : name window
 & : kill window
```

**อ่านเพิ่มเติม** : [https://bit.ly/2dZzTI3](https://bit.ly/2dZzTI3)
