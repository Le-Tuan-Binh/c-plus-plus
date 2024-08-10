## Getting Started

Trong C++, Function Overloading (Nạp chồng hàm) cho phép bạn định nghĩa nhiều hàm có cùng tên nhưng khác biệt về danh sách tham số. 

Điều này có nghĩa là bạn có thể có các hàm có **cùng tên** miễn là **danh sách tham số** của chúng **khác nhau về số lượng, kiểu dữ liệu của tham số hoặc kiểu dữ liệu của hàm**. 

Tuy nhiên bạn cần lưu ý, nếu bạn khai báo hai hàm với cùng tên và danh sách tham số nhưng với kiểu trả về khác nhau, chương trình của bạn sẽ không biên dịch được.

Khi bạn gọi một hàm được nạp chồng, trình biên dịch sẽ xác định phiên bản của hàm cần gọi dựa trên các đối số bạn cung cấp.

Bạn hãy xem đoạn chương trình bên dưới

```c++
#include <iostream>
#include <string>


long long sum(long long a, long long b, long long c) {
    return a + b + c;
}

int sum(int a, long long b) {
    return a + b;
}

int main() {

    /* Sum of three integer */
    long long numberOne = 1;
    long long numberTwo = 2;
    long long numberThree = 3;

    std::cout << "Result: "<< sum(numberOne, numberTwo, numberThree) << std::endl;

    /* Sum of two integer */
    int valueOne = -1;
    long long valueTwo = -2;
    std::cout << "Result: " << sum(valueOne, valueTwo) << std::endl;

    return 0;
}
```