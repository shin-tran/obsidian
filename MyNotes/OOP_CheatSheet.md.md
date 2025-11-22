# TỔNG HỢP KIẾN THỨC LẬP TRÌNH HƯỚNG ĐỐI TƯỢNG (OOP)
## I. KHÁI NIỆM CƠ BẢN (CORE CONCEPTS)
### 1. Lớp (Class) - "Khuôn mẫu"
- **Định nghĩa:** Là bản thiết kế (blueprint) hoặc khuôn mẫu để tạo ra đối tượng. Tập hợp các đối tượng có đặc tính tương tự nhau.
- **Đặc điểm:**
    - Trừu tượng hóa dữ liệu.
    - Không chiếm bộ nhớ khi chưa khởi tạo đối tượng.
- **Thành phần:**
    - **Thuộc tính (Attributes):** Biến lưu trữ trạng thái/dữ liệu. Có giá trị nhất định cho mỗi đối tượng tại mỗi thời điểm.
    - **Phương thức (Methods/Thao tác):** Hàm thể hiện hành vi/thao tác của đối tượng tác động qua lại với các đối tượng khác hoặc chính nó.
### 2. Đối tượng (Object) - "Thực thể"
- **Định nghĩa:** Là một thực thể cụ thể (instance) được tạo ra từ Class.
- **Đặc điểm:**
    - Có trạng thái (giá trị các thuộc tính) và hành vi riêng.
    - **Chiếm bộ nhớ** khi được khởi tạo.
### 3. Phạm vi truy cập (Access Modifiers)
- **`private`:** Chỉ nội bộ lớp và hàm bạn (friend) được truy cập. (Che giấu thông tin).
- **`protected`:** Nội bộ lớp + Lớp con kế thừa được truy cập.
- **`public`:** Truy xuất mọi nơi (Open interface).
## II. 4 TÍNH CHẤT TRỤ CỘT (THE 4 PILLARS)
### 1. Đóng gói (Encapsulation)
- **Ý nghĩa:** Gom dữ liệu và hàm vào một khối (Class).
- **Mục đích:** Che giấu thông tin quan trọng, tránh can thiệp trực tiếp sai lệch dữ liệu.
- **Triển khai:** Dữ liệu để `private`, thao tác qua `Getter` (lấy giá trị) và `Setter` (gán giá trị có kiểm tra).
### 2. Kế thừa (Inheritance)
- **Ý nghĩa:** Lớp con (Derived Class) thừa hưởng thuộc tính và phương thức từ lớp cha (Base Class).
- **Mục đích:** Tái sử dụng mã nguồn (Reusability), tránh viết lại code lặp, thể hiện quan hệ "IS-A" (Là một).
### 3. Đa hình (Polymorphism)
- **Ý nghĩa:** Một tên gọi (hàm) nhưng có nhiều hành vi khác nhau tùy ngữ cảnh.
- **Phân loại:**
    - **Compile-time (Lúc biên dịch):** Nạp chồng hàm (Overloading).
    - **Run-time (Lúc chạy):** Ghi đè hàm (Overriding) thông qua cơ chế Virtual Function.
### 4. Trừu tượng (Abstraction)
- **Ý nghĩa:** Ẩn đi chi tiết cài đặt phức tạp, chỉ cung cấp các tính năng cần thiết cho người dùng.
- **Triển khai:** Thông qua `Abstract Class` (Lớp trừu tượng) hoặc `Interface`.
## III. CÁC THÀNH PHẦN NÂNG CAO
### 1. Từ khóa đặc biệt (Keywords)
- **`static` (Tĩnh):**
    - _Biến static:_ Dùng chung bộ nhớ cho tất cả đối tượng của lớp (Biến của lớp, không phải biến của đối tượng).
    - _Hàm static:_ Gọi trực tiếp qua tên lớp \(`ClassName::Method()`\), không cần tạo đối tượng, chỉ được truy cập biến static.
