# **Buổi 4. Đệ quy**

### Nguyễn Chí Hiếu



## **4.1. Thông tin chung**

* Mục tiêu thực hành:
  * Giới thiệu khái niệm đệ quy và phân loại đệ quy.
  * Áp dụng đệ quy giải các bài toán đơn giản.
  * Hướng dẫn phương pháp khử đệ quy của một thuật toán.
* Thời gian thực hành: 3 tiết.
* Công cụ thực hành: Visual Studio.

## **4.2. Nội dung lý thuyết**

### 4.2.1. Đệ quy

> Khái niệm đệ quy
>
> * Vấn đề đệ quy là vấn đề được định nghĩa bằng chính nó.
> * Một hàm được gọi là đệ quy, nếu bên trong thân của hàm đó có gọi lại chính nó một cách trực tiếp hay gián tiếp. Hàm đệ quy gồm 2 phần:
>   * Phần cơ sở: điều kiện dừng quá trình gọi đệ quy.
>   * Phần đệ quy: thân hàm chứa lời gọi đệ quy.

### 4.2.2. Khử đệ quy

> * Sử dụng vòng lặp
> * Sử dụng cấu trúc ngăn xếp

## **4.3. Nội dung thực hành**

### 4.3.1. Đệ quy trong lập trình

* Ví dụ 1. Cài đặt hàm đệ quy tính $n!$.

  ```c#
  long Factorial(int n)
  {
      if (n == 0)
          return 1;
      return n * Factorial(n - 1);
  }
  ```

* Ví dụ 2. Cài đặt hàm đệ quy hiển thị đồng hồ đếm ngược.

  ```c#
  void CountDown(int n)
  {            
      if (n == 0)
          return;
      
      Console.Clear();
      Console.WriteLine(n);
      System.Threading.Thread.Sleep(1000); // 1 second
  
      CountDown(n - 1);
  }
  ```

* Ví dụ 3. Cài đặt hàm giải bài toán Tháp Hà Nội.

  ```c#
  // n dia, nguon, dich, tam
  void HaNoiTower(int n, string from, string to, string via)
  {
      if (n == 1)
          Console.WriteLine("Move 1 disk {0} to {1}", from, to);
      else
      {
          HaNoiTower(n - 1, from, via, to);
          HaNoiTower(1, from, to, via);
          HaNoiTower(n - 1, via, to, from);
      }
  }
  
  HaNoiTower(3, "A", "C", "B")
  ```

### 4.3.2. Khử đệ quy

* Ví dụ 4. Khử đệ quy hàm Factorial trong ví dụ 1.

  ```c#
  long Factorial(int n)
  {
      if (n == 0)
          return 1;
      
      long fact = 1;
      for (int i = 2; i <= n; i++)
          fact *= i;
      return fact;
  }
  ```

* Ví dụ 5. Khử đệ quy hàm CountDown trong ví dụ 2.

  ```c#
  void CountDown(int n)
  {
      while (n > 0)
      {
          Console.Clear();
          Console.WriteLine(n);
          System.Threading.Thread.Sleep(1000);
          n--;
      }
  }
  ```

## **4.4. Bài tập thực hành**

1. Cài đặt hàm đệ quy tính tổng của $n$ số nguyên dương.
2. Cài đặt hàm đệ quy đếm số bit của một số nguyên dương $n$.
3. Bài toán nuôi thỏ được mô tả như sau:

   >  * Bắt đầu với một thỏ đực và một thỏ cái vừa mới chào đời.
   >  * Thỏ đạt tới tuổi sinh sản sau một tháng.
   >  * Thời gian mang thai của một con thỏ là một tháng.
   >  * Sau khi tuổi sinh sản, thỏ cái đẻ đều đều mỗi tháng.
   >  * Một thỏ cái sinh ra một thỏ đực và một thỏ cái.
   >  * Không có thỏ chết.

* Hỏi sau một năm sẽ có bao nhiêu cặp thỏ?



