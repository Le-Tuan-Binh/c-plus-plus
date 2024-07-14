## Getting Started

Trong C++, một con trỏ hàm có thể được khai báo để trỏ tới một hàm có kiểu trả về và các tham số cụ thể.

Điều này cho phép bạn lưu trữ địa chỉ của một hàm trong một biến và gọi hàm đó thông qua biến này. Điều này đặc biệt hữu ích trong các tình huống mà hàm cần được chọn trong thời gian chạy, chẳng hạn như khi bạn muốn triển khai các cơ chế callback hoặc các bảng hàm.

## Getting Involved

### 1. Khai báo

Để khai báo một con trỏ hàm, bạn cần chỉ định **kiểu trả về của hàm** và **các kiểu tham số**.

    typedef <Kiểu dữ liệu trả về> (*funcPtr)(<Kiểu dữ liệu của tham số>,...);

Dưới đây là một ví dụ về khai báo một con trỏ hàm trỏ tới một hàm nhận một int và trả về một bool:

```c++
typedef bool (*funcPtr)(int value)
```

Ở đây ta có thể không khái báo từ khóa `typedef` tuy nhiên, việc sử dụng `typedef` trong trường hợp này giúp cho ta dễ sử dụng và quản lý con trỏ hơn.

### 2. Cách sử dụng con trỏ hàm

Đối với ví dụ ở phần 1, ta có thể khai báo các hàm có cùng format mà ta đã khởi tạo cho con trỏ để có thể sử dụng được chúng trong suốt quá trình chương trình thực thi.

Dưới đây là một hàm kiểm tra tính chẵn lẻ của 1 số nguyên với kiểu dữ liệu trả về là `bool` và các tham số là giá trị value ở kiểu `int`

```c++
bool (*funcPtr)(int value)
bool isEven(int number) {
    return number % 2 == 0;
}
funcPtr = isEven;
```

Lúc này ta có thể sử dụng hàm này như cách sử dụng hàm `isEven` bằng cách truyền vào giá trị cần kiểm tra

```c++
bool result = funcPtr(4);
```

Lúc này chương trình gọi đến hàm isEven() để thực hiện. Qua đó ta thấy việc khai báo con trỏ hàm chưa thật sự cần thiết đúng không nào. Vậy hãy đến ví dụ tiếp theo để ta có thể thấy được công dụng thiết thực hơn của `function pointer` nhé.

### 3. Sử dụng con trỏ hàm như 1 tham số trong hàm

Hãy đi qua một ví dụ cho thấy được sự tiện lợi của con trỏ hàm nhé. Nhìn vào bài toán bạn cần viết 1 hàm trả ra 1 vector với rất nhiều điều kiện khác nhau như: `isOdd()`, `isEven()`, `isPalindromic()` và `isPrime()`, thậm chí là rất nhiều hàm để kiểm tra điều kiện có dạng `bool function(int value)`.

Bạn có thể nếu không sử dụng con trỏ hàm, bạn sẽ phải tốn rất nhiều điều kiện `if` thậm chí rất nhiều vòng lặp và rất nhiều hàm đề giải quyết điều này. Hãy xem nếu có sự hổ trợ của con trỏ hàm thì điều này trở nên đơn giản thế nào nhé.

```c++
typedef bool (*Predicate)(int number);
vector<int> filter(const vector<int>& numbers, Predicate predicate) {
    vector<int> result;
    for (int number : numbers) {
        if (predicate(number)) {
            result.push_back(number);
        }
    }
    return result;
}
```

Đoạn mã bên trên, khai báo một hình thức đại diện cho tất cả con trỏ hàm có dạng kiểm tra điều kiện `bool function(int value)` để có thể có cách sử dụng hiệu quả hơn.

Xây dựng hàm filter với 2 tham số

- numbers: Danh sách các số trong vector cần sàng lọc các giá trị.

-predicate: Con trỏ hàm trỏ tới một hàm kiểm tra, điều kiện nào đó của các phần tử trong mảng.

Lúc này ta có thể xây dựng 1 chương trình in ra danh sách các số lẻ, số chẵn, số nguyên tố trong mảng 1 cách rất điệu đà như sau

```c++
typedef bool (*Predicate)(int number);

vector<int> filter(const vector<int>& a, Predicate satisfy) {
    vector<int> result;
    for (int num : a) {
        if (satisfy(num)) {
            result.push_back(num);
        }
    }
    return result;
}
bool isOdd(int number) {
    return number % 2 != 0;
}
bool isEven(int number) {
    return number % 2 == 0;
}
bool isPrime(int number) {
    if (number <= 1) return false;
    if (number == 2 || number == 3) return true;
    if (number % 2 == 0 || number % 3 == 0) return false;
    for (int i = 5; i * i <= number; i += 6) {
        if (number % i == 0 || number % (i + 2) == 0) return false;
    }
    return true;
}
int main() {
    vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    vector<int> oddNumbers = filter(numbers, isOdd);
    vector<int> evenNumbers = filter(numbers, isEven);
    vector<int> primeNumbers = filter(numbers, isPrime);
    cout << "Odd numbers in array: ";
    for (int number : oddNumbers) {
        cout << number << " ";
    }
    cout << endl;
    cout << "Even numbers in array: ";
    for (int number : evenNumbers) {
        cout << number << " ";
    }
    cout << endl;
    cout << "Prime numbers in array: ";
    for (int number : primeNumbers) {
        cout << number << " ";
    }
    cout << endl;
    return 0;
}
```

Bạn đã thấy được sự hữu dụng của `function pointer` chưa? Qua ví dụ trên ta thấy được việc sử dụng khéo léo `function pointer` có thể tối ưu mã nguồn của chúng ta một cách rất hiệu quả.

**Ưu điểm của Sử dụng Con trỏ Hàm**

- Linh hoạt: Cho phép viết mã tổng quát và tái sử dụng nhiều hơn.
- Cơ chế Callback: Hữu ích cho việc triển khai các hàm gọi lại.
- Bảng Hàm: Giúp triển khai các bảng nhảy cho các máy trạng thái hoặc trình thông dịch.
