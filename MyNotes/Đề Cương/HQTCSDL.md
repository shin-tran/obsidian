## PHẦN 1: GIẢI ĐÁP THEO ĐỀ CƯƠNG (CƠ BẢN)
#### 1. Lý thuyết tổng quan (Câu 1)
- **CSDL (Database):** Là tập hợp các dữ liệu có cấu trúc, liên quan với nhau, được lưu trữ để phục vụ nhu cầu khai thác thông tin của nhiều người dùng.
- **Hệ QT CSDL (DBMS - Database Management System):** Là phần mềm giúp tạo, quản lý, bảo trì và khai thác CSDL (Ví dụ: MS SQL Server, MySQL).
- **Kiến trúc MS SQL Server:**
    - _External Level (Mức ngoài):_ Người dùng nhìn thấy dữ liệu qua View.
    - _Conceptual Level (Mức quan niệm):_ Cấu trúc logic toàn bộ dữ liệu (Bảng, quan hệ).
    - _Internal Level (Mức trong):_ Cách dữ liệu lưu trữ vật lý trên ổ cứng.
#### 2. Thao tác với Database (Câu 2)
- **Tạo CSDL:** `CREATE DATABASE Ten_CSDL;`
- **Sử dụng CSDL:** `USE Ten_CSDL;`
- **Xóa CSDL:** `DROP DATABASE Ten_CSDL;`
- **Sao lưu (Backup):**
```sql
BACKUP DATABASE Ten_CSDL TO DISK = 'D:\backup.bak';
```
- **Phục hồi (Restore):**
```sql
RESTORE DATABASE Ten_CSDL FROM DISK = 'D:\backup.bak';
```
#### 3. Thao tác với Bảng & Ràng buộc (Câu 3)
- **Tạo bảng (Create Table):**
```sql
CREATE TABLE SinhVien (
    MaSV CHAR(10) PRIMARY KEY, -- Khóa chính
    HoTen NVARCHAR(50) NOT NULL,
    Diem TB FLOAT CHECK (DiemTB >= 0 AND DiemTB <= 10), -- Ràng buộc miền giá trị
    MaLop CHAR(10) REFERENCES Lop(MaLop) -- Khóa ngoại
);
```
- **Sửa bảng (Alter Table):**
    - Thêm cột: `ALTER TABLE SinhVien ADD Email VARCHAR(50);`
    - Sửa kiểu dữ liệu: `ALTER TABLE SinhVien ALTER COLUMN Email VARCHAR(100);`
    - Thêm ràng buộc: `ALTER TABLE SinhVien ADD CONSTRAINT DF_Diem DEFAULT 0 FOR DiemTB;`
#### 4. Truy vấn & Cập nhật dữ liệu (Câu 4)
- **Thêm (Insert):** `INSERT INTO SinhVien (MaSV, HoTen) VALUES ('SV01', N'Nguyễn Văn A');`
- **Sửa (Update):** `UPDATE SinhVien SET DiemTB = 8 WHERE MaSV = 'SV01';`
- **Xóa (Delete):** `DELETE FROM SinhVien WHERE MaSV = 'SV01';`
- **Truy vấn (Select):**
```sql
SELECT * FROM SinhVien WHERE DiemTB > 5 ORDER BY DiemTB DESC;
```
#### 5. Lập trình T-SQL: Thủ tục & Hàm (Câu 5 - Trọng tâm 5 điểm)
- **Khai báo biến:** `DECLARE @bien INT; SET @bien = 10;`
- **Cấu trúc điều khiển:** `IF...ELSE`, `WHILE`.
- **Thủ tục (Stored Procedure):** Dùng để thực hiện một loạt hành động (Thêm, xóa, sửa).
```sql
CREATE PROC sp_ThemSV (@MaSV CHAR(10), @Ten NVARCHAR(50))
AS
BEGIN
    IF EXISTS (SELECT * FROM SinhVien WHERE MaSV = @MaSV)
        PRINT N'Mã đã tồn tại'
    ELSE
        INSERT INTO SinhVien(MaSV, HoTen) VALUES (@MaSV, @Ten)
END
```
- **Hàm (Function):** Dùng để tính toán và **phải trả về** giá trị (Scalar) hoặc bảng (Table).
```sql
CREATE FUNCTION fn_TinhTuoi (@NamSinh INT)
RETURNS INT
AS
BEGIN
    RETURN YEAR(GETDATE()) - @NamSinh
END
```

