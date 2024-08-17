## Getting Started

Trong C++20, chúng ta có một cách tiếp cận linh hoạt hơn để tạo chuỗi đầu ra, gọi là string interpolation (nội suy chuỗi). Với string interpolation, chúng ta tạo một chuỗi chứa các ký tự đặc biệt đại diện cho placeholder (chỗ trống). Một chuỗi có chứa các placeholder này được gọi là chuỗi định dạng (format string).

Khi có chuỗi định dạng, chúng ta cung cấp các giá trị để chèn vào các chỗ trống, thay thế cho các ký hiệu placeholder đó.

Từ C++20 trở đi, thư viện chuẩn có hỗ trợ tính năng này thông qua std::format().

## Getting Involved

### 1. std::format()

**std::format()** nằm trong thư viện <format>. Cách sử dụng cơ bản là ta cung cấp một chuỗi định dạng làm tham số đầu tiên, chuỗi này sẽ chứa placeholder {}. Sau đó, ta cung cấp giá trị để chèn vào chỗ trống đó như tham số thứ hai:

```c++
#include <format>
int main(){
  std::format("I have {} apples", 5);
}
```

std::format() trả về một std::string, có thể lưu trữ như bất kỳ chuỗi nào khác, hoặc có thể xuất trực tiếp ra console bằng đoạn code bên dưới

```C++
#include <format>
#include <iostream>
int main(){
  std::string Apples{
    std::format("I have {} apples", 5)};
  std::cout << Apples
    		<< std::format(" and {} bananas", 2);
}
```

Chuỗi định dạng của chúng ta có thể có bất kỳ số lượng chỗ trống nào, chúng ta có thể điền các giá trị được cung cấp dưới dạng đối số bổ sung:

```c++
#include <format>
#include <iostream>

int main(){
  std::string Fruit{
    std::format(
      "{} apples, {} bananas, and {} pears",5, 2, 8)};
  std::cout << Fruit;
}
```
### 2. std::print()

C++23 giới thiệu thêm hàm std::print(), kết hợp tính năng của std::format() và tự động gửi đầu ra đến luồng, như std::cout.

Thay vì chúng ta viết

```c++
#include <format>
#include <iostream>
int main() {
  std::cout << std::format("{} apples", 5);
}
```

Chúng ta có thể viết lại thành như sau

```c++
#include <print>

int main(){
  std::print("{} apples", 5);
}
```

Chúng tôi sẽ tiếp tục sử dụng std::format() trong các ví dụ còn lại vì nó được sử dụng phổ biến hơn nhiều. Nhưng khi làm việc trên một dự án hỗ trợ std::print(), bạn nên lưu ý rằng đây là một tùy chọn.

Nếu bạn muốn in dấu { hoặc } trong chuỗi, bạn cần nhân đôi chúng. Ví dụ:

```c++
#include <format>
#include <iostream>

int main(){
  std::string Fruit{
    std::format(
      "{} apples and some braces: {{ }}", 5
    )};
  std::cout << Fruit;
}
```

```bash
5 apples and some braces: { }
```

**Positional Arguments**

Như chúng ta đã thấy, mỗi chỗ giữ chỗ được đánh dấu {} tương ứng tuần tự với các giá trị biến của chúng ta. {} đầu tiên được thay thế bằng giá trị đầu tiên, {} thứ hai được thay thế bằng giá trị thứ hai, v.v.

Chúng ta có thể kiểm soát điều này bằng cách chèn các số nguyên giữa các dấu ngoặc nhọn, biểu thị giá trị nào sẽ sử dụng. Các vị trí này bắt đầu từ số không, nghĩa là chúng ta bắt đầu đếm từ 0.

Điều đó có nghĩa là giá trị đầu tiên có chỉ số là 0, giá trị thứ hai có chỉ số là 1, v.v. Đây là một quy ước khá phổ biến trong lập trình và chúng ta sẽ thấy thêm các ví dụ về nó sau.

Cung cấp các đối số vị trí này cho phép chúng ta kiểm soát thứ tự các giá trị của mình được sử dụng để tạo chuỗi cuối cùng:

```c++
#include <format>
#include <iostream>
int main(){
	std::string Name{std::format("{1}, {0}", "James", "Bond")};
	std::cout << Name;
}
```

```c++
#include <format>
#include <iostream>

int main(){
	std::string Name{
	std::format("{1}, {0} {1}","James", "Bond")};
	std::cout << Name;
}
```

**Formatting Specifiers**

Khi chúng ta chèn giá trị vào chuỗi định dạng của mình, chúng ta thường có thể chỉ định các tùy chọn bổ sung, kiểm soát cách các giá trị đó được chèn vào.

Trong trình giữ chỗ, chúng ta truyền các tùy chọn sau ký tự dấu hai chấm `:`

Ví dụ, các kiểu số hỗ trợ trình chỉ định +, sẽ thêm tiền tố + vào giá trị, nếu giá trị là số dương. Để sử dụng trình giữ chỗ, trình giữ chỗ của chúng ta sẽ trông giống như {:+} như được hiển thị bên dưới:

```c++
#include <format>
#include <iostream>
int main(){
	std::string Number{std::format("{:+}", 10)};
	std::cout << Number;
}
```

**Đối số vị trí** của trình giữ chỗ nằm trước dấu `:` vì vậy, khi chúng ta sử dụng cả đối số vị trí và trình chỉ định định dạng, trình giữ chỗ của chúng ta sẽ trông như thế này:

```c++
#include <format>
#include <iostream>
int main(){
	std::string Number{std::format("{0:+}, {1:+}", 10, -42)};
	std::cout << Number;
}
```

