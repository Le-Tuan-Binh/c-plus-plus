## Getting Started

Trong C++ hiện đại, tuple là một container tiện lợi để lưu trữ một nhóm các giá trị khác kiểu. tuple được định nghĩa trong header <tuple> và cho phép bạn tạo các nhóm dữ liệu phức tạp hơn so với pair.

## Getting Involved

### 1. Khai báo Tuple

Có 2 cách khai báo cơ bản nhất cho một tuple trong ngôn ngữ lập trình c++

```c++
std::tuple<data_type, data_type, data_type> tuple_name = std::make_tuple(value, value, value);
```

Với cách thứ nhất này được sử dụng chủ yếu ở các phiên bản ngôn ngữ c++ cũ, với phiên bản c++ mới hơn ta có cách khai báo như sau

```c++
std::tuple<data_type, data_type, data_type, data_type> tuple_name(value, value, value, value);
```

### 2. Truy cập phần tử trong tuple

Để truy cập phần tử trong một tuple nào đó, ta truy cập thông qua **chỉ số** kết hợp với cặp hàm `get` được xây dựng trong thư viện của c++.

Để truy cập phần tử thứ `i` ta truy cập qua chỉ số `i-1`. Ví dụ để truy cập phần tử thứ 1, ta truy cập qua cặp lệnh sau `std::get<i-1>(tuple_name)`

### 3. Structured Bindings (C++17)

**Structured Bindings**, được giới thiệu trong C++17, cho phép bạn khai báo nhiều biến cùng một lúc và gán giá trị cho chúng từ một tuple, pair, hoặc một số kiểu dữ liệu khác có cấu trúc. Điều này giúp mã trở nên rõ ràng và dễ đọc hơn khi làm việc với các cấu trúc dữ liệu phức tạp.

#### 3.1 Khai báo một tuple

```c++
tuple<string, string,string> tuple_name("Le Tuan Binh", "TBin","bin");
```

Khi này để tối ưu việc lấy giá trị của tuple, ta có thể sử dụng `Structured Bindings` để có thể lấy được các giá trị của nó như sau

```c++
auto [value_one, value_two, value_three] = tuple_name;

std::cout << "value_one: " << value_one << ", value_two: " << value_two << ", value_three: " << value_three << std::endl;
```

Kết quả ta nhận được là

```bash
value_one: Le Tuan Binh, value_two: TBin, value_three: bin
```

Hãy xem đoạn chương trình mẫu phía dưới đây

```c++
#include <iostream>
#include <tuple>
#include <string>

int main() {
    std::tuple<int, double, std::string> myTuple(42, 3.14, "Hello");

    auto [myInt, myDouble, myString] = myTuple;

    std::cout << "Integer: " << myInt << std::endl;
    std::cout << "Double: " << myDouble << std::endl;
    std::cout << "String: " << myString << std::endl;

    myInt = 100;
    myDouble = 2.718;
    myString = "World";

    std::cout << "Modified Integer: " << myInt << std::endl;
    std::cout << "Modified Double: " << myDouble << std::endl;
    std::cout << "Modified String: " << myString << std::endl;
    return 0;
}
```

### 3.2 Phép toán so sánh giữa các Tuple

Tuple có thể được so sánh bằng các toán tử so sánh chuẩn (==, !=, <, >, <=, >=) và so sánh theo thứ tự từ điển. Các toán tử này so sánh các phần tử của tuple từ trái sang phải theo thứ tự từ phần tử đầu tiên đến phần tử cuối cùng.


### 4. Ứng dụng trong việc sử dụng Tuple

Chúng ta có thể sử dụng tuple để trả về nhiều giá trị cho một hàm. Việc trả về nhiều giá trị trong một hàm sẽ giúp việc xây dựng hàm của chúng ta trở nên tốt hơn. 

```c++
#include <iostream>
#include <tuple>
#include <string>
using std::cout, std::endl;
using std::string;
using std::tuple, std::make_tuple;

tuple<int, int> transform(int, int);
tuple<string, float> change(int);

tuple<int, int> transform(int a, int b) {
	tuple<int, int> result {a + 1, b + 2};
	return result;
}
tuple<string, float> change(int number) {
	auto result = make_tuple(string("Hello"), number * 1.1);
	return result;
}
```

Hãy xem cách sử dụng đoạn hàm phía trên ở thân chương trình `main` nhé

```c++
int main() {
	tuple<int, int> data = transform(4, 7);
	int a = get<0>(data);
	int b = get<1>(data);
	cout << "a=" << a << ","
		<< "b=" << b << endl;

	string word;
	float percent;
	tie(word, percent) = change(10);
	cout << "word=" << word << ","
		<< "percent=" << percent << endl;

	auto [salute, number] = change(76); 
	cout << "salute=" << salute << ","
		<< "number=" << number << endl;
}
```

Kết quả nhận được là

```bash
a=5,b=9
word=Hello,percent=11
salute=Hello,number=83.6
```

Tuy nhiên điểm mạnh của nó chưa dừng lại ở đó, hãy cùng tôi xem xét một cách thiết kế hàm được đề xuất bên dưới nhé

Một hàm bình thường cần trả về 4 giá trị sau đây:

- Success: bool Thành công hay không thành công

- Data: int (or any type). Nếu thành công thì kết quả là gì

- ErrorCode: int. Mã lỗi của lỗi trên

- Message: string. Cụ thể nếu lỗi đó thì thông báo người dùng thế nào

Hãy cùng tôi xem một bài toán rất thực tế chúng ta hay gặp nhé

