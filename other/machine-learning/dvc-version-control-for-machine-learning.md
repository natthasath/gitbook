# 🧤 DVC Version Control for Machine Learning

{% hint style="info" %}
การใช้งาน Version Control มีมานานแล้วสำหรับเหล่า Programmer และ Developer โดยในสายงานด้าน Data Science ที่ทำเกี่ยวกับ Machine Learning ก็มี Version Control เหมือนกัน เรียกว่า DVC ซึ่งจะคล้าย ๆ กับ Git
{% endhint %}

## **Workflow**

{% hint style="success" %}
โดยปกติการสร้าง Model ของ Machine Learning จะประกอบไปด้วย 3 ส่วน คือ Code, Data และ Configuration นำมา Train เพื่อให้ได้ Model และจะมีการทำ Reproduce
{% endhint %}

![](../../.gitbook/assets/dvc-00.png)

หลักการทำงานของ DVC จะคล้าย ๆ กับ Git แต่จะแบ่่งการเก็บออกเป็น 2 แบบ คือ ส่วนที่เป็น Code จะเก็บอยู่ใน Remote Code Storage ของ Git Server และส่วนที่เป็น Model จะเก็บอยู่ใน Remote Data Storage เช่น S3, GS, Azure, SSH ตามรูปด้านล่าง

![](../../.gitbook/assets/dvc.gif)

## **Download**