**Minimum Width Formatting**

Việc truyền một số nguyên dương đơn giản làm trình chỉ định định dạng sẽ đặt chiều rộng tối thiểu của giá trị đó trong chuỗi.

Ví dụ, chèn một số nguyên như 3 vào chuỗi chỉ cần một khoảng trắng. Nhưng nếu chúng ta đặt chiều rộng tối thiểu là 6, thì sẽ thêm khoảng trắng để đảm bảo biến của chúng ta sử dụng ít nhất 6 ký tự:

```C++
#include <format>
#include <iostream>
int main(){
	std::string Fruit{std::format("I have {:6} apples", 3)};
	std::cout << Fruit;
}
```
Các chỉ định về chiều rộng tối thiểu và căn chỉnh chủ yếu hữu ích khi chúng ta xuất nhiều dòng văn bản.

Ví dụ, nếu chúng ta đang cố gắng tạo một bảng, chúng ta sẽ muốn các cột của mình được căn chỉnh theo chiều dọc. Việc thiết lập chiều rộng tối thiểu có thể giúp chúng ta đạt được điều đó.

Dưới đây, chúng ta sử dụng các chỉ định này để tạo một bảng gồm 3 cột, với chiều rộng lần lượt là 8, 5 và 6:

```c++
#include <format>
#include <iostream>

int main(){
  std::cout
    << std::format(
      "{:8} | {:5} | {:6} |",
      "Item", "Sales", "Profit")

    << std::format(
      "\n{:8} | {:5} | {:6} |",
      "Apples", 53, 8.21)

    << std::format(
      "\n{:8} | {:5} | {:6} |",
      "Bananas", 194, 33.89)

    << std::format(
      "\n{:8} | {:5} | {:6} |",
      "Pears", 213, 106.35);
}
```

Kết quả ta nhận được là

```bash
Item     | Sales | Profit |
Apples   |    53 |   8.21 |
Bananas  |   194 |  33.89 |
Pears    |   213 | 106.35 |
```

**Alignment and Fill Formatting**

Khi biến của chúng ta là một số nguyên, chúng ta có thể thêm tiền tố 0 vào giá trị chiều rộng tối thiểu. Điều này có tác dụng là bất kỳ khoảng trắng bổ sung nào được chèn vào đều được điền bằng các số 0 đứng đầu:

```c++
#include <format>
#include <iostream>

int main(){
  std::string Fruit{
    std::format("I have {:04} apples", 3)};
  std::cout << Fruit;
}
```

Kết quả nhận được

```bash
I have 0003 apples
```

**Left, Center, and Right Alignment**

Chúng ta có thể thêm tiền tố cho chỉ định chiều rộng của mình bằng một ký tự bổ sung, chỉ định cách giá trị của chúng ta sẽ được căn chỉnh trong chiều rộng đó.

- `<` biểu thị căn trái
- `^` biểu thị căn giữa
- `>` biểu thị căn phải

Ví dụ, nếu chúng ta muốn chiều rộng trường của mình là 12 khoảng trắng và để giá trị của chúng ta được căn giữa trong khoảng trắng đó, chỗ giữ chỗ của chúng ta sẽ là {:^12}

```c++
#include <format>
#include <iostream>

int main(){
	std::string Alignment{std::format("| {:^12} |","Center")};
	std::cout << Alignment;
}
```

Ví dụ sau đây cho thấy tác dụng của ba tùy chọn căn chỉnh:

```c++
#include <format>
#include <iostream>

int main(){
	std::string Alignment{
		std::format("| {:<12} |\n| {:^12} |\n| {:>12} |",
			"Left", "Center", "Right"
		)};
	std::cout << Alignment;
}
```

Chúng ta cũng có thể đặt một ký tự trước mũi tên căn chỉnh, chỉ rõ chúng ta muốn điền vào khoảng trống bổ sung nào. Dưới đây, chúng ta điền vào khoảng trống bằng `-` ký tự:

```c++
#include <format>
#include <iostream>

int main(){
  std::string Alignment{
    std::format(
		"| {:-<12} |\n| {:-^12} |\n| {:->12} |",
		"Left", "Center", "Right")};
	std::cout << Alignment;
}
```

```bash
| Left-------- |
| ---Center--- |
| -------Right |
```

**Float Precision**

Yêu cầu định dạng phổ biến nhất khi làm việc với số dấu phẩy động là đặt mức độ chính xác của chúng.

Điều này được thực hiện bằng cách sử dụng dấu . theo sau là số chữ số có nghĩa mà chúng ta muốn đưa vào chuỗi kết quả:

```C++
#include <format>
#include <iostream>

int main(){
  float Pi{3.141592};
  std::cout
    << std::format("Pi: {:.1}", Pi)
    << std::format("\nPi: {:.3}", Pi)
    << std::format("\nPi: {:.5}", Pi);
}
```

Bên dưới, chúng tôi đã kết hợp điều này với `đối số chiều rộng (8)` cùng với căn chỉnh bên phải bằng cách sử dụng `>`, với bất kỳ khoảng trống thừa nào được điền bằng ký tự `-`:

```c++
#include <format>
#include <iostream>

int main(){
  float Pi{3.141592};
  std::cout
    << std::format("Pi: {:->8.1}", Pi)
    << std::format("\nPi: {:->8.3}", Pi)
    << std::format("\nPi: {:->8.5}", Pi);
}
```

Kết quả trên màn hình sẽ là

```bash
Pi: -------3
Pi: ----3.14
Pi: --3.1416
```