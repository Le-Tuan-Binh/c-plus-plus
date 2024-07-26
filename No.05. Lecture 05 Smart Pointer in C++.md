## Getting Started

**Smart pointer** (con trỏ thông minh) là một khái niệm trong C++ giúp quản lý bộ nhớ tự động và ngăn chặn rò rỉ bộ nhớ. 

Smart pointer cung cấp khả năng quản lý vòng đời của đối tượng mà chúng sở hữu thông qua các cơ chế tự động giải phóng bộ nhớ khi đối tượng không còn được sử dụng.

## Getting Involved

### 1. Tại Sao Cần Sử Dụng Smart Pointer?

Trong C++, việc quản lý bộ nhớ bằng tay thông qua con trỏ thô (raw pointer) thường dẫn đến các vấn đề như:

- **Rò rỉ bộ nhớ**: Khi bộ nhớ được cấp phát nhưng không được giải phóng đúng cách.
- **Sử dụng con trỏ không hợp lệ**: Khi con trỏ trỏ đến vùng nhớ đã bị giải phóng.
- **Quản lý vòng đời đối tượng phức tạp**: Đặc biệt khi có nhiều con trỏ cùng trỏ đến một đối tượng.

Smart pointer giải quyết những vấn đề này bằng cách tự động giải phóng bộ nhớ khi nó không còn được sử dụng.

### 2. Reference-counted smart pointer

**std::shared_ptr** là một loại smart pointer sử dụng cơ chế đếm tham chiếu để quản lý vòng đời của đối tượng. Nó cho phép nhiều con trỏ cùng sở hữu một đối tượng và tự động giải phóng bộ nhớ khi không còn bất kỳ con trỏ nào trỏ đến đối tượng đó.

**std::shared_ptr** duy trì một **bộ đếm tham chiếu** (reference count) để theo dõi số lượng con trỏ cùng trỏ đến đối tượng. Mỗi khi một std::shared_ptr mới được tạo và trỏ đến cùng một đối tượng, bộ đếm tham chiếu tăng lên. Khi một std::shared_ptr bị hủy, bộ đếm tham chiếu giảm đi. Khi bộ đếm tham chiếu bằng 0, đối tượng được giải phóng.

### 3. std::unique_ptr

**std::unique_ptr** là smart pointer sở hữu duy nhất một đối tượng. Nó đảm bảo rằng chỉ có một con trỏ duy nhất trỏ đến đối tượng tại một thời điểm.

```c++
#include <iostream>
#include <memory>
int main() {
    std::unique_ptr<int> ptr = std::make_unique<int>(10);
    std::cout << "Value: " << *ptr << std::endl;
} 
```

### 4. std::shared_ptr

**std::shared_ptr** là smart pointer cho phép nhiều con trỏ cùng sở hữu một đối tượng. Nó sử dụng đếm tham chiếu để quản lý vòng đời đối tượng và tự động giải phóng bộ nhớ khi không còn con trỏ nào trỏ đến đối tượng đó.

```c++
#include <iostream>
#include <memory>
int main() {
    std::shared_ptr<int> ptr1 = std::make_shared<int>(20);
    std::shared_ptr<int> ptr2 = ptr1; 
    std::cout << "Value: " << *ptr1 << std::endl;
    std::cout << "Use count: " << ptr1.use_count() << std::endl;
} 
```

### 5. std::weak_ptr

**std::weak_ptr** là smart pointer không sở hữu đối tượng mà nó trỏ đến, mà chỉ giữ một tham chiếu yếu đến đối tượng đó. Nó thường được sử dụng để phá vỡ vòng tham chiếu (circular reference) khi sử dụng std::shared_ptr.

Đôi lúc chúng ta chỉ muốn truy cập vào đối tượng cơ bản của shared_ptr mà không làm tăng số lượng tham chiếu thì `weak_ptr` là một trong những sự lựa chọn tốt.

```c++
#include <iostream>
#include <memory>
int main() {
    std::shared_ptr<int> sharedPtr = std::make_shared<int>(30);
    std::weak_ptr<int> weakPtr = sharedPtr; 
    if (auto tempPtr = weakPtr.lock()) {không
        std::cout << "Value: " << *tempPtr << std::endl;
    } else {
        std::cout << "Object no longer exists." << std::endl;
    }
}
```