## Getting Started

Trong thực tế lập trình, việc xử lý chuỗi (String) là vô cùng quan trọng bởi vì hầu hết các tương tác với người dùng đều thông qua kiểu dữ liệu chuỗi. Từ việc đọc dữ liệu đầu vào, xử lý văn bản, đến việc phân tích cú pháp các câu lệnh, chuỗi đóng vai trò quan trọng. Vì vậy, nắm vững các kỹ thuật thao tác trên chuỗi là điều cần thiết. Trong bài viết này, chúng ta sẽ đi qua một số kiến thức thường gặp và các kỹ thuật phổ biến để xử lý chuỗi trong C++.

## Getting Involved

### 1. Tách từ trong một chuỗi

Một trong những thao tác cơ bản và thường gặp nhất khi làm việc với chuỗi là tách từ. Việc tách từ trong một chuỗi giúp chúng ta có thể xử lý từng phần của chuỗi một cách độc lập, phục vụ cho nhiều mục đích khác nhau như phân tích dữ liệu, tìm kiếm, hay xử lý ngôn ngữ tự nhiên. Dưới đây là hai phương pháp phổ biến để tách từ trong một chuỗi trong C++.

#### 1.1 Stringstream

Stringstream là một công cụ mạnh mẽ và linh hoạt trong C++ cho phép chúng ta dễ dàng chuyển đổi và xử lý các chuỗi. Khi sử dụng stringstream, chuỗi được truyền vào sẽ được xử lý như một dòng ký tự, và các từ có thể được tách ra dựa trên khoảng trắng hoặc một ký tự đặc biệt nào đó.

Bạn hãy tham khảo đoạn chương trình mẫu bên dưới

```c++
vector<string> split(string str, char delimiter) {
    vector<string> tokens;
    string token;
    stringstream ss(str);
    while (getline(ss, token, delimiter)) {
        if (!token.empty()) {
            tokens.push_back(token);
        }
    }
    return tokens;
}
int main() {
    string str = "This is a sample string";
    vector<string> words = split(str, ' ');
    for (const auto& word : words) {
        cout << word << endl;
    }
    
    return 0;
}
```

**Giải thích:**

- **stringstream ss(str);** chuyển chuỗi đầu vào str thành một dòng ký tự có thể đọc từng phần dựa trên ký tự phân tách (ở đây là khoảng trắng ' ').

- **Hàm getline(ss, token, delimiter)** đọc từng phần của chuỗi ss cho đến khi gặp ký tự phân tách, và lưu kết quả vào biến token. Nếu token không rỗng, nó sẽ được thêm vào vector tokens.

Kỹ thuật này rất hiệu quả cho việc tách các từ trong chuỗi với các ký tự phân tách đơn giản như khoảng trắng, dấu phẩy, hoặc bất kỳ ký tự đơn nào.

#### 1.2 Sử dụng `.find()` và `.substr()`

Một cách tiếp cận khác để tách từ trong chuỗi là sử dụng kết hợp hai hàm find() và substr(). Cách này cho phép bạn tách từ dựa trên chuỗi con (substring) cụ thể, linh hoạt hơn trong những trường hợp chuỗi phân tách phức tạp.

```c++
vector<string> split(string haystack, string needle) {
    vector<string> result;
    int startPos = 0;
    size_t foundPos = haystack.find(needle, startPos);
    while (foundPos != string::npos) {
        int count = foundPos - startPos;
        string token = haystack.substr(startPos, count);
        if (!token.empty()) {
            result.push_back(token);
        }
        startPos = foundPos + needle.length();
        foundPos = haystack.find(needle, startPos);
    }
    string token = haystack.substr(startPos, haystack.length() - startPos);
    if (!token.empty()) {
        result.push_back(token);
    }
    
    return result;
}
int main() {
    string str = "apple#banana#cherry#date";
    vector<string> words = split(str, "#");
    for (const auto& word : words) {
        cout << word << endl;
    }
    return 0;
}
```

**Giải thích:**

- **Tìm kiếm vị trí phân tách:** Hàm find() tìm kiếm vị trí xuất hiện đầu tiên của chuỗi phân tách needle trong chuỗi chính haystack bắt đầu từ vị trí startPos.

