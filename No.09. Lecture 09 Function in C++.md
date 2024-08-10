## Getting Started

Tất cả các chương trình bạn đã viết cho đến nay đều chỉ bao gồm một hàm duy nhất là main(). 

Một ứng dụng C++ thực tế bao gồm nhiều hàm, mỗi hàm cung cấp một khả năng riêng biệt và được xác định rõ ràng. 

Việc thực thi bắt đầu từ hàm main(), hàm này phải được định nghĩa trong không gian tên toàn cục. Hàm main() sẽ gọi các hàm khác, và mỗi hàm này có thể gọi các hàm khác nữa, và cứ thế tiếp diễn. 

## Getting Involved

Khi một hàm gọi một hàm khác, rồi hàm này lại gọi một hàm khác nữa, và cứ tiếp tục như vậy, bạn sẽ có một tình huống mà nhiều hàm đang hoạt động đồng thời. Mỗi hàm đã gọi hàm khác mà chưa trả về sẽ đang chờ đợi hàm được gọi kết thúc. 

Rõ ràng, cần có cái gì đó để theo dõi từ đâu trong bộ nhớ mà mỗi lệnh gọi hàm được thực hiện và nơi nào chương trình sẽ tiếp tục khi một hàm trả về.

Thông tin này được ghi lại và quản lý tự động trong **Stack**. Call stack ghi lại tất cả các lệnh gọi hàm chưa hoàn thành và chi tiết của dữ liệu được truyền vào mỗi hàm. 

Một hàm nên thực hiện một **hành động đơn lẻ** và được **xác định rõ ràng**, đồng thời nên tương đối ngắn gọn. 

### 1. Định nghĩa hàm

Một hàm là một khối mã độc lập với một mục đích cụ thể. Các định nghĩa hàm nói chung có cấu trúc cơ bản giống như hàm main(). Một định nghĩa hàm bao gồm một tiêu đề hàm (function header) theo sau là một khối mã chứa mã lệnh cho hàm đó. Tiêu đề hàm xác định ba điều sau:

- **Kiểu trả về**: đó là loại giá trị, nếu có, mà hàm trả về khi kết thúc thực thi. Một hàm có thể trả về dữ liệu thuộc bất kỳ loại nào, bao gồm các kiểu cơ bản, kiểu lớp, kiểu con trỏ, hoặc kiểu tham chiếu. Nó cũng có thể không trả về gì, trong trường hợp đó bạn chỉ định kiểu trả về là **void**.

- **Tên của hàm**: Tên hàm được đặt theo cùng các quy tắc như biến. Thông thường sẽ đặt tên theo quy tắc `camelCase`.

- Danh sách tham số (**parameter list**):  và nó xuất hiện dưới dạng một danh sách các phần tử được phân tách bằng dấu phẩy giữa các dấu ngoặc đơn theo sau tên hàm.

```c++
return_type function_name(parameter_list)
{
/* Code for the function... */
}
```

Bạn có thể xem hình ảnh phía dưới để hiểu rõ hơn về cách hàm hoạt động và cách chương trình thực thi nó 

![alt text](/images/image-08.png)

**Nguyên mẫu hàm (function prototype)** là một mô tả một hàm đủ để trình biên dịch có thể biên dịch các lệnh gọi đến hàm đó. Nó xác định tên hàm, kiểu trả về của hàm và danh sách tham số của nó. Nguyên mẫu hàm đôi khi còn được gọi là khai báo hàm (function declaration).

### 2. Tham số truyền vào hàm

Trong ngôn ngữ lập trình C++, chúng ta có 2 cách truyền tham số vào hàm lần lượt là truyền theo giá trị (pass-by-value) và truyền theo tham chiếu (pass-by-reference).

#### 2.1 Pass-By-Value

Khi thực hiện truyền đối số ở dạng `Pass-by-value` Không có đối số nào được truyền trực tiếp vào hàm. Thay vào đó, các bản sao của các đối số được tạo ra, và những bản sao này được chuyển vào hàm.

![alt text](/images/image-09.png)

Mỗi lần bạn gọi hàm **power()**, trình biên dịch sắp xếp để các bản sao của các đối số được lưu trữ ở một vị trí tạm thời trong ngăn xếp lệnh gọi (call stack). Trong quá trình thực thi, tất cả các tham chiếu đến các tham số của hàm trong mã đều được ánh xạ đến các bản sao tạm thời của các đối số này. Khi quá trình thực thi của hàm kết thúc, các bản sao của đối số sẽ bị loại bỏ.

Bạn hãy xem đoạn chương trình bên dưới để hiểu rõ cơ chế hoạt động của nó

```c++
#include <iostream>
using namespace std;
void increaseByFive(int x) {
    x += 5;
    cout << "Value of x inside the increaseByFive function: " << x << endl;
}
int main() {
    int a = 10;
    increaseByFive(a);
    cout << "Value of a after calling increaseByFive: " << a << endl;
    return 0;
}
```

Kết quả trên màn hình ta nhận được

```bash
Value of x inside the increaseByFive function: 15
Value of a after calling increaseByFive: 10
```

Truyền tham số theo giá trị (pass-by-value) là cơ chế mặc định bằng cách nào đối số được truyền vào một hàm. Nó cung cấp nhiều bảo mật cho hàm gọi bằng cách ngăn hàm đó sửa đổi các biến thuộc về hàm gọi. Tuy nhiên, đôi khi bạn muốn sửa đổi các giá trị trong hàm gọi. Có cách nào để thực hiện điều đó khi bạn cần không?

#### 2.2 Pass-By-Reference