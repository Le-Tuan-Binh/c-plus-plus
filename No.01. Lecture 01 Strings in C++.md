## Getting Started

Trong ngôn ngữ lập trình C++, `std::string` là một kiểu dữ liệu chuỗi được định nghĩa trong thư viện tiêu chuẩn `<string>`. Nó cung cấp một cách linh hoạt và an toàn hơn để làm việc với chuỗi so với chuỗi kiểu C truyền thống.

Trong bài viết này sẽ hướng dẫn bạn qua các bước cơ bản để sử dụng chuỗi trong C++, từ khởi tạo đến thao tác trên chuỗi, và một số kĩ thuật hiện đại với chuỗi.

## Getting Involved

### 1. Khai báo

Để sử dụng thư viện `string`, bạn cần include gói thư viện `string` vào chương trình của mình. Dưới đây là một số cách khai báo thường thấy trong quá trình sử dụng chuỗi.

Lưu ý: Đối với `string`, kí tự cuối cùng của một chuỗi luôn luôn là ký tự `NULL`, kí tự này giúp cho ngôn ngữ lập trình biết được đây là `vị trí kết thúc của chuỗi`. Tuy nhiên ta không thể truy cập được kí tự NULL này và các hàm của lớp string cũng đã xử lý triệt để vấn đề này.

![alt text](/images/image_02.png)

#### 1.1 Khai báo chuỗi rỗng

Để khai báo một chuỗi rỗng trong C++, bạn sử dụng cú pháp sau:

```bash
string name_string;
```

**Giải thích:**

- std::string: Là lớp chuỗi từ thư viện chuẩn của C++ (string).
- name_string: Tên của biến chuỗi bạn đang khai báo.
- Khi bạn khai báo như trên, name_string sẽ được khởi tạo là một chuỗi rỗng, tức là không chứa bất kỳ ký tự nào.

#### 1.2 Khai báo chuỗi có giá trị ban đầu

Để khai báo một chuỗi có giá trị ban đầu trong C++, bạn có thể sử dụng cú pháp sau:

```bash
string name_string {value}
```

**Giải thích:**

- Trong trường hợp này, name_string sẽ được khởi tạo với giá trị `value`.
- Chuỗi name_string sẽ có độ dài bằng độ dài của chuỗi `value`, và chứa các ký tự tương ứng.

#### 1.3 Khai báo chuỗi có giới hạn độ dài với giá trị ban đầu

Đôi khi, bạn có thể muốn khai báo một chuỗi có độ dài tối đa (giới hạn số lượng ký tự) và cũng có giá trị ban đầu. Trong C++, bạn có thể làm như sau:

```bash
string name_string {value,max_size};
```

**Giải thích:**

- name_string: Tên của biến chuỗi.
- value: Giá trị ban đầu của chuỗi.
- max_size: Giới hạn số lượng ký tự tối đa mà chuỗi name_string có thể chứa.
- Khi bạn khai báo như trên, chuỗi name_string sẽ có độ dài tối đa là max_size và được khởi tạo với giá trị `value`.

Nếu độ dài của `value` lớn hơn max_size, chỉ số lượng ký tự đầu tiên của `value` sẽ được sao chép vào name_string.

#### 1.4 Khai báo chuỗi với số lần lặp của một kí tự nào đó

```bash
string name_string (loop_size,char);
```

Tuy nhiên bạn cần lưu với phương pháp khai báo chuỗi với số lần lặp của 1 kí tự nào đó ta cần chú ý những điều quan trọng sau

**1. Giá trị value phải là kí tự**

```c++
string name_string (6,’o’);
```

Với đoạn code bên trên ta có được giá trị hiển thị là

```bash
oooooo
```

**2. Phải sử dụng cặp ngoặc `()`**

```c++
string name_string {111,’z’};
```

Tuy nhiên với đoạn chương trình phía trên kết quả ta mong muốn là `111` chữ `z` tuy nhiên ta lại nhận được kết quả phía bên dưới