- **`const` (Hằng):**
    - _Biến const:_ Giá trị không đổi sau khi khởi tạo.
    - _Hàm const:_ (`void func() const`) Cam kết không thay đổi bất kỳ thuộc tính nào của đối tượng khi gọi hàm này.
- **`this` pointer:**
    - Là con trỏ trỏ đến chính đối tượng đang thực thi phương thức đó. Giúp phân biệt tham số truyền vào và thuộc tính class nếu trùng tên.
- **`friend` (Bạn):**
    - _Hàm bạn (Friend Function):_ Hàm tự do nhưng được quyền truy cập `private` của lớp.
    - _Lớp bạn (Friend Class):_ Lớp này có thể truy cập thành phần `private` của lớp kia.
### 2. Các loại Constructor & Destructor (Nâng cao)
- **Constructor (Hàm tạo):** Tự động chạy khi khởi tạo đối tượng.
    - _Default Constructor:_ Không tham số.
    - _Parameterized Constructor:_ Có tham số (truyền giá trị khởi tạo).
    - _Copy Constructor (Quan trọng):_ Tạo một đối tượng mới bằng cách sao chép dữ liệu từ một đối tượng cũ (`Class A = B`). Cần lưu ý **Deep Copy** (cấp phát bộ nhớ mới) và **Shallow Copy** (sao chép địa chỉ con trỏ).
- **Destructor (Hàm hủy):** Dọn dẹp bộ nhớ trước khi đối tượng bị hủy.
- **Virtual Destructor (Hàm hủy ảo - Quan trọng):**
    - Khi dùng đa hình (con trỏ cha trỏ đối tượng con), nếu Destructor lớp cha KHÔNG `virtual`, thì Destructor lớp con sẽ KHÔNG được gọi -> Gây rò rỉ bộ nhớ (Memory Leak).
### 3. Quan hệ giữa các đối tượng (Object Relationships)
- **Inheritance (Kế thừa):** Quan hệ **IS-A** (Con chó _là một_ Động vật).
- **Association (Kết hợp):** Quan hệ lỏng lẻo, đối tượng này "sử dụng" hoặc "biết" đối tượng kia. (Giáo viên _biết_ Học sinh).
- **Aggregation (Tụ tập):** Quan hệ **HAS-A (Weak)**.
    - Một đối tượng chứa đối tượng khác.
    - Nếu đối tượng cha hủy, đối tượng con **VẪN TỒN TẠI**.
    - _Ví dụ:_ `Lớp học` và `Học sinh`. Hủy lớp học, học sinh vẫn còn đó.
- **Composition (Thành phần):** Quan hệ **HAS-A (Strong)**.
    - Một đối tượng được cấu thành từ các đối tượng khác.
    - Nếu đối tượng cha hủy, đối tượng con **BỊ HỦY THEO**.
    - _Ví dụ:_ `Nhà` và `Phòng`. Đập nhà thì phòng cũng mất.
### 4. Interface vs Abstract Class
- **Abstract Class (Lớp trừu tượng):**
    - Có thể chứa cả hàm bình thường (có code) và hàm thuần ảo (pure virtual).
    - Có thể chứa thuộc tính (biến).
    - Dùng khi các lớp con có chung bản chất và một số logic chung.
- **Interface (Giao diện):**
    - Trong C++, Interface là lớp **chỉ chứa các hàm thuần ảo** (`virtual void func() = 0;`) và hằng số.
    - Không chứa thuộc tính hay hàm đã cài đặt.
    - Dùng để quy định một bộ hành vi (behavior) mà các lớp không liên quan nhau phải tuân thủ (Giống như bản hợp đồng).
## IV. SO SÁNH QUAN TRỌNG (COMPARISON)
### Overload (Nạp chồng) vs. Override (Ghi đè)

