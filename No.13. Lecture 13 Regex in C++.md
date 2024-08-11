## Getting Started

Regular Expressions (regex) là một công cụ mạnh mẽ để tìm kiếm và thao tác chuỗi trong C++. Thư viện `<regex>` trong C++ cung cấp các chức năng để làm việc với biểu thức chính quy. Dưới đây là các ví dụ thực tế về cách sử dụng regex trong C++ cho các tác vụ phổ biến.

## Getting Involved

### 0. Một số hàm thông dụng trong regex

#### std::regex_match

Kiểm tra xem toàn bộ chuỗi có khớp với biểu thức chính quy không.

```bash
bool regex_match(const std::string& str, const std::regex& pattern);
```

```c++
#include <iostream>
#include <regex>
int main() {
    std::string text = "hello";
    std::regex pattern("hello");
    if (std::regex_match(text, pattern)) {
        std::cout << "Match found!" << std::endl;
    } else {
        std::cout << "No match found." << std::endl;
    }
    return 0;
}
```

#### std::regex_search

Tìm kiếm một phần của chuỗi có khớp với biểu thức chính quy.

```bash
bool regex_search(const std::string& str, std::smatch& match, const std::regex& pattern);
```

```c++
#include <iostream>
#include <regex>
int main() {
    std::string text = "hello world";
    std::regex pattern("world");
    std::smatch match;
    if (std::regex_search(text, match, pattern)) {
        std::cout << "Match found: " << match.str() << std::endl;
    } else {
        std::cout << "No match found." << std::endl;
    }
    return 0;
}
```

#### std::regex_replace

Thay thế các phần của chuỗi khớp với biểu thức chính quy bằng một chuỗi khác.

```bash
std::string regex_replace(const std::string& str, const std::regex& pattern, const std::string& replacement);
```

```c++
#include <iostream>
#include <regex>
int main() {
    std::string text = "hello world";
    std::regex pattern("world");
    std::string replacement = "universe";
    std::string result = std::regex_replace(text, pattern, replacement);
    std::cout << "Result: " << result << std::endl;
    return 0;
}
```

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
### 3. Kiểm tra chuỗi chỉ chứa toàn số

**Giải thích:**

- **R"(\d+)"** là biểu thức chính quy kiểm tra chuỗi chỉ chứa các chữ số.

- **std::regex_match** kiểm tra xem chuỗi text có toàn chữ số không.

```c++
#include <iostream>
#include <regex>
bool isNumeric(const std::string& text) {
    std::string pattern = R"(\d+)";
    bool matched = std::regex_match(text, std::regex(pattern));
    return matched;
}
int main() {
    std::string text1 = "12345";
    std::string text2 = "123a5";

    std::cout << text1 << " is numeric: " << isNumeric(text1) << std::endl;  
    std::cout << text2 << " is numeric: " << isNumeric(text2) << std::endl;  
    return 0;
}
```

### 4. Kiểm tra đường dẫn url

```c++
#include <iostream>
#include <regex>
bool isValidURL(const std::string& url) {
    std::regex urlPattern(R"(https?:\/\/(www\.)?[a-zA-Z0-9\-\.]+\.[a-zA-Z]{2,})");
    return std::regex_match(url, urlPattern);
}
int main() {
    std::string url = "https://www.example.com";
    if (isValidURL(url)) {
        std::cout << url << " is a valid URL." << std::endl;
    } else {
        std::cout << url << " is not a valid URL." << std::endl;
    }
    return 0;
}
```

**Giải thích:**

- **R"(https?:\/\/(www\.)?[a-zA-Z0-9\-\.]+\.[a-zA-Z]{2,})"** là biểu thức chính quy kiểm tra định dạng URL.

- **https?** cho phép http hoặc https.

- **\/\/** là dấu phân cách trong URL.

- **(www\.)?** là phần tùy chọn www.

- **[a-zA-Z0-9\-\.]+\.[a-zA-Z]{2,}** là tên miền với phần mở rộng.

### 5. Tìm tất cả các số trong chuỗi

```c++
#include <iostream>
#include <regex>
#include <string>
#include <vector>
std::vector<std::string> findNumbers(const std::string& text) {
    std::vector<std::string> numbers;
    std::regex numberPattern(R"(\d+)");
    auto numbersBegin = std::sregex_iterator(text.begin(), text.end(), numberPattern);
    auto numbersEnd = std::sregex_iterator();
    for (std::sregex_iterator i = numbersBegin; i != numbersEnd; ++i) {
        std::smatch match = *i;
        numbers.push_back(match.str());
    }
    return numbers;
}
int main() {
    std::string text = "There are 2 apples and 10 oranges.";
    std::vector<std::string> numbers = findNumbers(text);
    std::cout << "Numbers found: ";
    for (const std::string& num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

**Giải thích:**

- **R"(\d+)"** là biểu thức chính quy tìm các số (một hoặc nhiều chữ số liên tiếp).

- **std::sregex_iterator** được sử dụng để lặp qua tất cả các kết quả tìm được.

Các số tìm được được lưu vào vector numbers.