```bash
oz
```

Giải thích: Giá trị `111` trong bảng mã Asscii là `o`, nên lúc này `name_string` sẽ có 2 phần tử là `o` và `z`.

#### 1.5 Khai báo chuỗi từ một chuỗi khác

Để khai báo một chuỗi từ một chuỗi khác trong C++, bạn có thể sử dụng cú pháp sau:

```c++
string name_string{other_String};
```

**Giải thích:**

- name_string: Tên của biến chuỗi mới bạn đang khai báo.
- other_String: Chuỗi mà bạn muốn sao chép giá trị từ đó vào name_string.

#### 1.6 Khai báo chuỗi từ một chuỗi khác từ vị trí start với number kí tự

```c++
string name_string {other_string,start,number}
```

Dưới đây là ví dụ cho cách hoạt động của việc khai báo từ một chuỗi khác với vị trí bắt đầu và số lượng kí tự của chuỗi mới.

![alt text](./images/image_01.png)

Tuy nhiên có một số trường hợp bàn cần phải lưu ý. Đoạn chương trình bên dưới là một trường hợp rất dễ nhầm lẫn trong quá trình sử dụng.

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
    string name = "Le Tuan Binh";

    string _pharse{name,5};

    string phrase{"Le Tuan Binh", 5};

    cout<<_pharse<<endl;

    cout<<phrase<<endl;
}
```

Bạn có thể thấy khi thực hiện chương trình trên, nhìn thoáng qua ta nghĩ kết quả của chúng có thể như nhau nhưng thực tế thì kết quả có chút khác biệt. Đây là kết quả hiển thị trên màn hình

```bash
an Binh
Le Tu
```

Thật lạ phải không, để giải thích cho việc này chúng ta hãy xem qua đoạn giải thích bên dưới:

- Đối với `_pharse`, tham số truyền vào là một chuỗi trong một biến, do đó thực hiện lấy hết kí tự từ vị trí 5 trong chuỗi name.

- Đối với `phrase`, tham số truyền vào hàm là một chuỗi trực tiếp, do đó thực hiện lấy 5 kí tự đầu tiên trong chuỗi name.

### 2. Chuyển đổi string sang chuỗi kí tự

Có 2 cách chuyển đổi một chuỗi dạng string sang chuỗi kí tự trong C, đây chỉ là một trong những cách khuyến khích và đề xuất, các bạn có thể sử dụng các cách dùng khác.

#### 2.1 Sử dụng hàm c_str()

Hàm `c_str()` trả về một con trỏ `const char*` trỏ đến mảng ký tự trong chuỗi std::string. Đây là cách khuyến khích để nhận một phiên bản không thể thay đổi của chuỗi như một mảng ký tự.

```c++
const char* c_string = name_string.c_str();
```

**Giải thích:**

- name_string: Là chuỗi std::string mà bạn muốn chuyển đổi.
- c_str(): Là phương thức của lớp std::string trả về con trỏ `const char*` tới một mảng ký tự.
- c_string: Là con trỏ trỏ đến mảng ký tự của chuỗi name_string.

**Lưu ý:** Chuỗi trả về từ c_str() là `const char*`, điều này có nghĩa là bạn không thể thay đổi các ký tự trong chuỗi bằng cách sử dụng con trỏ này. Nếu bạn cần thay đổi chuỗi, hãy sao chép nó vào một mảng ký tự mới.

#### 2.2 Sử dụng hàm data()

Hàm `data()` cũng trả về một con trỏ `char*` tới mảng ký tự trong chuỗi `std::string`, nhưng không yêu cầu rằng dữ liệu phải là const, do đó bạn có thể sửa đổi nội dung của chuỗi được trả về.

```c++
char* c_string = name_string.data();
```

**Giải thích:**

- name_string: Là chuỗi std::string mà bạn muốn chuyển đổi.
- data(): Là phương thức của lớp std::string trả về con trỏ `char*` tới một mảng ký tự.
- c_string: Là con trỏ trỏ đến mảng ký tự của chuỗi name_string.

**Lưu ý:** Với `data()`, bạn có thể thay đổi nội dung của chuỗi thông qua con trỏ `char*` được trả về. Tuy nhiên, bạn cần cẩn thận để đảm bảo rằng chuỗi std::string vẫn tồn tại và không bị hỏng khi thay đổi nội dung bên ngoài.

Trong cả hai trường hợp, bạn cần đảm bảo rằng chuỗi `std::string` mà bạn `đang tham chiếu vẫn tồn tại` khi bạn đang sử dụng con trỏ char* được trả về. Nếu chuỗi std::string bị hủy, con trỏ `char*`sẽ trỏ đến`dữ liệu không hợp lệ`, dẫn đến hành vi không xác định trong chương trình của bạn.

### 3. Nhập chuỗi từ bàn phím

#### 3.1 Đối với chuỗi không có khoảng trắng

Sử dụng `std::cin` để nhập chuỗi không chứa khoảng trắng.

Khi sử dụng operator `>>` của `std::cin`, nó chỉ nhận vào một từ đầu tiên cho đến khi gặp khoảng trắng hoặc ký tự newline (\n). Điều này có nghĩa là nếu bạn nhập nhiều từ cùng lúc, chỉ từ đầu tiên sẽ được lưu vào biến chuỗi.

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
    string str;
    cout << "Input string: ";cin >> str;
    cout << "The string is: " << str << std::endl;
    return 0;
}
```