| Đặc điểm    | Overload (Nạp chồng)                   | Override (Ghi đè)                                    |
| ----------- | -------------------------------------- | ---------------------------------------------------- |
| **Vị trí**  | Trong cùng một lớp (hoặc lớp kế thừa). | Xảy ra giữa Lớp Cha và Lớp Con.                      |
| **Tên hàm** | Giống nhau.                            | Giống nhau tuyệt đối.                                |
| **Tham số** | **KHÁC NHAU** (số lượng hoặc kiểu).    | **GIỐNG NHAU** tuyệt đối.                            |
| **Cơ chế**  | Đa hình lúc biên dịch (Compile-time).  | Đa hình lúc chạy (Run-time).                         |
| **Yêu cầu** | Không cần từ khóa `virtual`.           | Lớp cha phải có `virtual`, con có thể có `override`. |
## V. NGÂN HÀNG CÂU HỎI ÔN TẬP (Q&A) - TỪ TÀI LIỆU
**Câu 1: Phương pháp lập trình hướng đối tượng là gì?**
- Lấy đối tượng làm nền tảng để xây dựng thuật giải và chương trình.
- Dựa trên kiến trúc lớp (class) và đối tượng (object).
**Câu 2: Đối tượng là gì?**
- Là một phần tử, một thành viên cụ thể trong lớp.
**Câu 3: Lớp đối tượng là gì?**
- Tập hợp các đối tượng có đặc tính tương tự nhau. Đặc trưng bằng Thuộc tính và Thao tác.
**Câu 4: Các đặc điểm quan trọng của OOP?**
- 4 đặc điểm: Trừu tượng hóa, Đóng gói, Thừa kế, Đa hình.
**Câu 5: Phạm vi truy xuất gồm những gì?**
- Gồm 3 từ khóa: `public`, `private`, `protected` (Xem chi tiết mục I.3).
**Câu 6: Constructor là gì?**
- Là hàm thiết lập dùng để khởi tạo thể hiện của lớp và các giá trị thành phần. (Xem chi tiết mục III.1).
**Câu 7: Destructor là gì?**
- Là hàm hủy bỏ, dùng để dọn dẹp trước khi đối tượng bị hủy. Có dấu `~` trước tên.
**Câu 8: Kế thừa là gì?**
- Biểu diễn mối quan hệ đặc biệt hóa - tổng quát hóa.
- Cú pháp: `class LopCon : public LopCha { ... };`
**Câu 9: Quy tắc truy xuất trong Kế thừa?**
- _Quy tắc bảng:_
    - `Base` (protected) + Dẫn xuất `private` -> `Derived` (private).
    - `Base` (protected) + Dẫn xuất `protected` -> `Derived` (protected).
    - `Base` (protected) + Dẫn xuất `public` -> `Derived` (protected).
    - `Base` (public) + Dẫn xuất `private` -> `Derived` (private).
    - ... (Tóm lại: Quyền truy cập ở lớp con là sự kết hợp chặt chẽ nhất giữa quyền gốc và kiểu dẫn xuất).
**Câu 10: Phương thức ảo là gì? Lưu ý?**
- Là cách thể hiện đa hình trong C++.
- Lưu ý: Chỉ hoạt động qua con trỏ, nghi thức giao tiếp (tên, tham số, kiểu trả về) giữa cha và con phải **GIỐNG HỆT** nhau.
**Câu 11: Phương thức thuần ảo là gì?**
- Là phương thức ảo không có nội dung (`= 0`).
**Câu 12: Lớp trừu tượng là gì?**
- Là lớp cơ sở không có đối tượng nào thuộc chính nó (thường chứa hàm thuần ảo).
**Câu 13: Hàm friend?**
- Định nghĩa ngoài lớp, không phải hàm thành viên nhưng truy cập được private/protected.
**Câu 14: Thuộc tính là gì?**
- Những gì tạo nên đặc điểm của đối tượng.
**Câu 15: Phương thức là gì?**
- Những gì đối tượng có thể làm được (hành vi). Chỉ được gọi để tác động lên chính đối tượng đó.
**Câu 16: Copy Constructor?**
- Khởi tạo đối tượng bằng cách dùng đối tượng khác cùng lớp.
**Câu 17: Static và Non-static?**
- Static: Chung của lớp, tồn tại từ đầu đến cuối chương trình.
- Non-static: Riêng của đối tượng, ăn theo vòng đời đối tượng.