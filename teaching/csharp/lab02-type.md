# Bài 2. Các kiểu dữ liệu

## Biến
Trong ngôn ngữ lập trình, biến _(variable)_ là một vùng bộ nhớ được cấp phát dùng để lưu trữ giá trị cho một kiểu dữ liệu nào đó. Nó được truy xuất thông qua tên khai báo trước đó. 

Mỗi biến biểu diễn các thông tin cơ bản về:
- Kiểu dữ liệu
- Tên biến (phải tuân thủ quy tắc đặt tên)
- Giá trị
Tên biến:
- Đặt tên có ý nghĩa
- Không đặt trùng với từ khóa và các ký tự đặc biệt
- Phân biệt chữ hoa, chữ thường

## Hằng
Hằng là một biến được khai báo và khởi tạo giá trị chỉ một lần duy nhất và không thể thay đổi giá trị.

## Kiểu dữ liệu
Ngôn ngữ C# cung cấp nhiều kiểu dữ liệu nguyên thủy như: bool, char, int, double, string, ...

## Các vấn đề với kiểu dữ liệu

### Số thực dấu chấm động

Số thực dấu chấm động _(floating point)_ được dùng để biểu diễn xấp xỉ của các số thập phân. Các quy tắc biểu diễn số thực dấu chấm động được mô tả trong tiêu chuẩn quốc tế IEEE 754.

```csharp
double a = 0.15 + 0.15;
double b = 0.1 + 0.2;

Console.WriteLine(a == b); // False
Console.WriteLine(a >= b); // False
Console.WriteLine(a <= b); // True
```