#### 3.2 Đối với chuỗi có khoảng trắng

Hàm `std::getline` cho phép bạn nhập một chuỗi từ `std::cin` mà không bị giới hạn bởi khoảng trắng. Đây là một cách hiệu quả để nhận dữ liệu người dùng từ bàn phím.

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
    string str;
    cout << "Input string: ";
    getline(cin,str);
    cout << "The string is: " << str << std::endl;
    return 0;
}
```

**Giải thích:**

- std::getline(std::cin, str): Hàm này sẽ đọc toàn bộ dòng từ std::cin và lưu vào biến str.

- Nó sẽ dừng khi gặp dấu xuống dòng (\n) hoặc khi hết dữ liệu có thể đọc được.

- Với việc sử dụng `std::getline`, bạn có thể nhập một chuỗi đầy đủ từ người dùng mà không bị giới hạn bởi khoảng trắng. Điều này giúp đơn giản hóa việc xử lý dữ liệu từ bàn phím khi các dữ liệu đầu vào có thể chứa nhiều từ hay một dòng văn bản.

#### 3.3 Xử lý trôi lệnh trong ngôn ngữ C++

Để hiểu rõ vấn đề, bạn hay xem đoạn chương trình phía dưới, khi chúng ta cố gắng nhập một số và một chuỗi, chương trình sau khi nhận được giá trị số từ người dùng, sẽ không cho phép nhập giá trị chuỗi. Trong C++ nó gọi là trôi lệnh.

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
    int number; cin >> number;
    string str;
    cout << "Input string: ";
    getline(cin,str);
    cout<<"The number is: "<<number<<endl;
    cout<<"The string is: "<<str;
    return 0;
}
```

Đây là giá trị đầu vào và giá trị đầu ra mà ta nhận được từ đoạn chương trình trên

```bash
Input string: 123 Le Tuan Binh
The number is: 123
The string is:
```

**Giải thích:**

- Bản chất của hàm getline, nó sẽ dừng đọc chuỗi khi gặp kí tự xuống dòng. Do đó khi sử dụng getline cần luôn đảm bảo trước khi thực hiện getline không còn thừa kí tự enter nào trong bộ nhớ đệm.
- Bên cạnh đó, hàm cin sẽ luôn để lại một kí tự xuống dòng trong bộ nhớ đệm của bàn phím.
- Vì vậy trước khi sử dụng getline, mà có xuất hiện hàm cin cần phải xử lý kí tự enter đó.

