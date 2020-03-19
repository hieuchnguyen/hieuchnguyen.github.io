# Bài 1. Tổng quan lập trình C#

## Giới thiệu

**Chương trình C# đầu tiên**
- Cài đặt Visual Studio Community: https://visualstudio.microsoft.com/free-developer-offers/
- Sử dụng các công cụ online: https://codeinterview.io/,  https://dotnetfiddle.net/

```csharp
using System;
namespace Bai1
{  
  public class Program
  {
    public static void Main()
    {
      // In dòng chữ Hello World
      Console.Write("Hello World");
    }
  }
}
```
**:triangular_flag_on_post: Ý nghĩa:**
- using: thêm thư viện cần thiết
- namespace, class: chưa cần quan tâm
- Main(): mỗi chương trình khi chạy phải có một hàm main duy nhất
- Console.Write(), Console.WriteLine(): in một đoạn văn bản ra màn hình

## Nhập, xuất từ bàn phím
- Console.ReadLine(): đọc chuỗi nhập từ bàn phím, cần phải chuyển về các kiểu dữ liệu thích hợp trước khi sử dụng
- Console.Write(), Console.WriteLine(): in một chuỗi ra màn hình

```csharp
// Đổi tiền từ USD->VND
double vnd, usd;
int ty_gia;
Console.Write("Tien (USD) = ");
usd = Convert.ToDouble(Console.ReadLine());
Console.Write("Nhap ty gia VND va USD = ");
ty_gia = Convert.ToInt32(Console.ReadLine());
vnd = usd * ty_gia;
Console.WriteLine("Tien (VND) = {0}", vnd);
```