---
## PHẦN 2: KIẾN THỨC MỞ RỘNG (NÂNG CAO)
### 1. Sự khác biệt giữa DELETE và TRUNCATE
- `DELETE`: Xóa từng dòng, có thể phục hồi (rollback), có thể dùng WHERE. Chậm hơn.
- `TRUNCATE`: Xóa sạch dữ liệu bảng ngay lập tức, reset bộ đếm Identity, không dùng được WHERE. Rất nhanh nhưng nguy hiểm.
### 2. Các loại JOIN (Kết nối bảng)
- `INNER JOIN`: Chỉ lấy dữ liệu chung có ở 2 bảng.
- `LEFT JOIN`: Lấy hết bảng bên trái + dữ liệu chung (nếu bảng phải không có thì để NULL).
- `RIGHT JOIN`: Ngược lại với LEFT JOIN.
- _Mẹo:_ Khi đề bài yêu cầu "Liệt kê danh sách sinh viên **kể cả** những người chưa có điểm", hãy nghĩ ngay đến `LEFT JOIN`.
### 3. Hàm gộp (Aggregate Functions) & Group By
- Khi dùng `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` kèm với các cột khác, bắt buộc phải dùng `GROUP BY`.
- Điều kiện trên hàm gộp phải dùng `HAVING`, không dùng `WHERE`.
    - _Sai:_ `SELECT Lop, COUNT(*) FROM SV WHERE COUNT(*) > 50`
    - _Đúng:_ `SELECT Lop, COUNT(*) FROM SV GROUP BY Lop HAVING COUNT(*) > 50`
### 4. Dữ liệu Tiếng Việt (Unicode)
- Luôn dùng kiểu `NVARCHAR` hoặc `NCHAR`.
- Khi Insert/Update, phải có chữ **N** phía trước chuỗi. Ví dụ: `N'Nguyễn Văn A'`.
### 5. Trigger (Có thể xuất hiện ở câu nâng cao)
- Tự động chạy khi Insert/Update/Delete. Thường dùng để kiểm tra ràng buộc phức tạp mà `CHECK` không làm được (ví dụ: Điểm thi lần 2 phải lớn hơn lần 1).
- **Khái niệm:** Một dạng thủ tục đặc biệt tự động chạy khi có sự kiện `INSERT`, `UPDATE`, hoặc `DELETE`.
- **Bảng ảo (Magic Tables):** Chìa khóa để viết Trigger.
    - `inserted`: Chứa các dòng dữ liệu vừa được thêm vào hoặc sau khi sửa.
    - `deleted`: Chứa các dòng dữ liệu vừa bị xóa hoặc trước khi sửa.
