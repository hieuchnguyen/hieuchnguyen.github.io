# **Buổi 5. Chia để trị & Quay lui**

### Nguyễn Chí Hiếu



## **5.1. Thông tin chung**

* Mục tiêu thực hành:
  * Giới thiệu thuật toán chia để trị và thuật toán quay lui.
  * Áp dụng thuật toán chia để trị và thuật toán quay lui giải quyết một số bài toán cơ bản.
* Thời gian thực hành: 5 tiết.
* Công cụ thực hành: Visual Studio.

## **5.2. Nội dung lý thuyết**

### 5.2.1. Chia để trị

> Thuật toán chia để trị giải quyết một bài toán theo 3 bước sau:
>
> 1. Chia bài toán thành nhiều bài toán con nhỏ hơn (nhưng vẫn duy trì bản chất của bài toán ban đầu).
>
> 2. Trị/giải quyết theo kiểu đệ quy những bài toán con này.
>
> 3. Tổng hợp lời giải của các bài toán con thành lời giải của bài toán ban đầu.

### 5.2.3. Quay lui

> Thuật toán quay lui sẽ tìm lời giải từng bước. 
>
> * Mỗi bước chọn một trong các lựa chọn bằng cách thử tất cả các khả năng. 
> * Gọi đệ quy để tìm lời giải tiếp theo.

## **5.3. Nội dung thực hành**

### 5.3.1. Chia để trị

* Ví dụ 1. Cài đặt hàm tìm giá trị lớn nhất, nhỏ nhất của dãy số $a$.

    ```c#
    void StraightMaxMin(int[] a, 
                        ref int max, ref int min)
    {
        //max = min = a[0];
        for (int i = 1; i < a.Length; i++)
        {
            max = Math.Max(max, a[i]);
            min = Math.Min(min, a[i]);
        }
    }
    // main
    int max, min;
    max = min = a[0];
    StraightMaxMin(a, ref max, ref min);
    ```

    > Độ phức tạp thuật toán
    >
    > * $T \left( n \right) =  2 \left( n - 1 \right)$

  * Áp dụng thuật toán Chia để trị

    ```c#
    // |left, ..., mid | mid + 1, ..., right|
    void MaxMin(int[] a, int left, int right, 
                  ref int max, ref int min)
    {
        if (left == right) // 1
            max = min = a[left];
        else if (right - left == 1) // 2
        {
            max = Math.Max(a[left], a[right]);
            min = Math.Min(a[left], a[right]);
        }
        else // > 2
        {
            // 1. Divide
            int max1, min1, max2, min2;
            int mid = (left + right) / 2;
            // 2. Solve
            max1 = min1 = a[left];
            MaxMin(a, left, mid, ref max1, ref min1);
            max2 = min2 = a[mid + 1];
            MaxMin(a, mid + 1, right, ref max2, ref min2);
            // 3. Combine
            max = Math.Max(max1, max2);
            min = Math.Min(min1, min2);
        }
    }
    ```

    > Độ phức tạp của thuật toán
    >
    > * $T \left( n \right) =  
    >   \begin{cases}
    >   0, \quad n = 1\\\
    >   2, \quad n = 2\\\
    >   2 T \left( \frac{n}{2} \right) + 2, \quad n > 2
    >   \end{cases}
    >   $

### 5.3.2. Quay lui

* Ví dụ 2. Cài đặt hàm liệt kê tất cả chuỗi nhị phân $n$ bit.

    ```mermaid
    graph TB
    ???[???]
    	??? --> 0??[0??]
    		0?? --> 00?[00?]
    			00? --> 000[000]
    			00? --> 001[001]
    		0?? --> 01?[01?]
    			01? --> 010[010]
    			01? --> 011[011]
        ??? --> 1??[1??]
        	1?? --> 10?[10?]
        		10? --> 100[100]
    			10? --> 101[101]
        	1?? --> 11?[11?]
        		11? --> 110[110]
    			11? --> 111[111]
    ```
    * Khai báo mảng $a$ lưu trữ chuỗi nhị phân $n$ bit.

    ```c#
    void Enumerate(int[] a, int i)
    {
        if (i == a.Length)
        {
            PrintBinary(a);
            return;
        }
    
        a[i] = 0;
        Enumerate(a, i + 1);
        a[i] = 1;
        Enumerate(a, i + 1);
    }
      
    void PrintBinary(int[] a)
    {
        for (int i = 0; i < a.Length; i++)
            Console.Write(a[i] + ", ");
        Console.WriteLine();
    }
    ```


## **5.4. Bài tập thực hành**

