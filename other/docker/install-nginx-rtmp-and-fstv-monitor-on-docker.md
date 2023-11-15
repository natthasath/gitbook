# 🐳 Install Nginx-RTMP and FSTV-Monitor on Docker

{% hint style="info" %}
หลายคนคงเคยใช้งาน Streaming ผ่านทาง Facebook และ Youtube กันมาบ้าง ซึ่งเราสามารถทำการ Restream เพื่อใช้ในการถ่ายทอดสัญญาณพร้อมกันได้ ซึ่งเราจะใช้ Nginx-RTMP รันบน Docker ในการทำ Restream ร่วมกับ FSTV-Monitor ในการ Monitor แบบ Real-Time
{% endhint %}

## **Requirement**

* [OBS Studio](https://obsproject.com/)
* [VLC](https://get.videolan.org/vlc/3.0.6/win32/vlc-3.0.6-win32.exe)

## **Install**

* ดาวน์โหลด Docker Image

{% code title="#" %}
```
docker pull tiangolo/nginx-rtmp
```
{% endcode %}

* ทำการรัน Nginx-RTMP Container

{% code title="#" %}
```
docker run -d -p 1935:1935 -p 8080:80 --name nginx-rtmp tiangolo/nginx-rtmp
```
{% endcode %}

* ทำการดาวน์โหลด FSTV-Monitor จาก GitHub

{% code title="#" %}
```
git clone https://github.com/3m1o/nginx-rtmp-monitoring.git
```
{% endcode %}

{% code title="#" %}
```
cd nginx-rtmp-monitoring/
```
{% endcode %}

* ทำการแก้ไขไฟล์ config.json

{% code title="config.json" %}
```
{
  "site_title":"RTMP Monitoring",
  "http_server_port":9991,
  "rtmp_server_refresh":3000,
  "rtmp_server_timeout":15000,
  "rtmp_server_url":"http://ip_address:8080/stat.xml",
  "rtmp_server_stream_url":"rtmp://ip_address/stream/",
  "rtmp_server_control_url":"http://ip_address:8080/control",
  "session_secret_key":"stream_key",
  "username":"username",
  "password":"password",
  "language":"en",
  "template":"default",
  "login_template":"login",
  "version":"1.0.2"
}
```
{% endcode %}

* ทำการรัน Docker Compose

{% code title="#" %}
```
docker-compose up -d
```
{% endcode %}

* ทำการเปิดโปรแกรม OBS แล้วคลิก Add Source -> Video Capture Device

![OBS-01](../../.gitbook/assets/obs-01.png)

* เลือก Create new แล้วคลิก OK

![OBS-02](../../.gitbook/assets/obs-02.png)

* เลือก Device แล้วคลิก OK

![OBS-03](../../.gitbook/assets/obs-03.png)

* คลิก Settings

![OBS-04](../../.gitbook/assets/obs-04.png)

* คลิก Stream

![OBS-05](../../.gitbook/assets/obs-05.png)

* ทำการกรอก Server RTMP และ Stream Key แล้วคลิก OK

![OBS-06](../../.gitbook/assets/obs-06.png)

* คลิก Start Streaming

![OBS-07](../../.gitbook/assets/obs-07.png)

* ทำการเปิดโปรแกรม VLC แล้วคลิก Media -> Stream

![VLC-01](../../.gitbook/assets/vlc-01.png)

* คลิก Network

![VLC-02](../../.gitbook/assets/vlc-02.png)

* ทำการกรอก Network URL แล้วคลิก Stream

![VLC-03](../../.gitbook/assets/vlc-03.png)

* คลิก Next

![VLC-04](../../.gitbook/assets/vlc-04.png)

* คลิก Next

![VLC-05](../../.gitbook/assets/vlc-05.png)

* คลิก Next

![VLC-06](../../.gitbook/assets/vlc-06.png)

* คลิก Stream

![VLC-07](../../.gitbook/assets/vlc-07.png)

* จะแสดง Video Streaming

![VLC-08](../../.gitbook/assets/vlc-08.png)

* ลองเข้าไปที่ [http://localhost:9991](http://localhost:9991/) แล้วกรอก Username และ Password ด้วย admin : password

![RTMP-01](../../.gitbook/assets/rtmp-01.png)

* หลังจาก Login เข้ามาจะเห็นหน้าตาแบบนี้

![RTMP-02](../../.gitbook/assets/rtmp-02.png)

**อ่านเพิ่มเติม** : [https://dockr.ly/39A5uet](https://dockr.ly/39A5uet)
