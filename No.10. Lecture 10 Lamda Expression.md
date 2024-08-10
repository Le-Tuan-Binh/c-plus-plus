## Getting Started

Một biểu thức lambda trong C++ là một cú pháp viết tắt để định nghĩa một đối tượng hàm ẩn danh mà có thể được sử dụng thay thế cho một con trỏ hàm. 

Nó cho phép bạn định nghĩa một hàm ngay lập tức và truyền nó như một tham số cho một hàm khác hoặc sử dụng nó trực tiếp.

## Getting Involved

**Syntax**

```C++
[capture list] (parameter list) -> return type {
    /* *Function body */
}
```

**Định nghĩa**

- **`capture list`**: Danh sách các biến bên ngoài được lambda function sử dụng. Lambda có thể truy cập các biến trong phạm vi (scope) nơi nó được tạo ra. Có thể là dạng by value (`[=]`) hoặc by reference (**`[&]`**).
- **`parameter list`**: Danh sách các tham số của lambda function, tương tự như các tham số của một hàm thông thường.
- **`return type`**: Kiểu dữ liệu của giá trị trả về của lambda function.
- **`function body`**: Phần thân của lambda function, chứa mã lệnh thực hiện các công việc cần thiết.

**Capture List**

Biểu thức lambda có thể mạnh mẽ hơn một hàm thông thường bằng cách có thể truy cập vào các biến từ phạm vi bên ngoài. 
Cú pháp sử dụng cho việc bắt các biến

- `[&]`: bắt tất cả các biến bên ngoài bằng tham chiếu
- `[=]`: bắt tất cả các biến bên ngoài bằng giá trị
- `[a, &b]`: bắt biến a bằng giá trị và biến b bằng tham chiếu

Một lambda với một capture clause rỗng `[]` chỉ có thể truy cập các biến cục bộ của nó.

Bạn có thể tham khảo đoạn code bên dưới để hiểu rõ hơn về lamda expression

```C++
#include <iostream>

int main() {
    /* Lambda function để tính bình phương của một số nguyên */
    auto square = [](int x) -> int {
        return x * x;
    };

    /* Sử dụng lambda function */
    int result = square(5);
    std::cout << "Square of 5 is: " << result << std::endl;

    return 0;
}
```

```Bash
Square of 5 is: 25
```

**Capture By Reference**

```C++
#include <iostream>

int main() {
    int valueOne = 5;
    int valueTwo = 3;

    auto lambda = [&]() {
        std::cout << "Value One = " << valueOne 
				  << ", Value Two = " << valueTwo 
				  << std::endl;
        };

    valueOne = 10;
    valueTwo = 8;

    lambda();

    return 0;
}
```

```Bash
Value One = 10, Value Two = 8
```

**Capture By Value**

```C++
#include <iostream>

int main() {
    int valueOne = 5;
    int valueTwo = 3;

    auto lambda = [=]() {
        std::cout << "Value One = " << valueOne 
		          << ", Value Two = " << valueTwo 
		          << std::endl;
        };

    valueOne = 10;
    valueTwo = 8;

    lambda();

    return 0;
}
```

```Bash
Value One = 5, Value Two = 3
```

**Capture By Mixed**

```C++
#include <iostream>

int main() {
    int valueOne = 5;
    int valueTwo = 3;

    auto lambda = [valueOne, &valueTwo]() {
        std::cout << "Value One = " << valueOne 
				  << ", Value Two = " << valueTwo 
				  << std::endl;
        };

    valueOne = 10;
    valueTwo = 8;

    lambda();

    return 0;
}
```

```bash
Value One = 5, Value Two = 8
```

Tuy nhiên bản chất của lamda expression vẫn có rất nhiều vấn đề cần nhắc đến liệu ưu điểm và nhược điểm nó thế nào?

**Ưu điểm**

1. **Tiện lợi và ngắn gọn:** Lambda expressions cho phép bạn định nghĩa các hàm ngắn gọn ngay tại chỗ mà không cần phải tạo ra một hàm riêng lẻ, làm cho mã nguồn trở nên dễ đọc hơn.
    
2. **Truy cập vào biến từ phạm vi bên ngoài:** Lambda expressions cho phép bạn truy cập vào các biến từ phạm vi bên ngoài, giúp làm cho code trở nên linh hoạt hơn.
    
3. **Sử dụng trong các hàm gọi lại (callbacks) và thuật toán xử lý mảng:** Lambda expressions làm cho việc sử dụng các hàm gọi lại và việc triển khai các thuật toán xử lý mảng trở nên đơn giản hơn.

**Nhược điểm**

1. **Khó hiểu:** Lambda expressions có thể làm cho mã nguồn trở nên khó hiểu nếu sử dụng không cẩn thận, đặc biệt là khi chúng trở nên quá phức tạp.
    
2. **Khó tái sử dụng:** Lambda expressions thường được sử dụng cho các tác vụ cụ thể và không thể tái sử dụng nhiều lần trong mã nguồn.

**Khi nào cần sử dụng lamda expression**

1. **Khi cần một hàm ngắn gọn và chỉ được sử dụng một lần:** Lambda expressions thích hợp cho các tác vụ nhỏ và đơn giản mà chỉ được sử dụng một lần.
    
2. **Khi cần truy cập vào các biến từ phạm vi bên ngoài:** Lambda expressions là lựa chọn tốt khi bạn cần truy cập vào các biến từ phạm vi bên ngoài của hàm lambda.
    
3. **Khi cần sử dụng trong các hàm gọi lại và thuật toán xử lý mảng:** Lambda expressions làm cho việc triển khai các hàm gọi lại và thuật toán xử lý mảng trở nên dễ dàng hơn.