- **Tách chuỗi con:** Hàm substr() tạo một chuỗi con từ vị trí startPos đến vị trí ngay trước foundPos (vị trí tìm thấy chuỗi phân tách).

- **Cập nhật vị trí bắt đầu:** Sau khi tách một từ, startPos được cập nhật để bắt đầu tìm kiếm từ vị trí ngay sau chuỗi phân tách vừa tìm thấy.

- **Xử lý phần còn lại:** Cuối cùng, nếu còn phần chuỗi nào sau chuỗi phân tách cuối cùng, nó sẽ được thêm vào kết quả.

Phương pháp này linh hoạt hơn vì nó cho phép bạn tách chuỗi dựa trên các chuỗi phân tách phức tạp hơn là chỉ các ký tự đơn lẻ.

### 2. String conversion

Chuyển đổi giữa các kiểu dữ liệu khác nhau và chuỗi là một trong những thao tác phổ biến trong lập trình. Điều này bao gồm việc chuyển một giá trị số thành chuỗi để hiển thị hoặc lưu trữ, cũng như chuyển đổi một chuỗi thành số hoặc các kiểu dữ liệu khác để thực hiện các phép toán. Trong phần này, chúng ta sẽ xem xét một số phương pháp phổ biến để chuyển đổi giữa chuỗi và các kiểu dữ liệu khác trong C++.

#### 2.1. Chuyển đổi số thành chuỗi

Việc chuyển đổi số thành chuỗi thường được thực hiện khi cần hiển thị giá trị số dưới dạng văn bản, hoặc khi cần nối một số với các chuỗi khác.

##### 2.1.1. Sử dụng std::to_string

C++11 giới thiệu hàm std::to_string, cho phép bạn dễ dàng chuyển đổi các kiểu số (int, float, double, long, v.v.) thành chuỗi.

```c++
#include <iostream>
using namespace std;
int main() {
    int num = 42;
    double pi = 3.14159;
    string strNum = to_string(num);
    string strPi = to_string(pi);
    cout << "Number: " << strNum << endl;
    cout << "Pi: " << strPi << endl;
    return 0;
}
```

##### 2.1.2. Sử dụng std::stringstream

Một cách khác để chuyển đổi số thành chuỗi là sử dụng std::stringstream. Phương pháp này có thể sử dụng với tất cả các kiểu dữ liệu hỗ trợ toán tử xuất (<<).

```c++
#include <iostream>
#include <sstream>
using namespace std;
int main() {
    int num = 42;
    double pi = 3.14159;
    stringstream ss;
    ss << num;
    string strNum = ss.str();
    ss.str("");  
    ss.clear();
    ss << pi;
    string strPi = ss.str();
    cout << "Number: " << strNum << endl;
    cout << "Pi: " << strPi << endl;
    return 0;
}
```

**Giải thích:**

- **stringstream ss;** khởi tạo một đối tượng stringstream.

- s**s << num;** ghi giá trị số num vào đối tượng stringstream.

- **ss.str();** trả về chuỗi hiện tại được lưu trữ trong stringstream.

#### 2.2 Chuyển đổi chuỗi thành số

Khi xử lý dữ liệu đầu vào hoặc làm việc với các giá trị văn bản, thường có nhu cầu chuyển đổi các chuỗi thành số để thực hiện các phép toán hoặc kiểm tra logic.

##### 2.2.1. Sử dụng std::stoi, std::stol, std::stof, std::stod

C++11 cũng giới thiệu một số hàm chuyển đổi chuỗi thành số, như std::stoi (string to integer), std::stol (string to long), std::stof (string to float), và std::stod (string to double). 

```c++
#include <iostream>
using namespace std;

int main() {
    string strNum = "42";
    string strPi = "3.14159";
    
    int num = stoi(strNum);
    double pi = stod(strPi);
    
    cout << "Number: " << num << endl;
    cout << "Pi: " << pi << endl;
    
    return 0;
}
```

##### 2.2.2. Sử dụng stringstream