Bạn có thể xử lý việc này bằng một số phương pháp khác nhau, tuy nhiên bài viết này sẽ đề xuất bạn một phương pháp cơ bản và dễ nhất.

Sử dụng `cin.ignore()` để bỏ qua n kí tự trong bộ đệm bàn phím, với cách này bạn có thể bỏ qua được kí tự mà `cin` để lại trong bộ đệm bàn phím.

```c++

#include <iostream>
#include <string>
using namespace std;
int main() {
    int number; cin >> number;
    cin.ignore(1);
    string str;
    cout << "Input string: ";
    getline(cin,str);
    cout<<"The number is: "<<number<<endl;
    cout<<"The string is: "<<str;
    return 0;
}
```

### 4. Một số hàm thông dụng trong thư viện <string>

#### 4.1 Hàm size() và Hàm length()

Trong thư viện <string> của C++, có nhiều hàm hữu ích để làm việc với chuỗi (std::string). Trong số đó, size() và length() là hai hàm cơ bản cho phép bạn lấy độ dài của chuỗi.

```c++
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";

    // Sử dụng hàm size()
    std::cout << "Length of the string (using size()): " << str.size() << std::endl;

    return 0;
}
```

**Lưu ý:**

- Cả hai hàm size() và length() đều trả về giá trị kiểu size_t, là kiểu dữ liệu không âm được định nghĩa trong C++ để lưu trữ kích thước của các đối tượng.
- Bạn có thể sử dụng bất kỳ hàm nào trong hai hàm này để lấy độ dài của chuỗi, và không có sự khác biệt nào về hiệu suất hoặc tính năng giữa chúng.

#### 4.2 Hàm push_back()

Hàm `push_back()` trong C++ là một hàm thành viên của lớp `std::string`, được sử dụng để thêm một ký tự vào cuối chuỗi hiện tại.

```c++
<name_string>.push_back(<char>)
```

Bạn có thể xem ví dụ của đoạn chương trình sau

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
    string nameString = "Hi World!!!:3";
    nameString.push_back('3');
    cout << "After push back: " << nameString;
    cout<<endl;
}
```

```bash
After push back: Hi World!!!:33
```

#### 4.3 Hàm pop_back()

Hàm `pop_back()` trong C++ là một hàm thành viên của lớp `std::string`, được sử dụng để loại bỏ ký tự cuối cùng khỏi chuỗi hiện tại.

```c++
<name_string>.pop_back()
```

Bạn có thể xem ví dụ của đoạn chương trình sau

```c++
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello!";

    // Sử dụng hàm pop_back() để loại bỏ ký tự cuối cùng '!'
    str.pop_back();

    std::cout << "Modified string: " << str << std::endl;

    return 0;
}
```

```bash
Modified string: Hello
```

Không chỉ thế bạn có thể áp dụng `pop_back` và hàm `back` để có thể thực hiện nhiều yêu cầu phức tạp hơn như đoạn chương trình phía dưới

```c++
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";

    // Loại bỏ các ký tự phía sau dấu phẩy ','
    while (!str.empty() && str.back() != ',') {
        str.pop_back();
    }

    std::cout << "Modified string: " << str << std::endl;

    return 0;
}
```

```bash
Modified string: Hello,
```

#### 4.4 Hàm insert()

Chèn một xâu kí tự vào vị trí bất kì trong xâu ban đầu. Tham số truyền vào là vị trí cần chèn và xâu cần chèn vào trong chuỗi.

```c++
<name_string>.insert(index,stringInsert)
```

Bạn có thể tham khảo đoạn chương trình bên dưới để biết cách hoạt động của nó

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    std::string phrase{"We can insert a string."};
    std::string words{"a string into "};
    phrase.insert(14, words);
    cout << phrase;
}
```

![alt text](/images/image_03.png)

