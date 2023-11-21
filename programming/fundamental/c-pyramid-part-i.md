# 🟠 C Pyramid – Part I

{% hint style="info" %}
ย้อนกลับไปสมัยที่ผมทำงานที่แรก ซึ่งเขียน Windows Application ด้วยภาษา C# หัวหน้าได้ให้โจทย์ C Pyramid มาเพื่อฝึกพื้นฐานการเขียนโปรแกรม โดยจะแบ่งเป็น 2 ส่วน ส่วนแรกจะเป็นแบบง่ายที่จะแสดงผลลัพธ์ออกมาด้วย Asterisk ( \* ) ซึ่งจะมี ASCII Code เป็น 42
{% endhint %}

## **1. Half Pyramid Left**

* Result

```
        *
      * *
    * * *
  * * * *
* * * * *
```

* Code

```
main()
{      
     int r,c; 
     for(r=5; r>=1; r--)
     {
          for(c=1; c<r; c++)
          {
               printf(" ");
          }
          for(c=5; c>=r; c--)
          {
               printf("*");
          }
          printf("\n");
     }
     getch();
}
```

## **2. Half Pyramid Right**

* Result

```
*
* *
* * *
* * * *
* * * * *
```

* Code

```
main()
{
    int r, c;
    for (r = 1; r <= 5; r++)
    {
        for (c = 1; c <= r; c++)
        {
            printf("*");
        }
        printf("\n");
    }
    getch();
}
```

## **3. Reverse Half Pyramid Left**

* Result

```
* * * * *
  * * * *
    * * *
      * *
        *
```

* Code

```
main()
{
    int r, c;
    for (r = 1; r <= 5; r++)
    {
        for (c = 1; c < r; c++)
        {
            printf(" ");
        }
        for (c = 5; c >= r; c--)
        {
            printf("*");
        }
        printf("\n");
    }
    getch();
}
```

## **4. Reverse Half Pyramid Right**

* Result

```
* * * * *
* * * *
* * *
* *
*
```

* Code

```
main()
{
    int r, c;
    for (r = 1; r <= 5; r++)
    {
        for (c = 5; c >= r; c--)
        {
            printf("*");
        }
        printf("\n");
    }
    getch();
}
```

## **5. Full Pyramid**

* Result

```
        *
      * * *
    * * * * *
  * * * * * * *
* * * * * * * * *
```

* Code

```
main()
{      
    int r,c,cen=5; 
    for(r=1; r<=5; r++)
    {
        for(c=1; c<=9; c++)
        {   
            if( (c >= (cen - (r - 1))) && (c <= (cen + (r - 1))) )
            {
                printf("*");
            }
            else
            {
                printf(" ");
            }
        }
        printf("\n");
    }
    getch();
}
```

## **6. Reverse Full Pyramid**

* Result

```
* * * * * * * * *
  * * * * * * *
    * * * * *
      * * *
        *
```

* Code

```
main()
{      
    int r,c,cen=5; 
    for(r=5; r>=1; r--)
    {
        for(c=1; c<=9; c++)
        {   
            if( (c >= (cen - (r - 1))) && (c <= (cen + (r - 1))) )
            {
                printf("*");
            }
            else
            {
                printf(" ");
            }
        }
        printf("\n");
    }
    getch();
}
```
