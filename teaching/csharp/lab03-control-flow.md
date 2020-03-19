# Bài 3. Các cấu trúc điều khiển

## Cấu trúc tuần tự

Lệnh
Khối lệnh
Biểu thức điều kiện

## Cấu trúc rẽ nhánh

Ví dụ:

```csharp
int n = 5;
if (n > 0)
{
  Console.WriteLine("{n} là số nguyên dương", n);
}
```
```csharp
int n = 5;
if (n % 2 == 0)
{
  Console.WriteLine("{0} là số chẵn", n);
}
else
{
  Console.WriteLine("{0} là số lẻ", n);
}
```
```csharp
int n = 10;
if (n < 5)
{
  Console.WriteLine("{0} < 5", n);
}
else if (n > 5)
{
  Console.WriteLine("{0} > 5", n);
}
else
{
  Console.WriteLine("{0} == 5");
}
```
```csharp
int i = 10;
// Kiểm tra 0 <= i <= 0
if (0 <= i)
{
  if (i <= 10)
  {
    Console.WriteLine("0 <= i <= 10");
  }
}
// Rút gọn if
if (0 <= i &&  <= 10)
{
  Console.WriteLine("0 <= i <= 10");
}
```
## Cấu trúc lặp
### Lệnh for


### Lệnh while
