## Getting Started

Trong C++, Function Template là một cách để viết một hàm có thể hoạt động với nhiều kiểu dữ liệu khác nhau mà không cần phải viết lại mã nguồn cho từng kiểu dữ liệu đó. Thay vì viết các hàm riêng lẻ cho mỗi kiểu dữ liệu, bạn có thể sử dụng function template để tạo một mẫu hàm mà sau đó có thể sử dụng với bất kỳ kiểu dữ liệu nào.

## Getting Involved

**Syntax**

```C++
template <class T>
return_type function_name(T arg) {
    /* Function Body */
}
```

**Định nghĩa**

- `template <class T>`: Khai báo một function template với tham số kiểu `T`.
- `T`: Kiểu dữ liệu chung được sử dụng trong Function Template.
- `return_type`: Kiểu dữ liệu của giá trị trả về của hàm.
- `function_name`: Tên của hàm.
- `arg`: Đối số của hàm, có kiểu dữ liệu là `T`.

Bạn hãy tham khảo đoạn code ví dụ bên dưới để hiểu rõ hơn về cách vận hành của **template** trong C++. Tuy nhiên trong bài viết này tôi chỉ đề cập với cách dùng với hàm, trong thực tế việc sử dụng **template** sẽ có nhiều công dụng hay và thú vị hơn rất nhiều.

```C++
#include <iostream>
#include <string>

template <class T>

void permute(T& valueOne, T& valueTwo) {
    T value = valueOne;
    valueOne = valueTwo;
    valueTwo = value;
}

int main() {
    int numberOne = 1;
    int numberTwo = 2;
    std::cout << "Before swap: " << numberOne << " " << numberTwo << std::endl;
    permute(numberOne, numberTwo);
    std::cout << "After swap: " << numberOne << " " << numberTwo << std::endl;
    std::string stringOne = "Le Tuan Binh";
    std::string stringTwo = "Binh Le Tuan";
    std::cout << "Before swap: " << stringOne << " " << stringTwo << std::endl;
    permute(stringOne, stringTwo);
    std::cout << "After swap: " << stringOne << " " << stringTwo << std::endl;
    return 0;
}
```