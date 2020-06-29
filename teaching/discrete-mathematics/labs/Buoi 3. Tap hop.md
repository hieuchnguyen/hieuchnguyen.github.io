# **Buổi 3. Tập hợp (Set)** 

### Nguyễn Chí Hiếu

https://anonfile.com/03f6h282n9/Buoi_3._Tap_hop_pdf



## **3.1. Thông tin chung**

* Mục tiêu thực hành:
  * Hiểu các khái niệm trong tập hợp.
  * Áp dụng cài đặt được hàm thực hiện các phép toán trên tập hợp.
* Thời gian thực hành: 2 tiết.
* Công cụ thực hành: Visual Studio.

## **3.2. Nội dung lý thuyết**

> Cho 2 tập hợp $A$ và $B$
>
> * $A \subseteq B$ *($A$ là tập hợp con của $B$)*, nếu và chỉ nếu
>   * $\forall x, \left( x \in A \right) \Leftrightarrow \left( x \in B \right)$
>
> * Các phép toán trên tập hợp
>   * $A \cup B = \{ x | x \in A \vee x \in B \}$
>   * $A \cap B = \{ x | x \in A \wedge x \in B \}$
>   * $A \smallsetminus B = \{  x | x \in A \wedge x \notin B \}$

## **3.3. Nội dung thực hành**

### 3.3.1. Kiểm tra tập hợp con

* Ví dụ 1. Cho 2 tập hợp $A = \{ 1, 2 \}, B = \{ 1, 2, \cdots, 10 \}$. Cài đặt hàm kiểm tra $A \subseteq B$?

    ```c#
    bool NotIn(int x, int[] a)
    {
        for (int i = 0; i < a.Length; i++)
            if (x == a[i])
                return false;
        return true;
    }

    bool IsSubSet(int[] a, int[] b)
    {
        for (int i = 0; i < a.Length; i++)
            if (NotIn(a[i], b))
                return false;
        return true;
    }
    ```

### 3.3.2. Tập hợp bằng nhau

* Ví dụ 2. Cho 2 tập hợp $A = \{ 1, 2, \cdots, 10 \}, B = \{ 1, 2, \cdots, 10 \}$. Cài đặt hàm kiểm tra $A = B$?

  ```c#
  bool IsEqual(int[] a, int[] b)
  {
      return IsSubSet(a, b) && IsSubSet(b, a);
  }
  ```

### 3.3.3. Các phép toán trên tập hợp

* Ví dụ 3. Cho 2 tập hợp $A = \{ 1, 3, 5, 7, 9 \}, B = \{ 2, 4, 6, 8, 10 \}$. Viết hàm thực hiện các phép toán sau đây:
  * $A \cup B$
  * $A \cap B$
  * $A \smallsetminus B$

  ````c#
  int[] Union(int[] a, int[] b)
  {
      int[] c;
      int i, j;
      c = new int[a.Length + b.Length];
      for (i = 0; i < a.Length; i++)
      	c[i] = a[i];
      for (j = 0; j < b.Length; j++)
      	if (NotIn(b[j], a))
          {
              c[i++] = b[j];
              //c[i + 1] = b[j]; // 1 3 5 7 0 12
  		}
      return c;
  }
  ````

  ```c#
  int[] Intersection(int[] a, int[] b)
  {
      int[] c;
      int i, j, k;    
      k = 0;
      c = new int[Math.Max(a.Length, b.Length)];
      for (i = 0; i < a.Length; i++)
      	for (j = 0; j < b.Length; j++)
      		if (a[i] == b[j])
     				 c[k++] = a[i];// c[k+1] = a[i];
      return c;
  }
  ```

  ```c#
  int[] Difference(int[] a, int[] b)
  {
      int[] c;
      int i, j;
      j = 0;
      c = new int[a.Length];
      for (i = 0; i < a.Length; i++)
      	if (NotIn(a[i], b))
      		c[j++] = a[i];
      return c;
  }
  ```

## **3.4. Bài tập thực hành**

Cho 3 tập hợp $A = \{ a, b, c \}, B = \{ b, c, d \}, C = \{  a, b, c, d, e\} $. Cài đặt hàm thực hiện các phép toán sau đây:

1. $A \cup B$
2. $B \cap C$
3. $A \smallsetminus B$
4. $A \cup \left( B \cap C \right)$ 
5. $A \subseteq B$?