Tuy nhiên vẫn còn rất nhiều phiên bản của hàm `insert` mà bạn có thể tìm hiểu và áp dụng, dưới đây là một số phiên bản mà tôi biết

```bash
std::string& insert(size_t pos, const std::string& str);
std::string& insert(size_t pos, const std::string& str, size_t subpos, size_t sublen);
std::string& insert(size_t pos, const char* s);
std::string& insert(size_t pos, const char* s, size_t n);
std::string& insert(size_t pos, size_t n, char c);
```

**Trong đó**

- pos: Vị trí mà bạn muốn chèn nội dung vào.
- str: Chuỗi hoặc phần chuỗi mà bạn muốn chèn vào.
- subpos: Vị trí bắt đầu trong str để chèn.
- sublen: Số lượng ký tự từ str sẽ được chèn.
- s: Một con trỏ `const char*` tới một mảng ký tự mà bạn muốn chèn.
- n: Số lượng ký tự từ s sẽ được chèn.
- c: Ký tự mà bạn muốn chèn, sẽ được lặp lại n lần.

#### 4.5 Hàm erase()

Xóa một xâu kí tự từ vị trí bất kì trong xâu ban đầu. Tham số truyền vào là vị trí bắt đầu xía và độ dài của xâu cần xóa.

```c++
<name_string>.erase(index,lengthWantToDelete)
```

Để có thể trực quan hơn về cách hoạt động của nó, bạn hãy xem đoạn code phía bên dưới

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    std::string phrase{"We can insert a string."};
    phrase.erase(13, 2);
    cout << phrase;
}
```

Đoạn chương trình trên thực hiện xóa 2 kí tự tính từ vị trí 13. Do đó kết quả ta nhận được sẽ như bên dưới

```bash
We can insert string
```

Tuy nhiên khi sử dụng `erase()` bạn cần chú ý một số vấn đề sau

Lưu ý: Trong các tham số trên không bắt buộc phải truyền vào

- Nếu chỉ truyền vào 1 tham số, mặc định chương trình sẽ đọc đó là tham số của vị trí index và xóa từ index đến hết chuỗi.

**Ví dụ:**

```c++
std::string phrase{"We can insert a string."};
phrase.erase(13);
```

```bash
We can insert
```

- Nếu không truyền vào tham số nào, mặc định chương trình sẽ hiểu là xóa hết cả chuỗi

**Ví dụ:**

```c++
std::string phrase{"We can insert a string."};
phrase.erase();
```

> Đối vối một số yêu cầu trong thực tế, bạn cần xóa tất cả các kí tự nào đó trong chuỗi, đối với ngôn ngữ C++ 20 trở lên có hổ trợ một hàm `erase()` tuy nhiên cách dùng sẽ có chút khác biệt
>
> ```c++
> erase(namestrings,charWantToDelete)
> ```

Để có thể hình dung được cách hoạt động của nó, đoạn chương trình bên dưới sẽ thể hiện một cách minh họa cách phương thức `erase()` hoạt động

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string s{ "Hello!!!!!. This is my Program!!!"};
    erase(s, '!');
    cout << s;
}
```

```bash
Hello. This is my Program
```

#### 4.6 Hàm find()

Tìm kiếm một xâu con bất kì trong một xâu khác. Hàm trả về vị trí đầu tiên của xâu cần tìm kiếm trong xâu khác nếu tồn tại. Ngược lại hàm trả về giá trị string::npos.

