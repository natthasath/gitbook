# 🟤 C Pyramid – Part II

{% hint style="info" %}
หลังจากที่เราได้ทำส่วนแรกไปแล้ว โจทย์ C Pyramid ในส่วนที่สองจะเป็นแบบยากขึ้นมาอีกขั้น โดยจะแสดงผลลัพธ์ออกมาด้วยตัวอักษรมากกว่า 1 ตัว ส่วนใหญ่จะใช้ตัวอักษรภาษาอังกฤษตั้งแต่ A, B, C ไปเรื่อย ๆ ซึ่งจะมี ASCII Code ตั้งแต่ 65 เป็นต้นไป
{% endhint %}

## **1. Character Row Start A**

* Result

```
A B C D E
  A B C D
    A B C
      A B
        A
```

* Code

```
main()
{
    char r, c;
    for (r = 'E'; r >= 'A'; r--)
    {
        for (c = 'E'; c > r; c--)
        {
            printf(" ");
        }
        for (c = 'A'; c <= r; c++)
        {
            printf("%c", c);
        }
        printf("\n");
    }
    getch();
}
```

## **2. Character Row Start A++**

* Result

```
A B C D E
  B C D E
    C D E
      D E
        E
```

* Code

```
main()
{
    // Pattern ASCII not int r,c
    char r, c, i = 0;
    for (r = 'E'; r >= 'A'; r--)
    {
        for (c = 'E'; c > r; c--)
        {
            printf(" ");
        }
        for (c = 'A' + i; c <= r + i; c++)
        {
            printf("%c", c);
        }
        i++;
        printf("\n");
    }
    getch();
}
```

## **3. Pascal**

* Result

```
        1
      1   1
    1   2   1
  1   3   3   1
1   4   6   4   1
```

* Code

```
main()
{
    int r, c, s, v = 1;

    for (r = 0; r < 5; r++)
    {
        for (s = 1; s <= 5 - r; s++)
        {
            printf("  ");
        }
        for (c = 0; c <= r; c++)
        {
            if (c == 0 || r == 0)
            {
                v = 1;
            }
            else
            {
                v = (v * (r - c + 1)) / c;
            }
            printf("%4d", v);
        }
        printf("\n");
    }
    getch();
}
```
