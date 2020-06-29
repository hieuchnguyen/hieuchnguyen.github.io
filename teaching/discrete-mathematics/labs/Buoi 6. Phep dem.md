# **Buổi 6. Phép đếm**

### Nguyễn Chí Hiếu

## **6.1. Thông tin chung**

* Mục tiêu thực hành:
  * Hiểu các khái niệm trong phép đếm: quy tắc nhân, quy tắc cộng; khái niệm hoán vị, chỉnh hợp, tổ hợp.
  * Áp dụng cài đặt được hàm sinh các hoán vị, chỉnh hợp, tổ hợp của một tập hợp.
* Thời gian thực hành: 5 tiết.
* Công cụ thực hành: Visual Studio.

## **6.2. Nội dung lý thuyết**

### 6.2.1. Quy tắc cộng, quy tắc nhân

> * Quy tắc cộng: nếu $T_{1} \left( n \right) = O \left( g_{1} \left( n\right) \right) $ và $T_{2} \left( n \right) = O \left( g_{2} \left( n\right) \right) $ là thời gian thực hiện của 2 đoạn chương trình $P_{1}$ và $P_{2}$ thì thời gian thực hiện của 2 đoạn chương trình đó *nối tiếp nhau* là:
>
>   $T \left( n \right) = O \left( g_{1} \left( n \right) + g_{2} \left( n \right) \right)$.
>
> * Quy tắc nhân: nếu $T_{1} \left( n \right) = O \left( g_{1} \left( n\right) \right) $ và $T_{2} \left( n \right) = O \left( g_{2} \left( n\right) \right) $ là thời gian thực hiện của 2 đoạn chương trình $P_{1}$ và $P_{2}$ thì thời gian thực hiện của 2 đoạn chương trình đó *lồng vào nhau* là:
>
>   $T \left( n \right) = O \left( g_{1} \left( n \right) \cdot g_{2} \left( n \right) \right)$.

### 6.2.2. Hoán vị, chỉnh hợp, tổ hợp

## 6.3. **Nội dung thực hành**

### 6.3.1. Áp dụng quy tắc cộng, quy tắc nhân trong lập trình

* Ví dụ 1. Cho biết giá trị trả về của hàm Function1(). n1= 2, n2=5, n3=10

    ```c#
    int Function1(int n1, int n2, int n3)
    {
        int s = 0;
        for (int i = 1; i <= n1; i++)
            s++;
        for (int j = 1; j <= n2; j++)
            s++;
        for (int k = 1; k <= n3; k++)
            s++;
        return s;
    }
    ```

* Ví dụ 2. Cho biết giá trị trả về của hàm Function2().

    ```c#
    int Function2(int n1, int n2, int n3)
    {
        int s = 0;
        int i, j, k;            
        for (i = 1; i <= n1; i++)           
            for (j = 1; j <= n2; j++)
                for (k = 1; k <= n3; k++)
                    s++;
        return s;
    }
    ```

### 6.3.2. Hoán vị, chỉnh hợp, tổ hợp

* Ví dụ 3. Cho tập hợp $S = \{ 'A', 'B', 'C' \}$. Cài đặt hàm liệt kê tất cả hoán vị của s.

    ```mermaid
    graph TB
    ABC1[ABC] -->|C<->C| ABC2[ABC]
        ABC2 -->|B<->B| ABC3[ABC]	
        ABC2 -->|B<->A| BAC3[BAC]
    ABC1[ABC] -->|C<->B| ACB2[ACB]
        ACB2 -->|B<->B| ACB3[ACB]	
        ACB2 -->|C<->A| CAB3[CAB]
    ABC1[ABC] -->|C<->A| CBA2[CBA]
        CBA2 -->|B<->B| CBA3[CBA]	
        CBA2 -->|B<->C| BCA3[BCA]
    ```

    ```c#
    void Swap(char[] s, int i, int j)
    {
        char tmp = s[i];
        s[i] = s[j];
        s[j] = tmp;
    }
    // bca, cba, cab, acb, bac, abc
    void Permutation(char[] s, int n)
    {
        if (n == 1)
            Console.WriteLine(s);
        else
        {
            for (int i = 0; i < n; i++)
            {
                Swap(s, i, n - 1);
                Permutation(s, n - 1);
                Swap(s, i, n - 1);
            }
        }
    }
    ```

* Ví dụ 4. Cho tập hợp $S = \{ 'A', 'B', 'C' \}$. Cài đặt hàm liệt kê tất cả chỉnh hợp chập 2 của 3 phần tử trong tập hợp $s$.

    ```c#
    // ca, ba, ab, cb, ac, bc
    void kPermutation(char[] s, int k, int n)
    {
        if (k == 0)
        {
            for (int i = n; i < s.Length; i++)
                Console.Write(s[i]);
            Console.WriteLine();
        }
        else
        {
            for (int i = 0; i < n; i++)
            {
                Swap(s, i, n - 1);
                kPermutation(s, k - 1, n - 1);
                Swap(s, i, n - 1);
            }
        }
    }
    ```

## **6.4. Bài tập thực hành**

1. Cài đặt hàm in ra màn hình các hình như sau:

```c++
//1
* * * * * *
* * * * * *
* * * * * *
* * * * * *
* * * * * *
//2
* * * * *
* * * *
* * * 
* * 
*
//3
*
* *
* * *
* * * *
* * * * *
//4
* * * * *
* * * *
* * *
* *
*
//5
*
* *
* * * 
* * * *
* * * * * 
```

3. Cho tập hợp $s = \{ 'a', 'b', 'c' \}$. Cài đặt hàm liệt kê tất cả tổ hợp chập 2 của 3 phần tử trong tập hợp $s$.

4. Cài đặt hàm hiển thị tam giác Pascal (áp dụng nhị thức Newton). Ví dụ, tam giác Pascal có chiều cao $n = 4$.

```c++
1 
1	1
1 	2	1
1 	3	3	1
1	4	6	4	1
```

```c#
int C(int k, int n)
{
    if (k == 0 || k == n)
    	return 1;
    return C(k, n - 1) + C(k - 1, n - 1);
}

void DrawTrianglePascal(int n)
{
    int i, j;   
    for (i = 0; i < n; i++)
    {
        for (j = 0; j <= i; j++)
        	Console.Write("{0}", C(j, i));
        Console.WriteLine();
    }
}
```