Hãy xem đoạn chương trình phía dưới để có thể hình dung được cách hoạt động của nó

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string sentence{"Manners maketh man"};
    string word{"man"};
    cout << sentence.find(word) << endl; // Outputs 15
    cout << sentence.find("Ma") << endl; // Outputs 0
    cout << sentence.find('k') << endl;  // Outputs 10
    cout << sentence.find('x') << endl;  // Outputs string::npos
}
```

- Tuy nhiên khi thực hiện chạy chương trình, ta nhận được kết quả như sau với giá trị của string::npos là 18446744073709551615.
- Trong ngôn ngữ lập trình C++, string::npos được định nghĩa là một giá trị rất lớn có thể được biểu diễn ở kiểu dữ liệu size_t.
- Với hệ điều hành 64-bits, giá trị này có thể lên tới 2^64 – 1

Bạn có thể sử dụng string::npos để kiểm tra một chuỗi có xuất hiện trong chuỗi khác hay không bằng cách như sau.

```c++
if (sentence.find("Hello") == std::string::npos){
    std::cout << "Character not found" << std::endl;
} 
```

Không chỉ thế hàm `find()` còn có rất nhiều cách dùng khác nhau, bạn có thể tìm hiểu thêm về cách dùng hàm `find()` tại đây [std::string::find()](https://cplusplus.com/reference/string/string/find/).

Dưới đây tôi sẽ cùng bạn tìm hiểu về một cách dùng của hàm `find()` như sau

```bash
find(stringWantToFind,startIndex)
```

> Tìm kiếm chuỗi từ vị trí startIndex, trả về vị trí xuất hiện đầu tiên của chuỗi cần tìm kiếm, nếu không tìm thấy trả về string::npos.

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string sentence{"Manners maketh man"};
    string word{"man"};
    std::cout << sentence.find("an", 1) << std::endl;
    std::cout << sentence.find("an", 3) << std::endl;
}
```

```bash
1
16
```

Hãy xem một ứng dụng của hàm `find()` mà chúng ta thường thấy nhất sau đây

> Đếm số lần xuất hiện của một chuỗi nào đó trong chuỗi khác
> Lưu ý: Các chuỗi con có thể chồng chéo nhau

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    std::string sentence{"Manners maketh man"};
    std::string word{"an"};
    int count{};
    for (size_t i{}; i <= sentence.length() - word.length();)
    {
        size_t position = sentence.find(word, i);
        if (position == std::string::npos)
            break;
        ++count;
        i = position + 1;
    }
    std::cout << '"' << word << "\" occurs in \"" << sentence
              << "\" " << count << " times." << std::endl;
}
```

Bên cạnh đó hàm `find()` còn có một cách dùng thường được sử dụng như sau

```bash
find(stringWantToFind,startIndex,numberOfCharacter)
```

Tìm kiếm `numberOfCharacter` kí tự tính từ `trái sang phải` của `stringWantToFind` `bắt đầu từ vị trí startIndex` của xâu cần tìm kiếm.

Bạn hãy xem đoạn chương trình tham khảo phía bên dưới để có thể hiểu rõ được cách dùng của nó nhé

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    std::string sentence{"Manners maketh man"};
    std::cout << sentence.find("ananas", 8, 2) << std::endl;
}

```

**Giải thích:** Tìm kiếm 2 kí tự đầu của `“ananas”` là `“an”` trong chuỗi sentence từ vị trí số `8`. Kết quả trả ra là `16`.

Một số tình huống bạn có thể gặp trong thực tế, hãy cùng tôi xem qua nhé.

> Đếm số lần xuất hiện của một chuỗi nào đó trong một chuỗi nào đó, các chuỗi con không thể chồng chéo nhau.

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    std::string text; // The string to be searched
    std::string word; // Substring to be found
    std::cout << "Enter the string to be searched and press Enter:\n";
    std::getline(std::cin, text);
    std::cout << "Enter the string to be found and press Enter:\n";
    std::getline(std::cin, word);
    size_t count{}; // Count of substring occurrences
    size_t index{}; // String index
    while ((index = text.find(word, index)) != std::string::npos)
    {
        ++count;
        index += word.length(); // Advance by full word (discards overlapping occurrences)
    }
    std::cout << "Your text contained " << count << " occurrences of \""
              << word << "\"." << std::endl;
}
```

Bạn có thể xem hình ảnh minh họa phía dưới đây để có thể hiểu rõ cách hoạt động của nó.

![alt text](/images/image_04.png)
