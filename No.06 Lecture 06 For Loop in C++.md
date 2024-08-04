## Getting Started

**Vòng lặp for**: là một cơ chế cho phép bạn thực thi một câu lệnh hay một khối lệnh lặp đi lặp lại cho đến khi một điều kiện nào đó thõa mãn.

Một cấu trúc vòng lặp cơ bản bao gồm 2 thành phần chính

- Các câu lệnh và khối câu lệnh được thực hiện lặp đi lặp lại.

- Điều kiện dừng của vòng lặp, các giá trị khởi tạo và biến tăng của vòng lặp.

## Getting Involved

### 1. Vòng lặp cơ bản

Vòng lặp for thường thực thi một câu lệnh hoặc khối câu lệnh với số lần được xác định trước, nhưng bạn cũng có thể sử dụng nó theo những cách khác.

![alt text](/images/image_05.png)

Trong đó:

- initialization: Các giá trị khởi tạo khi vòng lặp bắt đầu

- condition: Điều kiện dừng của vòng lặp

- iteration: Bước nhảy của giá trị mỗi lần lặp

Trong 3 giá trị này, bạn có thể bỏ qua bất kì thành phần nào, tuy nhiên dấu **;** bắt buộc phải tồn tại khi thiếu các thành phần.

```c++
for (std::size_t i{0};;i++){
	cout<<"HELLO WORLD"<<endl;
}
```

Đoạn chương trình bên trên thực hiện in ra liên tục dòng chữ `HELLO WORLD` không có điều kiện dừng.

Biểu thức khởi tạo của vòng lặp chỉ được thực thi một lần duy nhất khi mới bắt đầu vòng lặp. Sau đó điều kiện vòng lặp được kiểm tra, nếu đúng thực hiện khối lệnh bên trong vòng lặp, nếu sai thì vòng lặp kết thúc. Sau mỗi lần thực thi khối lệnh vòng lặp thì biểu thức lặp hay còn gọi là biến nhảy của vòng lặp được thực hiện và tiếp tục kiểm tra điều kiện.

Bên cạnh đó bạn có thể dùng một biến `local` để đưa vào vòng lặp thay vì khởi tạo giá trị ban đầu và biến này sẽ tự biến mất.

```c++
std::size_t i {};
for (i = 0; i < 12; ++i) 
{
cout<<"Hello World"<<endl;
}
```

Trong đoạn chương trình này, biến `i` được truyền vào tham số khởi tạo của vòng lặp, do đó khi kết thúc vòng lặp, ta vẫn có thể truy cập và sử dụng được biến `i`.

### 2. Biểu thức vòng lặp có thể còn phức tạp hơn thế ?

Bạn có thể định nghĩa và khởi tạo **nhiều hơn một biến** của một kiểu nhất định trong biểu thức điều khiển vòng lặp for đầu tiên. 

Bạn chỉ cần tách từng biến khỏi biến tiếp theo bằng **dấu phẩy**. Sau đây là một ví dụ thực tế sử dụng điều đó:

```c++
for (int i = 0, j = 10; i < j; ++i, --j) {
	std::cout << "i: " << i << ", j: " << j << std::endl;
}
```

Kết quả ta nhận được trên màn hình là như sau

```bash
i: 0, j: 10
i: 1, j: 9
i: 2, j: 8
i: 3, j: 7
i: 4, j: 6
```

**Giải thích**
**Giá trị khởi tạo:** Trong phần đầu tiên của biểu thức điều khiển vòng lặp, chúng ta định nghĩa và khởi tạo hai biến i và j. Biến i được khởi tạo là 0 và biến j được khởi tạo là 10.
**Điều kiện dừng:** Điều kiện để tiếp tục vòng lặp là i < j. Vòng lặp sẽ tiếp tục chạy miễn là điều kiện này đúng.
**Biến nhảy của vòng lặp:** Trong phần cuối của biểu thức điều khiển vòng lặp, chúng ta tăng biến i lên 1 và giảm biến j xuống 1 sau mỗi lần lặp.

### 3. Range-Based For Loop

Bên cạnh việc sử dụng các vòng lặp cơ bản, chúng ta có thể sử dụng `range-based` loop để có thể dễ dàng duyệt qua tất các phần tử trong một mảng hay danh sách các phần tử nào đó.

Cấu trúc cơ bản của một `range-based` loop là 

```c++
for ([initialization;] range_declaration : range_expression){
	loop statement or block;
}
```

Dấu ngoặc vuông chỉ để tham khảo, và chúng chỉ ra rằng phần khởi tạo là tùy chọn. Câu lệnh khởi tạo trong vòng lặp for dựa trên phạm vi, ngoài việc nó là tùy chọn, hoàn toàn tương tự như vòng lặp for thông thường. Bạn có thể sử dụng nó để khởi tạo một hoặc nhiều biến mà bạn có thể sử dụng trong phần còn lại của vòng lặp for dựa trên phạm vi.

Đây là đoạn chương trình mô phỏng cho cách sử dụng của nó

```c++
#include <iostream>
#include <vector>
int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    for (int value : vec) {
        std::cout << value << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

**range_expression** xác định phạm vi là nguồn dữ liệu, và **range_declaration** xác định một biến sẽ được gán từng giá trị trong phạm vi này lần lượt, với một giá trị mới được gán trong mỗi lần lặp. Điều này sẽ rõ ràng hơn với một ví dụ. Hãy xem xét các câu lệnh sau:

```c++
int values [] {2, 3, 5, 7, 11, 13, 17, 19, 23, 29};
int total {};
for (int x : values){
	total += x;
}
```

Biến x sẽ được gán một giá trị từ mảng values trong mỗi lần lặp. Nó sẽ được gán các giá trị 2, 3, 5, và cứ tiếp tục như vậy. Do đó, vòng lặp sẽ tính tổng tất cả các phần tử trong mảng values vào biến total. Biến x là biến cục bộ trong vòng lặp và không tồn tại ngoài vòng lặp.

```c++
int total {};
for (int x : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29}){
	total += x;
}
```

Sử dụng từ khóa auto sẽ làm cho trình biên dịch suy luận ra kiểu đúng cho x. Từ khóa auto được sử dụng thường xuyên với vòng lặp for dựa trên phạm vi. Đây là một cách tốt để lặp qua tất cả các phần tử trong một mảng hoặc các loại phạm vi khác. Bạn không cần phải biết số lượng phần tử. Cơ chế vòng lặp sẽ lo liệu điều đó.

```c++
int total {};
for (auto x : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29}){
	total += x;
}
```