```bash
Giả sử bạn có yêu cầu cần lấy giá trị người dùng nhập vào và chuyển sang kiểu số nguyên sau đó thông báo cho người dùng thành công hay thất bại.
```

Với yêu cầu trên chúng ta nghĩ ngay tới việc sử dụng những câu điều kiện cùng với hàm stoi để chuyển một chuỗi bất kì thành một số và thông báo cho người dùng. 

Nhưng hãy thử một đoạn code bên dưới và kiểm tra xem liệu nó có thành công không nhé!!!

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string s = "number one";
    cout << stoi(s);
}
```

Bạn có thể thay chương trình sẽ báo ngay cho một lỗi và liệu người dùng có thể biết được lỗi này là lỗi gì hay không? Và nếu thất bại thì đó có phải là cái họ mong muốn thấy hay không.

Không chỉ thế, việc để quản lý có thể có bao nhiêu lỗi xảy ra cũng khiến ta cảm giác thật khó khăn, vậy làm thế nào?

Có rất nhiều cách có thể áp dụng ở đây như `xử lý ngoại lệ` hoặc kiểm tra bằng cách duyệt qua tất cả các kí tự trong chuỗi... Ở đây việc làm thế nào để kiểm tra không phải là điều tôi muốn truyền tải. Hãy thử xây dựng một đoạn chương trình dùng `tuple` để quản lý các mã lỗi một cách tốt hơn nhé.

**Bước 1: Xác định những lỗi có thể xảy ra**

Ở đây khi chuyển từ một chuỗi về một số ta có thể có các lỗi như sau: Chuỗi rỗng, chuỗi không phải số, hoặc chuỗi không nằm trong miền giá trị ta mong muốn... Ta có thể sử dụng `enum` để quản lý các mã lỗi như sau.

```c++
enum IntegerParseErrorCode {
  EmptyInput,
  InvalidFormat,
  ValueNotInDomain
};
```

**Bước 2: Xây dựng hàm chuyển đổi sử dụng tuple**

Ta sẽ xây dựng một phương thức trả về 4 giá trị lần lượt mà tôi đã đề cập phía trên bằng cách sử dụng tuple.

```c++
tuple<bool, int, int, string>
```

Ở đây tôi chỉ hiển thị việc xây dựng hàm, việc còn lại kiểm tra cho từng yêu cầu bạn cần phải tự triển khai theo mong muốn và ý tưởng của bạn nhé.

```c++
tuple<bool, int, int, string> parse(string buffer) {
	bool success = true;
	int data = 0;
	int errorCode = 0;
	string message = 0;

	/* Kiểm tra chuỗi rỗng */
	if (buffer.length() == 0) {
		success = false;
		errorCode = IntegerParseErrorCode::EmptyInput;
		message = "Input cannot be empty";
	}

	/* Kiểm tra chuỗi chỉ có kí tự số */
	regex integerPattern(R"(^-?\d+$)");
    if (!regex_match(buffer, integerPattern)) {
        success = false;
        errorCode = IntegerParseErrorCode::InvalidFormat;
        message = "Invalid format. Expected an integer.";
    }=
	auto result = make_tuple(success, data, errorCode, message);
	return result;	
}
```

Bạn sẽ đặt ra cho tôi 1 thắc mắc là tại sao phải làm thế này, tại sao phải có enum và tại sao phải dùng 4 giá trị thế kia? Để trả lời câu hỏi này chúng ta hãy cùng xem cách dùng của nó nhé.

```c++
string buffer;getline(cin, buffer);
auto[success, data, errorCode, message] = parse(buffer);
```

Bạn thấy việc kiểm tra ở thân chương chính hoàn toàn gọn và việc hiển thị và tránh bị dừng chương trình đột ngột sẽ hiệu quả tránh việc người dùng phải nhìn những cái họ hoàn toàn không hiểu

```c++
#include <tuple>
#include <string>
#include <regex>
#include <iostream>
using namespace std;
enum IntegerParseErrorCode {
    EmptyInput,
    InvalidFormat,
    ValueNotInDomain
};
tuple<bool, int, int, string> parse(const string& buffer) {
    bool success = true;
    int data = 0;
    int errorCode = 0;
    string message;

    // Kiểm tra nếu chuỗi đầu vào trống
    if (buffer.empty()) {
        success = false;
        errorCode = IntegerParseErrorCode::EmptyInput;
        message = "Input cannot be empty";
        return make_tuple(success, data, errorCode, message);
    }

    // Sử dụng regex để kiểm tra định dạng chuỗi
    regex integerPattern(R"(^-?\d+$)");
    if (!regex_match(buffer, integerPattern)) {
        success = false;
        errorCode = IntegerParseErrorCode::InvalidFormat;
        message = "Invalid format. Expected an integer.";
        return make_tuple(success, data, errorCode, message);
    }
    data = stoi(buffer);
    return make_tuple(success, data, errorCode, message);
}
int main() {
    string testCases[] = { "123", "-45", "", "12a", "300" };
    for (const auto& testCase : testCases) {
        auto [success, data, errorCode, message] = parse(testCase);

        cout << "Input: " << testCase << "\n";

        cout << "Success: " << success << "\n";

        if (success) {
            cout << "Data: " << data << "\n";
        }
        else {
            cout << "ErrorCode: " << errorCode << "\n";
            cout << "Message: " << message << "\n";
        }
        cout << "--------------------\n";
    }
    return 0;
}
```

Với chương trình trên, việc nghiệp vụ mở rộng thêm nhiều tình huống lỗi hơn cũng dễ dàng và việc thay đổi code không ảnh hưởng tới phần chương trình chính của hệ thống.





