## Getting Started

Trong C++, `con trỏ` và `hằng số` là những khái niệm cơ bản, và khi kết hợp chúng lại, ta có hai cấu trúc quan trọng: con trỏ hằng (**const pointer**) và hằng con trỏ (**pointer const**). Hiểu rõ sự khác biệt giữa chúng là điều quan trọng để viết mã nguồn mạnh mẽ và không có lỗi.

## Getting Involved

### 1. Const Pointer - Con trỏ hằng

Một con trỏ hằng là một con trỏ trỏ tới một giá trị hằng. Điều này có nghĩa là giá trị mà con trỏ trỏ tới không thể bị thay đổi thông qua con trỏ đó.

Cú pháp của một con trỏ hằng

    const data_type *ptr;

**Giải thích:**

- `const int* ptr` nghĩa là ptr là một **con trỏ** trỏ tới một **const int**.

- Bạn **có thể thay đổi địa chỉ** mà ptr trỏ tới, nhưng **không thể thay đổi giá trị** tại địa chỉ mà ptr trỏ tới.

```c++
#include <iostream>
int main() {
    int value1 = 10;
    int value2 = 20;
    const int *ptr = &value1;
    // *ptr = 30;
	// --> Error: Không thể thay đổi giá trị nó đang trỏ tới
    ptr = &value2;
    std::cout << *ptr << std::endl;
    return 0;
}
```

### 2. Pointer Const - Hằng con trỏ

Một hằng con trỏ, hay thường được gọi là `const pointer`, là một con trỏ mà **giá trị của nó (địa chỉ nó giữ)** không thể thay đổi sau khi khởi tạo.

Điều này có nghĩa là con trỏ sẽ luôn trỏ tới cùng một địa chỉ, nhưng **giá trị tại địa chỉ đó có thể thay đổi**.

Cú pháp của hằng con trỏ

    data_type *const ptr;

**Giải thích:**

- `int *const ptr` nghĩa là ptr là một `hằng con trỏ` trỏ tới một `int`.
- Bạn có thể thay đổi giá trị tại địa chỉ mà ptr trỏ tới, nhưng không thể thay đổi địa chỉ mà ptr trỏ tới.

```c++
#include <iostream>
int main() {
    int value1 = 10;
    int value2 = 20;
    int *const ptr = &value1;
    *ptr = 30;
    std::cout << *ptr << std::endl;
    // ptr = &value2;
	// --> Error: không thể thay đổi địa chỉ mà ptr trỏ tới
    return 0;
}
```

### 3. Const Pointer to Const - Hằng Con Trỏ Trỏ Tới Hằng

Một hằng con trỏ trỏ tới hằng kết hợp cả hai khái niệm trên: địa chỉ của con trỏ và giá trị tại địa chỉ đó đều không thể thay đổi.

Cú pháp của hằng con trỏ tới con trỏ hằng

    const data_type *const ptr;

**Giải thích:**

- `const int *const ptr` nghĩa là ptr là một hằng con trỏ trỏ tới một const int.
- Bạn không thể thay đổi địa chỉ mà ptr trỏ tới, và cũng không thể thay đổi giá trị tại địa chỉ đó.

```c++
#include <iostream>
int main() {
    int value1 = 10;
    const int *const ptr = &value1; 
    std::cout << *ptr << std::endl; 
    // *ptr = 30;
	// --> Error: không thể thay đổi giá trị của một const int
    // ptr = &value2;
	// --> Error: không thể thay đổi địa chỉ mà ptr trỏ tới
    return 0;
}
```
