## Getting Started

Vòng lặp while là một cấu trúc điều khiển cho phép bạn thực thi một đoạn mã lặp đi lặp lại miễn là một điều kiện cụ thể là đúng. Điều kiện được kiểm tra ở đầu mỗi lần lặp, vì vậy nếu điều kiện ban đầu là sai, vòng lặp sẽ không được thực hiện lần nào. 

## Getting Involved

Dưới đây là câu lệnh cơ bản của vòng lặp while

```c++
while (condition) {
	// Code block
}
```

Ví dụ: In ra tất cả các số từ 1 đến 5 sử dụng vòng lặp **while**

```c++
#include <iostream>
int main() {
    int i = 1;
    while (i <= 5) {
        std::cout << i << std::endl; 
        ++i; 
    }
    return 0;
}
```

**Giải thích:**
Khởi tạo biến đếm, chúng ta khởi tạo một biến i với giá trị ban đầu là 1.
Điều kiện của vòng lặp: vòng lặp sẽ tiếp tục thực hiện miễn là giá trị của i nhỏ hơn hoặc bằng 5.
Thân vòng lặp trong mỗi lần lặp, giá trị của i được in ra màn hình.
Tăng giá trị của i: sau mỗi lần lặp, giá trị của i được tăng lên 1.