# 🧤 Thai Natural Language Processing with Python

{% hint style="info" %}
หลายคนคงเคยได้ยินการนำ Machine Learning มาใช้ในการทำ Text Analysis, Text Mining และ Text Analytics ซึ่งจะใช้ Natural Language Processing ( NLP ) ในการเรียนรู้ภาษาของมนุษย์ มาใช้กับงานประเภท Speech-to-Text, Text-to-Speech, Speech Recognition, Text Categorization, Text Generation, Machine Translation, Question Answering นอกจากนี้ยังสามารถนำมาใช้ในการวิเคราะห์อารมณ์ Text Sentiment ได้อีกด้วย
{% endhint %}

## **Thai NLP**

<details>

<summary>Corpus ( corpus )</summary>

เป็นฐานข้อมูลภาษาไทยที่มีการแยกเป็นหมวดหมู่ไว้ โดยจะทำการดาวน์โหลด [Corpus](http://www.arts.chula.ac.th/ling/tnc/) ที่พร้อมใช้งานแล้ว ซึ่งเราสามารถทำการเรียกใช้งานพร้อมทั้ง Return ค่าในลักษณะของ frozenset

</details>

<details>

<summary>Soundex ( soundex )</summary>

เป็นวิธีการที่ใช้ในการทำ [Word Similarity Matching](https://www.thinkinfi.com/2018/09/word-similarity-matching-using-soundex.html) สำหรับหาคำที่ออกเสียงคล้ายกันระหว่างคำ 2 คำด้วย Soundex Algorithm จากเสียงพูดของมนุษย์ Phonetic Type 6 แบบ ซึ่งเป็นส่วนหนึ่งของการทำ Text Analysis

</details>

<details>

<summary>Spelling ( spell )</summary>

เป็นวิธีการที่ใช้ในการทำ [Spelling Correction](https://www.thinkinfi.com/2019/09/natural-language-processing-using.html) สำหรับตรวจสอบคำสะกดในภาษาไทย โดยมีความแม่นยำ Accuracy อยู่ที่ 80-90 และมีความเร็วในการประมวลผลอยู่ที่ 10 Word / Second

</details>

<details>

<summary>Summarization ( summarize )</summary>

เป็นวิธีการที่ใช้ในการทำ [Text Summarization](https://stackabuse.com/text-summarization-with-nltk-in-python/) สำหรับนับจำนวนคำ โดยทำการแปลงข้อความที่อยู่ในลักษณะ Paragraph ให้อยูในลักษณะ Sentence แล้วใช้วิธีการตัดคำ Word Tokenization เพื่อทำการหา Frequency ของ Word

</details>

<details>

<summary>Part-of-Speech ( tag )</summary>

เป็นวิธีการที่ใช้ในการทำ [POS Tagging](https://www.thinkinfi.com/2018/10/extract-custom-entity-using-nltk-pos.html) สำหรับกำหนดประเภทของคำใน Sentence ในลักษณะของ Word Class หรือ Lexical Category โดยสามารถนำไปใช้ในการหา Custom Keyword ของ Sentence ซึ่งประกอบไปด้วย Engine ได้แก่ perceptron ( default ), unigram และ artagger

</details>

<details>

<summary>Tokenization ( tokenize )</summary>

เป็นวิธีการที่ใช้ในการทำ [Word Tokenization](https://www.thinkinfi.com/2019/09/natural-language-processing-using.html) สำหรับการตัดคำจาก Sentence ซึ่งประกอบไปด้วย Engine ได้แก่ newmm ( default ), longest, multi\_cut, pyicu, deepcut, tcc และ etcc

</details>

<details>

<summary>Transliteration ( transliterate )</summary>

เป็นวิธีการที่ใช้ในการทำ [Romanization, Transliteration, and Transcription](http://www.royin.go.th/wp-content/uploads/royin-ebook/276/FileUpload/758\_6484.pdf) ถอดเสียงภาษาไทยเป็นตัวอักษรละติน ซึ่งประกอบไปด้วย Engine ได้แก่ royin ( default ) และ thai2rom

</details>

<details>

<summary>ULMFit ( ulmfit )</summary>

เป็นวิธีการที่ใช้ในการทำ [Transfer Learning](https://arxiv.org/abs/1801.06146) สำหรับหาค่าเฉลี่ยของ Vocab ที่ไม่ได้อยู่ใน Pretrained Vocab ด้วยเทคนิค Universal Language Model Fine-tuning for Text Classification ซึ่งจะช่วยลดความผิดพลาดได้ถึง 18-24%

</details>

<details>

<summary>Word Vector ( word_vector )</summary>

เป็นวิธีการที่ใช้ในการทำ [Word Embedding](http://nlp.fast.ai/) แปลงข้อความเป็นตัวเลขในลักษณะของ Vector สำหรับหาคำที่มีความสัมพันธ์คล้ายกันระหว่างคำ 2 คำด้วยการ Multiplication Combination Objective ซึ่งได้มาจากผลคูณด้วยวิธี Omer Levy & Yoav Goldberg ซึ่งจะได้ List of Word ที่แบ่ง Label ออกเป็น Positive และ Negative โดยสามารถนำไปประยุกต์ใช้ในการหาว่าคำใดไม่เข้าพวก

</details>

## **Tokenization Engine**

{% hint style="success" %}
ในการตัดคำภาษาไทย Thai Word Segmentation จะต้องใช้ Dictionary-based ของภาษาไทยในการตัดคำ ซึ่งก็จะประกอบไปด้วย Tokenization Engine ที่ใช้ในการตัดคำ ได้แก่ newmm, longest, multi\_cut, pyicu, deepcut, tcc และ etcc
{% endhint %}

## **Get Started**

* ทำการสร้าง Virtual Environment

{% code title="C:\>" %}
```
mkvirtualenv thai-nlp
```
{% endcode %}

{% code title="C:\>" %}
```
workon thai-nlp
```
{% endcode %}

* ทำการติดตั้ง Package

{% code title="(thai-nlp) C:\>" %}
```
pip install pythainlp[full]
```
{% endcode %}

* ทำการสร้างไฟล์ thai\_nlp.py

{% code title="thai_nlp.py" %}
```
from pythainlp.tokenize import word_tokenize

text = "สถาบันบัณฑิตพัฒนบริศาสตร์"
print(word_tokenize(text, engine="newmm")) #['สถาบันบัณฑิตพัฒนบริหารศาสตร์']
print(word_tokenize(text, engine="icu")) #['สถาบัน', 'บัณฑิต', 'พัฒนบริหารศาสตร์']
```
{% endcode %}

* ทำการรัน thai\_nlp.py

{% code title="" %}
```
python thai_nlp.py
```
{% endcode %}

* จะแสดงผลลัพธ์ของการตัดคำ Word Tokenization

```
['สถาบันบัณฑิตพัฒนบริหารศาสตร์']
['สถาบัน', 'บัณฑิต', 'พัฒนบริหารศาสตร์']
```

**อ่านเพิ่มเติม** : [https://bit.ly/2mQIeou](https://bit.ly/2mQIeou), [https://bit.ly/2nJyP2h](https://bit.ly/2nJyP2h), [https://bit.ly/2pf9UnN](https://bit.ly/2pf9UnN), [https://bit.ly/2mQqr0y](https://bit.ly/2mQqr0y)
