# **Buổi 2. Lượng từ**

### Nguyễn Chí Hiếu



## **2.1. Thông tin chung**

* Mục tiêu thực hành:
  * Nhắc lại kiến thức về vị từ, lượng từ.
  * Áp dụng lượng từ phổ dụng và lượng từ tồn tại trong lập trình.
* Thời gian thực hành: 5 tiết.
* Công cụ thực hành: Visual Studio.

## **2.2. Nội dung lý thuyết**

### 2.2.1. Vị từ

> Một vị từ là một khẳng định $p \left( x, y, \dots \right)$ trong đó có chứa một số biến $x, y, \dots$ lấy giá trị trong những tập hợp cho trước $A, B, \dots$ sao cho
>
> * Bản thân $p \left( x, y, \dots \right)$ không phải mệnh đề.
> * Nếu thay $x, y, \dots$ bởi những phần tử cố định nhưng tùy ý $a \in A, b \in B,  \dots$ ta sẽ được một mệnh đề $p \left( a, b,  \dots \right)$, nghĩa là chân trị của nó hoàn toàn xác định.

### 2.2.2. Lượng từ 

> * Mệnh đề $\forall x \in A, p \left( x \right)$ được gọi là lượng từ hóa của vị từ $p \left( x \right)$ bởi lượng từ *"với mọi"* (ký hiệu $\forall$).
>
> * Mệnh đề $\exists x \in A, p \left( x \right)$ được gọi là lượng từ hóa của vị từ $p \left( x \right)$ bởi lượng từ *"tồn tại"* (ký hiệu $\exists$).

## **2.3. Nội dung thực hành**

### 2.3.1. Lượng từ $\forall$ trong lập trình

* Ví dụ 1. Cho $x = \{-10, 0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100\}$ và $p(x)$ = *"$x$ là số chẵn"* là vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\forall x, p(x)$.

    ```c#
    bool p(int x)
    {
        return x % 2 == 0;
    }
    // true: so chan, false: so le
    ```

    ```c#
    bool ForAll(int[] a)
    {
        for (int i = 0; i < a.Length; i++)
            if (!p(a[i]))
                return false;
        return true;
    }
    ```

* Ví dụ 2. Cho $x = \{0, 10, 20, \cdots, 100\}$, $p(x)$ = *"$x$ là số chẵn"* và $q(x)$ = *"$x \geq 0$"* là vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\forall x, p(x) \wedge q(x)$.

    ```c#
    bool q(int x)
    {
        return x >= 0;    
    }
    ```

    ```c#
    bool ForAll2(int[] a)
    {
        for (int i = 0; i < a.Length; i++)
            if (!p(a[i]) || !q(a[i])) // if (!(p(a[i]) && q(a[i])))
                return false;
        return true;
    }
    ```

* Ví dụ 3. Cho A là tập hợp các thú cưng và $p(x)$ = *"Giới tính đực"* là vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\forall x \in A, p(x)$.

    ```c#
    public class Pet // Pet.cs
    {
        public string Name;
        public bool Gender; // true: male, false: female
        public int Age;
        public double Height;
        public double Weight;
    
        public Pet(string name, bool gender, int age, double height, double weight)
        {
            this.Name = name;
            this.Gender = gender;
            this.Age = age;
            this.Height = height;
            this.Weight = weight;
        }
    }
    ```

    ```c#
    Pet[] pets =
    {
        new Pet("Tom", true, 5, 0.75, 10),
        new Pet("Jerry", true, 1, 0.1, 0.2),
        new Pet("Spike", false, 10, 1.2, 35)
    };
    const bool MALE = true;
    bool ForAllMale(Pet[] pets)
    {
        for (int i = 0; i < pets.Length; i++)
            if (pets[i].Gender != MALE)
                return false;
        return true;
    }
    ```

* Thay vòng lặp for bằng foreach

    ```c#
    bool ForAllMale(Pet[] pets)
    {
        foreach (Pet pet in pets)
            if (pet.Gender != MALE)
            	return false;
        return true;
    }
    ```

* Sử dụng câu lệnh LINQ

    ```c#
    bool ForAllMale(Pet[] pets)
    {    
        return pets.All(pet => pet.Gender == MALE);
    }
    ```

### 2.3.2. Lượng từ $\exist$ trong lập trình

* Ví dụ 4. Cho A là tập hợp các thú cưng và $p(x)$ = *"Giới tính đực"* là vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề  $\exists \in A, p(x)$.

    ```c#
    bool ExistsMale(Pet[] pets)
    {
        return pets.Any(pet => pet.Gender == true);
    }
    ```

### 2.3.3. Lượng từ của vị từ $p\left( x, y \right)$ theo 2 biến $x, y$

* Ví dụ 5. Cho  $x = \{1, 2, \cdots, 10\}, y = \{ 1.2, 2.5, 0.5 \}$ và $t \left( x, y \right)$ = *"$x \times y = 1$"* là vị từ theo 2 biến $x, y$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\forall x \exists y, t(x, y)$.

    ```c#
    bool t(int x, double y)
    {
        return x * y == 1;
    }

    bool ForAllExists(int[] a, double[] b)
    {
        for (int i = 0; i < a.Length; i++)
            for (int j = 0; j < b.Length; j++)
                if (t(a[i], b[j]))
                    return true;
        return false;
    }
    ```

## **2.4. Bài tập thực hành**

1. Cho  $x = \{ 1, 2, \cdots, 10 \}$ và $p \left( x \right)$ = *"$x^{2} \geq 100$"* là vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\exists x, p(x )$.
2. Cho  $x = \{ 1, 2, \cdots, 10 \}$ và $p \left( x \right)$ = *"$x$ là số nguyên tố"* là vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\exists x, p(x )$. *(Số nguyên tố là số lớn hơn 1 và chia hết cho chính nó)*
3. Cho  $x = \{ 1, 2,  \cdots, 10 \}$, $p \left( x \right)$ = *"$x^{2} \geq 100$"* và $q \left( x \right)$ = *"$x$ chia hết cho $100$"* là hai vị từ theo biến $x$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\exists x, p(x) \wedge q \left( x \right)$.
4. Cho $x = \{ 1, 2, \cdots, 10 \}$, $y = \{ 2, 4, 6, 8 \}$ và $p \left( x, y \right)$ = *"x = y"* là vị từ theo hai biến $x, y$. Cài đặt hàm xác định chân trị của biểu thức mệnh đề $\forall x \exists y, p \left( x, y \right)$.