Giống như chuyển đổi số thành chuỗi, bạn cũng có thể sử dụng std::stringstream để chuyển đổi chuỗi thành số.

```c++
#include <iostream>
#include <sstream>
using namespace std;

int main() {
    string strNum = "42";
    string strPi = "3.14159";
    
    stringstream ss;
    ss << strNum;
    int num;
    ss >> num;
    
    ss.str("");
    ss.clear();

    ss << strPi;
    double pi;
    ss >> pi;
    
    cout << "Number: " << num << endl;
    cout << "Pi: " << pi << endl;
    
    return 0;
}
```

**Giải thích:**

- **stringstream ss(strNum);** khởi tạo một đối tượng stringstream từ chuỗi strNum.

- **ss >> num;** chuyển chuỗi strNum thành số và gán cho num.

### 3. String concatenation

Nối chuỗi là một trong những thao tác cơ bản và thường xuyên được sử dụng khi làm việc với chuỗi trong lập trình. Nó cho phép bạn kết hợp hai hoặc nhiều chuỗi lại với nhau để tạo thành một chuỗi mới. Trong C++, có nhiều cách khác nhau để thực hiện việc nối chuỗi, từ các toán tử đơn giản cho đến các phương pháp tối ưu hóa hiệu suất.

#### 3.1. Sử dụng toán tử +

Cách đơn giản và phổ biến nhất để nối hai chuỗi trong C++ là sử dụng toán tử +. Toán tử này tạo ra một chuỗi mới bằng cách nối chuỗi phía bên trái với chuỗi phía bên phải.

```c++
#include <iostream>
using namespace std;
int main() {
    string str1 = "Hello, ";
    string str2 = "world!";
    string result = str1 + str2;
    cout << result << endl;  
    return 0;
}
```

#### 3.2. Sử dụng std::stringstream để nối nhiều chuỗi

Khi cần nối nhiều chuỗi lại với nhau, đặc biệt trong vòng lặp hoặc khi làm việc với số lượng lớn chuỗi, sử dụng std::stringstream có thể là một lựa chọn hiệu quả hơn so với các phương pháp khác. std::stringstream hoạt động giống như một bộ đệm, giúp tránh việc tạo ra nhiều chuỗi trung gian.

```c++
#include <iostream>
#include <sstream>
using namespace std;
int main() {
    string str1 = "Hello";
    string str2 = ", ";
    string str3 = "world";
    string str4 = "!";
    stringstream ss;
    ss << str1 << str2 << str3 << str4;
    string result = ss.str();
    cout << result << endl;  
    return 0;
}
```

**Giải thích:**

- **stringstream ss;** khởi tạo một đối tượng stringstream.

- **ss << str1 << str2 << str3 << str4;** nối các chuỗi str1, str2, str3, và str4 lại với nhau trong stringstream.

- **ss.str();** trả về chuỗi kết quả.

Phương pháp này giúp bạn nối nhiều chuỗi mà không cần tạo ra nhiều chuỗi trung gian, giúp tiết kiệm bộ nhớ và tối ưu hóa hiệu suất.

### 4. String Pluralization

Đa dạng hóa số lượng từ (Pluralization) là một khái niệm quan trọng trong việc xử lý chuỗi, đặc biệt là khi bạn cần phải hiển thị các thông điệp hoặc nội dung có liên quan đến số lượng. Ví dụ, bạn có thể muốn hiển thị "1 item" nếu số lượng là 1, nhưng hiển thị "2 items" nếu số lượng lớn hơn 1. Việc này đòi hỏi bạn phải xử lý chuỗi để thêm phần kết thúc phù hợp với từ (thường là thêm "s" trong tiếng Anh).

```c++
#include <sstream>
#include <string>
using namespace std;
string pluralize(int count, string singular, string plural) {
    stringstream builder;
    builder << count << " ";  
    if (count <= 1) {
        builder << singular;
    } else {
        builder << plural;
    }
    string result = builder.str();
    return result;
}
int main() {
    int itemCount = 5;
    string message = "You have " + pluralize(itemCount, "item", "items") + " in your cart.";
    cout << message << endl;  
    return 0;
}
```