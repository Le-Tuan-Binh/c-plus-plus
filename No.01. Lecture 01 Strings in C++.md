## Getting Started

Trong ngôn ngữ lập trình C++, `std::string` là một kiểu dữ liệu chuỗi được định nghĩa trong thư viện tiêu chuẩn `<string>`. Nó cung cấp một cách linh hoạt và an toàn hơn để làm việc với chuỗi so với chuỗi kiểu C truyền thống.

Trong bài viết này sẽ hướng dẫn bạn qua các bước cơ bản để sử dụng chuỗi trong C++, từ khởi tạo đến thao tác trên chuỗi, và một số kĩ thuật hiện đại với chuỗi.

## Getting Involved

### 1. Khai báo

Để sử dụng thư viện `string`, bạn cần include gói thư viện `string` vào chương trình của mình. Dưới đây là một số cách khai báo thường thấy trong quá trình sử dụng chuỗi.

#### 1.1 Khai báo chuỗi rỗng

```bash
string name_string;
```

#### 1.2 Khai báo chuỗi có giá trị ban đầu

```bash
string name_string {value}
```

#### 1.3 Khai báo chuỗi có giới hạn độ dài với giá trị ban đầu

```bash
string name_string {value,max_size};
```

#### 1.4 Khai báo chuỗi với số lần lặp của một kí tự nào đó

```bash
string name_string (loop_size,char);
```

Tuy nhiên bạn cần lưu với phương pháp khai báo chuỗi với số lần lặp của 1 kí tự nào đó ta cần chú ý những điều quan trọng sau

1. Giá trị value phải là kí tự

```c++
string name_string (6,’o’);
```

Với đoạn code bên trên ta có được giá trị hiển thị là

```bash
oooooo
```

2. Phải sử dụng cặp ngoặc `()`

```c++
string name_string {111,’z’};
```

Tuy nhiên với đoạn chương trình phía trên kết quả ta mong muốn là `111` chữ `z` tuy nhiên ta lại nhận được kết quả phía bên dưới

```bash
oz
```

Giải thích: Giá trị `111` trong bảng mã Asscii là `o`, nên lúc này `name_string` sẽ có 2 phần tử là `o` và `z`.

#### 1.5 Khai báo chuỗi từ một chuỗi khác

```c++
string name_string{other_String};
```

#### 1.6 Khai báo chuỗi từ một chuỗi khác từ vị trí start với number kí tự

```c++
string name_string {other_string,start,number}
```

Dưới đây là ví dụ cho cách hoạt động của việc khai báo từ một chuỗi khác với vị trí bắt đầu và số lượng kí tự của chuỗi mới.

![alt text](./images/image_01.png)
