## Getting Started

Regular Expressions (regex) là một công cụ mạnh mẽ để tìm kiếm và thao tác chuỗi trong C++. Thư viện `<regex>` trong C++ cung cấp các chức năng để làm việc với biểu thức chính quy. Dưới đây là các ví dụ thực tế về cách sử dụng regex trong C++ cho các tác vụ phổ biến.

## Getting Involved

### 1. Kiểm tra Định dạng Email

Để kiểm tra xem một chuỗi có phải là địa chỉ email hợp lệ không, bạn có thể sử dụng regex.

```c++
#include <regex>
bool isValidEmail(const std::string& email) {
    std::regex emailPattern(R"((\w+)(\.\w+)*@(\w+)(\.\w+)+)");
    return std::regex_match(email, emailPattern);
}
int main() {
    std::string email = "example@domain.com";
    if (isValidEmail(email)) {
        std::cout << email << " is a valid email address." << std::endl;
    } else {
        std::cout << email << " is not a valid email address." << std::endl;
    }
    return 0;
}
```

**Giải thích:**

- **R"((\w+)(\.\w+)*@(\w+)(\.\w+)+)"**: là biểu thức chính quy kiểm tra định dạng email.

- **\w+** đại diện cho một hoặc nhiều ký tự từ a-z, A-Z, 0-9 hoặc dấu gạch dưới _.

- ***(\.\w+)**** cho phép các ký tự “.” tiếp theo với từ.

- **@** là ký tự đặc biệt bắt buộc.

- **(\w+)(\.\w+)+** đại diện cho tên miền, với ít nhất một dấu chấm . và phần mở rộng.

### 2. Kiểm tra định dạng số điện thoại (0XX)-XXXXXXX

Định dạng số điện thoại cần kiểm tra là (0XX) YYYYYYYY, trong đó:

- (0XX) là mã vùng, với 0 theo sau là hai chữ số.

- YYYYYYYY là phần số điện thoại, gồm 8 chữ số.

Biểu thức chính quy để kiểm tra định dạng này là **R"(\(0\d{2}\) \d{8})"**.

**Giải thích:**

- **\(0\d{2}\)** kiểm tra mã vùng, với 0 và theo sau là hai chữ số (\d{2}).

- **\d{8}** kiểm tra phần số điện thoại, gồm 8 chữ số.

Dấu cách giữa mã vùng và phần số điện thoại là bắt buộc.

```c++
#include <iostream>
#include <regex>
#include <string>

bool isValidPhoneNumber(const std::string& phoneNumber) {

    const std::string pattern = R"(\(0\d{2}\) \d{8})";

    bool matched = std::regex_match(phoneNumber, std::regex(pattern));

    return matched;
}

int main() {

    std::string phoneNumber1 = "(012) 12345678";  
    std::string phoneNumber2 = "(012) 1234567";   
    std::string phoneNumber3 = "(123) 12345678";  
    std::string phoneNumber4 = "(012) 123456789";

    std::cout << phoneNumber1 << " is valid: " << (isValidPhoneNumber(phoneNumber1) ? "Yes" : "No") << std::endl;
    std::cout << phoneNumber2 << " is valid: " << (isValidPhoneNumber(phoneNumber2) ? "Yes" : "No") << std::endl;
    std::cout << phoneNumber3 << " is valid: " << (isValidPhoneNumber(phoneNumber3) ? "Yes" : "No") << std::endl;
    std::cout << phoneNumber4 << " is valid: " << (isValidPhoneNumber(phoneNumber4) ? "Yes" : "No") << std::endl;
    return 0;
}
```