1. Cho dãy số có thứ tự  $a = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}$. Dựa vào thuật toán tìm kiếm nhị phân (BinarySearch) xây dựng thuật toán tìm kiếm tam phân (TernarySearch) để tìm một phần tử x trong dãy số.

```c#
int TernarySearch(int[] a, int left, int right, int x)
{
    int mid1, mid2;

    if (left > right)
    	return -1;

    mid1 = (left + right) / 3;
    if (a[mid1] == x)
    	return mid1;
    mid2 = mid1 + (left + right) / 3;
    if (a[mid2] == x)
    	return mid2;

    if (a[mid1] > x)
    	return TernarySearch(a, left, mid1 - 1, x);
    else if (a[mid2] < x)
    	return TernarySearch(a, mid2 + 1, right, x);
    else // a[mid1] < x < a[mid2]
    	return TernarySearch(a, mid1 + 1, mid2 - 1, x);
}
```

2. Bài toán mê cung (Maze) được mô tả như sau:

   > - Mê cung là một ma trận $m \times n$
   >
   >   - \# là tường
   >
   >   - \* là đường đi
   >
   >   - R (Rabbit) :rabbit:
   >
   >   - C (Carrot) :carrot:
   >
   >   ```c#
   >   # # # # # # # # # #
   >   # R # # #   #     # 
   >   # * #   #   #   # #   
   >   # * #             #
   >   # * * *           #
   >   # # # *           #
   >   # * * *   # # # # #
   >   # *         #   # # 
   >   # C #             #
   >   # # # # # # # # # #
   >   ```
   >
   > - Tìm đường đi từ R đến C (right, down, left, up)

   ```c#
   using System;
   class Test2 {
   	public static bool step(char[,] maze, int x, int y) {
   		if (maze[x, y] == 'C')
   			return true;		
   		if (maze[x, y] == '#' || maze[x, y] == '*')
   			return false;
   		
           // Backtracking
   		bool result;
   		maze[x, y] = '*';		
   				
   		// Right
   		result = step(maze, x, y + 1);
   		if (result) return true;
   		// Down
   		result = step(maze, x + 1, y);
   		if (result) return true;		
   		// Left
   		result = step(maze, x, y - 1);
   		if (result) return true;
           // Up
   		result = step(maze, x - 1, y);
   		if (result) return true;
   
   		maze[x, y] = ' ';
   		return false;
   	}
   	
       public static void print(char[,] maze) {
   		for (int x = 0; x < 10; x++) {
   			for (int y = 0; y < 10; y++) {
   				Console.Write(maze[x, y] + " ");
   			}
   			Console.WriteLine();
   		}
       }
   
       static void Main() {
           char[,] maze = {
               {'#', '#', '#', '#', '#', '#', '#', '#', '#', '#'},
               {'#', ' ', '#', ' ', '#', ' ', '#', ' ', ' ', '#'},
               {'#', ' ', '#', ' ', '#', ' ', '#', ' ', '#', '#'},
               {'#', ' ', '#', ' ', ' ', ' ', ' ', ' ', ' ', '#'},
               {'#', ' ', ' ', ' ', '#', ' ', ' ', ' ', ' ', '#'},
               {'#', '#', '#', ' ', ' ', ' ', ' ', ' ', ' ', '#'},
               {'#', ' ', ' ', ' ', ' ', '#', '#', '#', '#', '#'},
               {'#', ' ', ' ', '#', ' ', ' ', '#', ' ', '#', '#'},
               {'#', ' ', '#', ' ', ' ', ' ', ' ', ' ', ' ', '#'},
               {'#', '#', '#', '#', '#', '#', '#', '#', '#', '#'}
           };
           maze[1, 1] = 'R';
           maze[8, 1] = 'C';
           if (step(maze, 1, 1))
               maze[1, 1] = 'R';
           print(maze);
       }
   }
   ```

3. Bài toán xếp hậu (8-Queen) được mô tả như sau:

   > * Bàn cờ Vua kích thước $8 \times 8$.
   > * Một quân hậu trên bàn cờ có thể ăn được các quân khác nằm cùng một dòng, một cột hay một đường chéo.
   > * Tìm cách xếp $n$ quân hậu trên bàn cờ sao cho không quân nào ăn nhau.

4. Bài toán mã đi tuần (Knight tour) được mô tả như sau:

   > * Bàn cờ Vua có kích thước $8 \times 8$
   > * Một quân mã được đặt trên một ô bất kỳ và di chuyển theo luật cờ Vua để đi qua tất cả các ô đúng một lần.
   > * Tìm hành trình di chuyển của quân mã trên bàn cờ.