- **Ví dụ:** _Không cho phép xóa sinh viên nếu sinh viên đó đã có điểm thi._
```sql
CREATE TRIGGER tg_KiemTraXoaSV
ON SinhVien
FOR DELETE
AS
BEGIN
    -- Nếu mã SV bị xóa có tồn tại trong bảng KetQua
    IF EXISTS (SELECT * FROM deleted d JOIN KetQua k ON d.MaSV = k.MaSV)
    BEGIN
        PRINT N'Sinh viên này đã có điểm, không được xóa!'
        ROLLBACK TRANSACTION -- Hủy bỏ thao tác xóa
    END
END
```
### 6. TRANSACTION (Giao dịch & An toàn dữ liệu)
- **Mục đích:** Đảm bảo một chuỗi hành động phải **thành công tất cả** hoặc **thất bại tất cả**.
- **Cấu trúc:**
```sql
BEGIN TRANSACTION
BEGIN TRY
    -- Các lệnh SQL thực hiện (Ví dụ: Trừ tiền A, Cộng tiền B)
    INSERT INTO...
    UPDATE...

    COMMIT TRANSACTION -- Nếu chạy ổn hết thì Lưu
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION -- Nếu có 1 lỗi bất kỳ thì quay lại từ đầu (Hoàn tác)
    PRINT N'Đã xảy ra lỗi'
END CATCH
```
### 7. CÁC KỸ THUẬT TRUY VẤN NÂNG CAO
**a. Truy vấn lồng (Subquery)**
Dùng khi kết quả của câu lệnh này là điều kiện đầu vào của câu lệnh kia.
- **Dạng `IN` / `NOT IN`:** Tìm sinh viên _chưa từng_ thi môn nào.
```sql
SELECT * FROM SinhVien 
WHERE MaSV NOT IN (SELECT DISTINCT MaSV FROM KetQua)
```
- **Dạng `EXISTS`:** Kiểm tra sự tồn tại (Thường nhanh hơn IN khi dữ liệu lớn).
**b. CTE (Common Table Expression)**
Giúp viết code trong sáng hơn, đặc biệt khi cần truy vấn đệ quy hoặc phân trang.
```sql
;WITH DiemTrungBinh AS (
    SELECT MaSV, AVG(Diem) as DTB FROM KetQua GROUP BY MaSV
)
SELECT * FROM DiemTrungBinh WHERE DTB >= 8.0
```
**c. Xử lý chuỗi và ngày tháng (Rất hay dùng trong báo cáo)**
- **Tách họ tên:** Dùng `SUBSTRING`, `CHARINDEX`, `LEN`, `REVERSE`.
    - _Ví dụ lấy tên (từ khoảng trắng cuối cùng):_ Logic phức tạp, nhưng nếu đề yêu cầu đơn giản thì dùng `LEFT`, `RIGHT`.
- **Tính toán ngày:**
    - `GETDATE()`: Lấy ngày giờ hiện tại.
    - `DATEDIFF(YEAR, NgaySinh, GETDATE())`: Tính tuổi.
    - `DATEADD(DAY, 7, NgayMuon)`: Tính ngày phải trả sách (cộng thêm 7 ngày).
### 8. KIẾN THỨC VỀ VIEW (KHUNG NHÌN)
- **Tác dụng:**
    - Bảo mật (Chỉ cho người dùng thấy cột cần thiết, giấu lương, thông tin nhạy cảm).
    - Đơn giản hóa câu truy vấn (Lưu câu SELECT phức tạp thành 1 bảng ảo).
- **Lưu ý:** View không lưu dữ liệu, nó chỉ lưu câu lệnh truy vấn.

---
## PHẦN 3: CHIẾN THUẬT LÀM BÀI (90 PHÚT)
1. **Xử lý Câu 5 trước hoặc dành nhiều thời gian nhất (5 điểm) :**
    - Đây là câu quyết định đậu rớt. Hãy viết khung sườn trước (`CREATE PROC... AS BEGIN... END`).
    - Nếu quên cú pháp logic phức tạp, hãy viết chú thích ý tưởng (comment) để giám khảo thấy tư duy logic, bạn vẫn có thể được chấm điểm thành phần.
2. **Đừng mất điểm oan ở Câu 1 (1 điểm):**
    - Học thuộc lòng khái niệm. Trả lời ngắn gọn, gạch đầu dòng, không viết lan man.
3. **Kiểm tra kỹ cú pháp Câu 2, 3, 4:**
    - Quên dấu phẩy `,` giữa các cột hoặc quên đóng ngoặc `)` là lỗi thường gặp nhất khiến bài viết tay bị trừ điểm oan uổng.
    - Kiểm tra logic khóa ngoại: Bảng chứa khóa chính phải được tạo trước, bảng chứa khóa ngoại tạo sau.