* [DVC](https://dvc.org/)

## **Get Started**

* ทำการดาวน์โหลดและติดตั้ง DVC

![](../../.gitbook/assets/dvc-01.png)

* ทำการดาวน์โหลด Code และสร้าง Git Repository

{% code title="C:\dvc>" %}
```
git init
```
{% endcode %}

{% code title="C:\dvc>" %}
```
wget https://dvc.org/s3/examples/so/code.zip
```
{% endcode %}

{% code title="C:\dvc>" %}
```
unzip code.zip && rm -f code.zip
```
{% endcode %}

{% code title="C:\dvc>" %}
```
git add code/
```
{% endcode %}

{% code title="" %}
```
git commit -m "download and initialize code"
```
{% endcode %}

* ทำการสร้าง Virtual Environment

{% code title="C:\dvc>" %}
```
mkvirtualenv venv
```
{% endcode %}

{% code title="C:\dvc>" %}
```
workon venv
```
{% endcode %}

* ทำการติดตั้ง Package จากไฟล์ requirements.txt

{% code title="(venv) C:\nlp>" %}
```
pip install -r code/requirements.txt
```
{% endcode %}

* ทำการสร้าง DVC Repository

{% code title="(venv) C:\nlp>" %}
```
dvc init
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
git commit -m "initialize DVC"
```
{% endcode %}

* ทำการดาวน์โหลด Dataset และทำการ Add ใน DVC ด้วย

{% code title="" %}
```
mkdir data
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
wget -P data https://dvc.org/s3/examples/so/Posts.xml.zip
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
dvc add data/Posts.xml.zip
```
{% endcode %}

* ทำการ Commit การเปลี่ยนแปลงไปยัง Git Repository

{% code title="(venv) C:\nlp>" %}
```
git add data/Posts.xml.zip.dvc data/.gitignore
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
git commit -m "add dataset"
```
{% endcode %}

* ทำการ Run ใน DVC เพื่อรวบรวมคำสั่งในแต่ละ Stage

{% code title="(venv) C:\nlp>" %}
```
dvc run -d data/Posts.xml.zip ^
        -o data/Posts.xml ^
        -f extract.dvc ^
        unzip data/Posts.xml.zip -d data
```
{% endcode %}

* ทำการ Convert ไฟล์จาก XML เป็น TSV ใน DVC เพื่อทำ Feature Extraction ได้ง่ายขึ้น

{% code title="(venv) C:\nlp>" %}
```
dvc run -d code/xml_to_tsv.py -d data/Posts.xml ^
          -o data/Posts.tsv ^
          -f prepare.dvc ^
          python code/xml_to_tsv.py data/Posts.xml data/Posts.tsv
```
{% endcode %}

* ทำการ Split Dataset ใน DVC เพื่อแบ่งข้อมูลที่ใช้ในการ Training และ Test โดยกำหนดให้ Test Dataset มีอัตราส่วนเป็น 0.2 และกำหนดค่า Seed ในการ Random เป็น 20170426

{% code title="(venv) C:\nlp>" %}
```
dvc run -d code/split_train_test.py -d data/Posts.tsv ^
          -o data/Posts-train.tsv -o data/Posts-test.tsv ^
          -f split.dvc ^
          python code/split_train_test.py data/Posts.tsv 0.2 20170426 ^
          data/Posts-train.tsv data/Posts-test.tsv
```
{% endcode %}

* ทำการ Extract Feature and Label ใน DVC ซึ่งจะได้ไฟล์ Pickle

{% code title="(venv) C:\nlp>" %}
```
dvc run -d code/featurization.py -d data/Posts-train.tsv -d data/Posts-test.tsv ^
        -o data/matrix-train.pkl -o data/matrix-test.pkl ^
        -f featurize.dvc ^
        python code/featurization.py data/Posts-train.tsv data/Posts-test.tsv ^
        data/matrix-train.pkl data/matrix-test.pkl
```
{% endcode %}

* ทำการ Train Model กับ Training Dataset ใน DVC

{% code title="(venv) C:\nlp>" %}
```
dvc run -d code/train_model.py -d data/matrix-train.pkl ^
        -o data/model.pkl ^
        -f train.dvc ^
python code/train_model.py data/matrix-train.pkl 20170426 data/model.pkl
```
{% endcode %}

* ทำการ Evaluate Model กับ Test Dataset ใน DVC

{% code title="" %}
```
dvc run -d code/evaluate.py -d data/model.pkl -d data/matrix-test.pkl ^
          -M auc.metric ^
          -f evaluate.dvc ^
python code/evaluate.py data/model.pkl data/matrix-test.pkl auc.metric
```
{% endcode %}

* ทำการตรวจสอบ Accuracy ใน DVC ด้วย Metric

{% code title="(venv) C:\nlp>" %}
```
dvc metrics show
```
{% endcode %}

```
auc.metric: AUC: 0.587951
```

* ทำการ Commit การเปลี่ยนแปลงไปยัง Git Repository

{% code title="(venv) C:\nlp>" %}
```
git add *.dvc auc.metric
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
git commit -am "create pipeline"
```
{% endcode %}

* &#x20;ทำการแก้ไขไฟล์ code/featurization.py ( บรรทัดที่ 72-73 )

{% code title="(venv) C:\nlp>" %}
```
notepad code/featurization.py
```
{% endcode %}

```
bag_of_words = CountVectorizer(stop_words='english',
                               max_features=5000,
                               ngram_range=(1, 2))
```

* &#x20;ทำการ Reproduce สำหรับทุก Stage ซึ่งจะทำแบบ Auto หากมีการแก้ไขไฟล์

{% code title="(venv) C:\nlp>" %}
```
dvc repro evaluate.dvc
```
{% endcode %}

* ทำการตรวจสอบ Accuracy ใน DVC ด้วย Metric ในทุก Branch

{% code title="(venv) C:\nlp>" %}
```
dvc metrics show -a
```
{% endcode %}

* ทำการ Commit การเปลี่ยนแปลงไปยัง Git Repository

{% code title="(venv) C:\nlp>" %}
```
git add evaluate.dvc auc.metric
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
git commit -m "add evaluation step to the pipeline
```
{% endcode %}

* &#x20;ทำการ Tag ในการเก็บ Checkpoint เพื่อใช้ในการ Compare

{% code title="(venv) C:\nlp>" %}
```
git tag -a "baseline-experiment" -m "baseline"
```
{% endcode %}

* ทำการ Show Pipeline แบบ ASCII

{% code title="(venv) C:\nlp>" %}
```
dvc pipeline show --ascii train.dvc
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
dvc pipeline show --ascii train.dvc --commands
```
{% endcode %}

{% code title="(venv) C:\nlp>" %}
```
dvc pipeline show --ascii train.dvc --outs
```
{% endcode %}

* จะแสดง Visualize Pipeline ในแบบ ASCII

![](../../.gitbook/assets/dvc-02.png)

**อ่านเพิ่มเติม** : [https://bit.ly/2FOQM5v](https://bit.ly/2FOQM5v)
