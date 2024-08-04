## Getting Started

**Vòng lặp for**: là một cơ chế cho phép bạn thực thi một câu lệnh hay một khối lệnh lặp đi lặp lại cho đến khi một điều kiện nào đó thõa mãn.

Một cấu trúc vòng lặp cơ bản bao gồm 2 thành phần chính

- Các câu lệnh và khối câu lệnh được thực hiện lặp đi lặp lại.

- Điều kiện dừng của vòng lặp, các giá trị khởi tạo và biến tăng của vòng lặp.

## Getting Involved

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


