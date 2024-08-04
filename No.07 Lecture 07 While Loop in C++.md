## Getting Started

Vòng lặp while là một cấu trúc điều khiển cho phép bạn thực thi một đoạn mã lặp đi lặp lại miễn là một điều kiện cụ thể là đúng. Điều kiện được kiểm tra ở đầu mỗi lần lặp, vì vậy nếu điều kiện ban đầu là sai, vòng lặp sẽ không được thực hiện lần nào. 

## Getting Involved

### 1. Vòng lặp while cơ bản

Dưới đây là câu lệnh cơ bản của vòng lặp while

```c++
while (condition) {
	// Code block
}
```

![alt text](/images/image-06.png)

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
- Khởi tạo biến đếm, chúng ta khởi tạo một biến i với giá trị ban đầu là 1.
- Điều kiện của vòng lặp: vòng lặp sẽ tiếp tục thực hiện miễn là giá trị của i nhỏ hơn hoặc bằng 5.
- Thân vòng lặp trong mỗi lần lặp, giá trị của i được in ra màn hình.
- Tăng giá trị của i: sau mỗi lần lặp, giá trị của i được tăng lên 1.

### 2. Vòng lặp while với đầu vào của người dùng

Dưới đây là một ví dụ khác sử dụng vòng lặp while để yêu cầu người dùng nhập một số dương. Nếu người dùng nhập số không dương, vòng lặp sẽ yêu cầu nhập lại.

```c++
#include <iostream>
int main() {
    int number;
    std::cout << "Enter a positive number: ";
    std::cin >> number;
    while (number <= 0) {
        std::cout << "The number must be positive. Please try again: ";
        std::cin >> number;
    }
    std::cout << "You entered: " << number << std::endl;
    return 0;
}
```

### 3. Sự chuyển đổi giữa vòng lặp for và while

Với nguyên mẫu của vòng lặp for

```c++
for (initialization; condition; iteration){
	body
}
```

Khi đó ta có thể chuyển sang vòng lặp while như thế này

```c++
{
	initialization;
	while (condition)
	{
		body
		iteration;
	}
}
```

Bạn có thể tham khảo code dưới đây

```c++
#include <iostream>

int main() {
    {
        int count = 0;
        while (count < 5) {
            std::cout << count << std::endl;
            ++count;
        }
        // 'count' có thể được sử dụng ở đây
    }
    // 'count' không thể được sử dụng ở đây
    return 0;
}
```

- **Phạm vi mới:** Việc đặt vòng lặp while trong cặp dấu ngoặc nhọn {} tạo ra một phạm vi mới. Biến count được khai báo bên trong phạm vi này và chỉ tồn tại trong phạm vi đó.

- **Phạm vi của biến:** Sau khi vòng lặp while kết thúc, biến count không còn tồn tại và không thể được sử dụng ngoài phạm vi này.

Sử dụng cặp dấu ngoặc nhọn này là một cách để kiểm soát phạm vi của các biến trong vòng lặp while, tương tự như cách các biến trong vòng lặp for được kiểm soát. Điều này có thể giúp tránh xung đột biến và làm cho mã của bạn dễ đọc hơn.

### 4. Vòng lặp do-while

Vòng lặp do-while tương tự như vòng lặp while ở chỗ nó tiếp tục thực hiện khi điều kiện của vòng lặp còn đúng. Tuy nhiên, điểm khác biệt chính là điều kiện của vòng lặp do-while được kiểm tra sau mỗi lần thực hiện vòng lặp, điều này có nghĩa là đoạn mã trong vòng lặp do-while sẽ luôn được thực hiện ít nhất một lần, bất kể điều kiện ban đầu có đúng hay không.

![alt text](/images/image-07.png)