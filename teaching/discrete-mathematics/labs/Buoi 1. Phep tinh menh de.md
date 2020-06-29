# **Buổi 1. Phép tính mệnh đề**

### Nguyễn Chí Hiếu



## **1.1. Thông tin chung**

* Mục tiêu thực hành: 
  * Hướng dẫn in bảng chân trị của các phép tính mệnh đề.
  * Áp dụng của các phép toán logic trong lập trình.
* Thời gian thực hành: 5 tiết
* Công cụ thực hành: Visual Studio

## **1.2. Nội dung lý thuyết**

> **Các phép toán logic trong lập trình**
>
> | Tên phép toán | Ký hiệu|  C#  |
> | ------------- | :--: | :--: |
> | Phép phủ định (negation) | $\neg$ |!|
> | Phép nối liền (conjunction) | $\wedge$ |&&|
> | Phép nối rời (disjunction) | $\vee$ |\|\||

## **1.3. Nội dung thực hành**

### 1.3. 1. In bảng chân trị của các phép tính mệnh đề

>  **Phép phủ định**

| p    | $\neg$p |
| ---- | ------- |
| 0    | 1       |
| 1    | 0       |

* Ví dụ 1. Cho mệnh đề p, in bảng chân trị của phép phủ định $\neg$p.

    ``` c#
    bool Negation(bool p)
    {
        return !p;
    }
    
    void TruthTableNegation()
    {
        bool p = false;
        do
        {
            Console.WriteLine("{0}\t{1}", p, Negation(p));
            p = !p;
        } while (p);
    }
    ```

>  **Phép nối liền/hội**

| p    | q    | p$\wedge$q |
| ---- | ---- | ---------- |
| 0    | 0    | 0          |
| 0    | 1    | 0          |
| 1    | 0    | 0          |
| 1    | 1    | 1          |

* Ví dụ 2. Cho mệnh đề p và q, in bảng chân trị của p $\wedge$ q .
    ``` c#
    bool Conjunction(bool p, bool q)
    {
        return p && q;
    }
    
    void TruthTableConjunction()
    {
        bool p, q;
        p = q = false;
        do
        {
            do
            {
                Console.WriteLine("{0}\t{1}\t{2}", p, q, Conjunction(p, q));
                q = !q;
            } while (q);
            p = !p;
        } while (p);
    }
    ```

>  **Phép nối rời/tuyển**

| p    | q    | p$\vee$q |
| ---- | ---- | -------- |
| 0    | 0    | 0        |
| 0    | 1    | 1        |
| 1    | 0    | 1        |
| 1    | 1    | 1        |


>  **Phép kéo theo**
>
>  * p $\rightarrow$ q $\Leftrightarrow$ $\neg$ p $\vee$ q

| p    | q    | p$\rightarrow$q |
| ---- | ---- | ---- |
| 0    | 0    | 1 |
| 0    | 1    | 1 |
| 1    | 0    | 0 |
| 1    | 1    | 1 |

>  **Phép kéo theo hai chiều**

| p    | q    | p$\leftrightarrow$q |
| ---- | ---- | ---- |
| 0    | 0    | 1 |
| 0    | 1    | 0 |
| 1    | 0    | 0 |
| 1    | 1    | 1 |

### 1.3.2. Logic trong lập trình 

> **Thứ tự thực hiện các phép toán logic**
>
> 1. !
> 2. &&
> 3. ||

* Ví dụ 3. Cho biết trả về của các biểu thức sau đây:
  * 1 < 2 || 5 > 10 && 2 == 7
  * 1 < 2 || 5 > 10 && (2 == 7)
  * (1 < 2 || 5 > 10) && 2 == 7
  * (2 > 5) || 3 == (2 + 1) || (5 < 10) || (6 != (5 + 1)) || (7 <= 6)


> **Phủ định của phủ định**
>
> $\neg \neg p \Leftrightarrow p$

* Ví dụ 4. Biên dịch và chạy đoạn chương trình sau đây:

    ```c#
    bool Negation2(bool p)
    {
        return !!p;
    }
    // main
    if (Negation2(p) == p)
        Console.WriteLine("!!p == p");
    else
        Console.WriteLine("!!p != p");
    ```

> **DeMorgan**
>
> 1. $\neg (p \wedge q) \Leftrightarrow (\neg p) \vee (\neg q)$
>
>    !(p && q) $\Leftrightarrow$ (!p) || (!q)
>
> 2. $\neg (p \vee q) \Leftrightarrow (\neg p) \wedge (\neg q)$
>
>    !(p || q) $\Leftrightarrow$ (!p) && (!q )

* Ví dụ 5. Cho mảng a gồm các số nguyên: 1, 3, 2, 7, 4, -79, 8, 10, 48, 33, 101, 68. Tính tổng các số thỏa 1 trong 2 điều kiện sau:
  * a[i] là số lẻ
  * a[i] là số chẵn thỏa các điều kiện sau:
    * 0 < a[i] < 100
    * a[i]  $\not \vdots$ 6
    * a[i]  $\not \vdots$ 8

  ```c#
  int[] a = { 1, 3, 2, 7, 4, -79, 8, 10, 48, 33, 101, 68 };
  //
  int Sum(int[] a)
  {
      int i, sum;
      i = sum = 0;
      while (i < a.Length)
      {
          if (
              (a[i] % 2 != 0 || a[i] > 0) 
              && (a[i] % 2 != 0 || a[i] < 100) 
              && (a[i] % 2 != 0 
                  || (!(a[i] % 6 == 0 || a[i] % 8 == 0))
              )
          )
          {
              sum += a[i];
              Console.Write(a[i] + " + ");
          }
          i++;
      }
  
      return sum;
  }
  ```

  * Rút gọn điều kiện if theo các bước sau:

  $\Rightarrow$

  ```c#
  if (
      a[i] % 2 != 0 
      || (
          a[i] > 0 
          && a[i] < 100 
          && !(a[i] % 6 == 0 || a[i] % 8 == 0)
      )
  )
  ```

  $\Rightarrow$

  ```c#
  if (
      a[i] % 2 != 0 
      || (
          a[i] > 0 
          && a[i] < 100 
          && a[i] % 6 != 0 
          && a[i] % 8 != 0
      )
  )
  ```


## **1.4. Bài tập thực hành**

1. Cài đặt lần lượt 3 hàm sau đây và nhận xét:

    ```c#
    bool notBothZero(int x, int y)
    {
        return !(x == 0 && y == 0);
    }
    ```

    ```c#
    bool func1(int x, int y)
    {
        return x != 0 && y != 0;
    }
    ```
    ```c#
    bool func2(int x, int y)
    {
        return x!= 0 || y != 0;
    }
    ```

* Hàm func1 có tương đương với notBothZero()?
* Hàm func2 có tương đương với notBothZero()?
* Hàm func1 có tương đương với func2?

2. Rút gọn biểu thức điều kiện

    ```c#
    if (!(x != 0 && y / x < 1) || x == 0)
    {
        // Do a few things.
    }
    ```

3. Rút gọn biểu thức điều kiện
    ```c# 
    if ((!x.size() <= 0 && x.get(0) != 11) || x.size() > 0)
    {
        if (!(x.get(0) == 11 && (x.size() > 13 || x.size() < 13)) 
            && (x.size() > 0 || x.size() == 13))
        {
            // Do a few things.
        }
    }
    ```
