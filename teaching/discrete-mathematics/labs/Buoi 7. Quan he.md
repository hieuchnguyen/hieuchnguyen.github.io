# **Buổi 7. Quan hệ**

### Nguyễn Chí Hiếu



## **7.1. Thông tin chung**

* Mục tiêu thực hành:
  * Hiểu khái niệm về quan hệ và các tính chất của một quan hệ.
  * Áp dụng cài đặt được các hàm tìm quan hệ và xác định các tính chất của một quan hệ.
* Thời gian thực hành: 5 tiết.
* Công cụ thực hành: Visual Studio.

## **7.2. Nội dung lý thuyết**

### 7.2.1. Khái niệm quan hệ

>* Một quan hệ giữa tập hợp $A$ và tập hợp $B$ là một tập hợp con $\mathcal{R}$ của $A \times B$. Nếu $\left( a, b \right) \in \mathcal{R}$.
>* Một quan hệ giữa $A$ và $A$ được gọi là là quan hệ trên $A$.

### 7.2.2. Các tính chất của quan hệ

> Cho $\mathcal{R}$ là một quan hệ trên tập hợp $A$
>
> * Tính phản xạ
> * Tính đối xứng
> * Tính phản xứng
> * Tính bắc cầu

### 7.2.3. Quan hệ tương đương, quan hệ thứ tự

>Cho $\mathcal{R}$ là một quan hệ trên tập hợp $A$
>
>* Một quan hệ $\mathcal{R}$ trên tập hợp $A$ được gọi là là quan hệ tương đương nếu nó phản xạ, đối xứng, bắc cầu.
>* Một quan hệ $\mathcal{R}$ trên tập hợp $A$ được gọi là là quan hệ tương đương nếu nó phản xạ, phản xứng, bắc cầu.

## **7.3. Nội dung thực hành**

### 7.3.1. Tìm quan hệ giữa 2 tập hợp

* Ví dụ 1. Cho 2 tập hợp $A = \{ 2, 7 \}, B = \{ 3, 5, 6, 9 \}$ và $\mathcal{R}$ là một quan hệ gồm những bộ $\left( a, b \right)$ thỏa điều kiện $a < b$.

  * Định nghĩa lớp đối tượng Pair là một bộ trong quan hệ $\mathcal{R}$. Mỗi bộ gồm 2 thành phần first và second.

    ```c#
    class Pair
    {
        private int first;
        private int second;
    
        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    
        public int First { get => first; set => first = value; }
        public int Second { get => second; set => second = value; }
    }
    ```

  * Định nghĩa lớp đối tượng Relation với thuộc tính là danh sách chứa các bộ trong một quan hệ:

    ```c#
    class Relation
    {
        private List<Pair> pairs;
    
        public Relation(int[] a, int[] b)
        {
            this.Pairs = GetPairs(a, b);
        }
    
    	internal List<Pair> Pairs { get => pairs; set => pairs = value; }
        // ...
    }
    ```

  * Tìm quan hệ $\mathcal{R}$ giữa 2 tập hợp $A$ và $B$.

    ```c#
    // A to B
    public List<Pair> GetPairs(int[] a, int[] b)
    {
        List<Pair> pairs = new List<Pair>();
        int i, j;
        for (i = 0; i < a.Length; i++)
            for (j = 0; j < b.Length; j++)
                if (a[i] < b[j])
                    pairs.Add(new Pair(i, j));
        return pairs;
    }
    ```

  * In quan hệ $\mathcal{R}$ giữa 2 tập hợp $A$ và $B$.

    ```c#
    public void PrintPairs(int[] a, int[] b)
    {
        int first, second;
        for (int i = 0; i < Pairs.Count; i++)
        {
            first = a[Pairs[i].First];
            second = b[Pairs[i].Second];
            Console.Write("({0}, {1})", first, second);
        }
    }
    ```

### 7.3.2. Biểu diễn quan hệ bằng ma trận

* Ví dụ 2. Cho tập hợp $A = \{ 2, 3, 5, 7, 11 \}$ và $\mathcal{R}$ là quan hệ "chia hết" trên tập hợp $A$. Biểu diễn quan hệ $\mathcal{R}$ bằng ma trận.

  * Cài đặt lại các hàm khởi tạo, GetPairs và PrintPairs chỉ gồm 1 tham số là tập hợp $A$.

    ```c#
    public List<Pair> GetPairs(int[] a)
    {
        List<Pair> pairs = new List<Pair>();
        int i, j;
        for (i = 0; i < a.Length; i++)
            for (j = 0; j < a.Length; j++)
                if (a[i] % a[j] == 0) //
                    pairs.Add(new Pair(i, j));
        return pairs;
    }
    
    public void PrintPairs(int[] a)
    {
        int first, second;
        for (int i = 0; i < Pairs.Count; i++)
        {
            first = a[Pairs[i].First];
            second = a[Pairs[i].Second];
            Console.Write("({0}, {1})", first, second);
        }
    }
    ```

  * Biểu diễn quan hệ bằng ma trận.

    ```c#
    public int[,] PairsToMatrix(int[] a)
    {
        int[,] m = new int[a.Length, a.Length];
        int i, j;
        for (i = 0; i < a.Length; i++)
            for (j = 0; j < a.Length; j++)
                m[i, j] = 0;
    
        for (i = 0; i < Pairs.Count; i++)
            m[Pairs[i].First, Pairs[i].Second] = 1;
        return m;
    }
    ```

### 7.3.3. Kiểm tra các tính chất của quan hệ

* Ví dụ 3. Cho tập hợp $A = \{ 2, 3, 5, 7, 11 \}$ và $\mathcal{R}$ là quan hệ "chia hết" trên tập hợp $A$. Kiểm tra tính chất phản xạ của quan hệ $\mathcal{R}$.

  ```c#
  public bool IsReflexive(int[] a)
  {
      int[,] m = new int[a.Length, a.Length];
      m = PairsToMatrix(a);
      for (int i = 0; i < a.Length; i++)
          if (m[i, i] == 0)
              return false;
      return true;
  }
  ```

## **7.4. Bài tập thực hành**

1. Kiểm tra tính chất đối xứng, phản xứng của quan hệ $\mathcal{R}$ trong ví dụ 3.
2. Cho 2 tập hợp $A = \{ 0, 1, 2, 3, 4 \}, B = \{ 0, 1, 2, 3 \}$ và $\mathcal{R}$ là một quan hệ gồm những bộ $\left( a, b \right)$ thỏa điều kiện.
   * $a = b$
   * $a | b$