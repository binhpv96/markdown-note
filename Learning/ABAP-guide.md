> *`ABAP là gì? `*
> *`ABAP là ngôn ngữ lập trình của SAP`*

<br>

### 📌 LESSON 1 - Basic Syntax

👉 **ABAP data type**: kiểu dữ liệu được chia thành 2 loại `dữ liệu nguyên thủy (Elementary Data Types)` và `dữ liệu phức tạp (Complex Data Types)`.
<br>
   - Elementary Data Types
     | Loại | Kich Thước| Description | 
     | ----------- | ----------- | ----------- |
     | **`C`** ( character ) | 1 - 65535 | chuỗi kí tự có độ dài cố định |
     | **`N`** ( numeric text ) | 1 - 65535 | chứa số nhưng ở dạng văn bản (không tính toán được) |
     | **`D`** ( date ) | 8 | lưu trữ ngày (YYYYMMDD) |
     | **`T`** ( time ) | 6 | lưu trữ thời gian (HHMMSS) |
     | **`I`** ( integer ) | 4 | lưu trữ số nguyên |
     | **`F`** ( floating point ) | 8 | số thực dấu chấm động |
     | **`P`** ( packed number - DEC ) | 1 - 16 | dùng cho số thập phân (số tiền, phép toán chính xác) |
     | **`X`** ( hexadecimal ) | 1 - 65535 | chuỗi nhị phân (hex) |

   - Complex Data Types
     | Loại | Description | 
     | ----------- | ----------- |
     | **`Structure`** | nhóm các kiểu dữ liệu khác nhau |
     | **`Table`**  | một bảng chứa nhiều dòng dữ liệu có cùng cấu trúc | 
     | **`Internal Table`** | bảng nội bộ được lưu trong bộ nhớ, hỗ trợ xử lý dữ liệu linh hoạt |
     | **`Object`** | Dùng trong lập trình OOP của ABAP | 

<br>

👉 **Write with position, length?**
`WRITE` là lệnh để hiện thị dữ liệu, tương tự `Sout` trong Java
có thể chỉ định vị trí xuất hiện bằng `AT` và độ dài bằng `LENGTH`
💡Ví dụ: 
 > `WRITE 'Việt Nam vô địch' AT 3 LENGTH 10`

<br>

- **Khai báo biến**
    > `DATA a TYPE I VALUE 5`

<br>

- **Message output for report**
`MESSAGE` được dùng để hiển thị thông báo trong trương trình
Cú pháp: 
    > `MESSAGE 'lỗi kiểu dữ liệu' TYPE 'E'.` 

    Có các type như `I (information)`, `W (warning)`, `E (error)`, `S (success)` và `A (dừng chương trình)` 

<br>

👉 **Text Symbols**
    Được định nghĩa trong `Text Elements` và giúp quản lý đa ngôn ngữ
    💡Ví dụ: 
 > `WRITE TEXT-001`

<br>

👉 **Date and Time Calculator**
 > `DATA today TYPE D.`
 > `today = SY-DATUM.`
 >
 > `DATA now TYPE T.`
 > `now = SY-UZEIT.`
 >
 > `DATA tomorrow TYPE D.`
 > `tommorrow = SY-DATUM + 1.`

🌐[Video Basic Syntax - Part 1](https://youtu.be/gQmSwrn53gE)
<br>

👉 **If - Else**
Cú pháp:
> `IF a > 10.`
> `WRITE 'input > 10'.`
> `ELSE IF a = 10.`
> `WRITE input = 10.`
> `ELSE.`
> `WRITE input < 10.`
> `ENDIF.`

<br>

👉 **Loop**
- LOOP . . . AT ( lặp qua bảng nội bộ )
    > `DATA: lt_numbers TYPE TABLE OF I,`
    >  `wa_number  TYPE I.`
    >
    > `APPEND 10 TO lt_numbers.`
    > `APPEND 20 TO lt_numbers.`
    > `APPEND 30 TO lt_numbers.`
    >
    > `LOOP AT lt_numbers INTO wa_number.`
    > `ENDLOOP.`

- DO . . . ENDDO
    > `DO 5 TIMES.`
    > `WRITE 'Đã lặp'.`
    > `ENDDO.`

- WHILE . . . ENDWHILE
    > `WHILE count < 5.`
    > `WRITE 'giá trị: ', count.`
    > `count = count - 1.`
    > `ENDWHILE.`

<br>

👉 **Selection-screen (cơ bản)**
`SELECTION-SCREEN` giúp tạo giao diện nhận dữ liệu
> `PARAMETERS: p_name TYPE STRING,`
> `p_age TYPE I.`

🌐[Video Basic Syntax - Part 2](https://youtu.be/HbCroU8FODU)

<br>

> ***Transaction code***
> - SE38 create / change / display ABAP program
> - SE11 to open ABAP dictionary and create table / view / data elements / domains
> - SE91 to open Message Class

### 📌 LESSON 2 - Data Dictionary

👉 **What is data dictionary?**
Data dictionary giúp quản lí dữ liệu trong SAP. Nó cung cấp các đối tượng dữ liệu như `Table`, `View`, `Data Elements`, `Domains`, . . . mà không cần thao tác trực tiếp với hệ quản trị cơ sở dữ liệu ( DBMS ).

<br>

👉 **1. Domains**
- Xác định kiểu dữ liệu, độ dài, giá trị hợp lệ ( value range ) cho một trường
- Một domain có thể được dùng bởi nhiều `data elements` khác nhau
💡Ví dụ: Domain `DOM_CURENCY` có kiểu dữ liệu `CHAR (3)` dùng để lưu các mã tiền tệ (VND, EUR, USD, ...)

<br>

👉 **2. Data Elements**
- Là định nghĩa một trường dữ liệu dựa trên domain.
- Chứa mô tả ( short text ) và có thể gán vào các trường trong bảng.
💡Ví dụ: `DE_CURRENCY` dùng domain `DOM_CURRENCY`.

<br>

👉 **3. Table**
- Đây là đối tượng quan trọng nhất của Data Dictionary
- `Transparent table` là bảng thông dụng nhất, lưu dữ liệu trực tiếp vào bảng vật lý trong CSDL.
- `Pooled Table & Cluster Table` (chả ma nào dùng).

<br>

👉 **4. Views**
- Dùng để xem dữ liệu từ 1 hoặc nhiều bảng gộp lại 1 lần (mà không lưu dữ liệu vật lý)
- Có 4 loại: 
`Database View`: tương tự JOIN trong SQL Sever
`Protection View`: lọc bớt cột của một bảng
`Help View`: hỗ trợ tìm kiếm dữ liệu
`Maintenance`: chỉnh sửa dữ liệu trong giao diện SAP

<br>

👉 **5. Types**
- Giúp định nghĩa kiểu dữ liệu có thể tái sử dụng
- Gồm các loại: `Structure ( STRUC )`, `Table Type ( TTYP )`, `Data Type ( DTEL )` và `Domain (  DOMA )`.
💡Ví dụ 
    > `TYPES: ty_amount TYPE p DECIMALS 2.`
    > `DATA: lv_total TYPE ty_amount.`

### 📌 LESSON 3 - ABAP Open SQL

👉 **What is Open SQL**

 | Tiêu chí | Open SQL | Native SQL | 
 | ----------- | ----------- | ----------- |
 | **`Định nghĩa`** | Tập hợp các lệnh SQL chuẩn của SAP để thao tác với CSDL trong môi trường ABAP | Lệnh SQL thuần ( thuộc DBMS ) có thể gọi trực tiếp từ ABAP |
 | **`Tính độc lập với DBMS`** | Hoạt động trên mọi hệ DBMS mà SAP hỗ trợ | Phụ thuộc vào từng DBMS riêng (`Oracle`, `MSSQL`, . . .) |
 | **`Tối ưu hóa hiệu suất`** | SAP tự động tối ưu hóa + chuyển đổi SQL phù hợp với DBMS | Không tự động tối ưu hóa |
 | **`Dễ sử dụng`** | Cú pháp đơn giản | Phức tạp, cần viết đúng cú pháp của từng loại DBMS |
 | **`Hỗ trợ các lệnh SQL`** | Không hỗ trợ các lệnh như `JOIN` phức tạp, `GROUP BY`, `ORDER BY` | Hỗ trợ tất cả |
 | **`Truy vấn các bảng ngoài SAP Dictionary`** | Không | Truy cập tất cả bảng trong DBMS, kể cả bảng không thuộc SAP |
 | **`Duy trì hệ thống`** | Dễ bảo trì, thể chuyển đổi giữa các DBMS mà không cần sửa code | Muốn đổi DBMS phải sửa toàn bộ Native SQL |

___

### 📌 LESSON 4 - Internal table

👉 **Internal Table và Work Area ( Structure )**

 | Tiêu chí | Work Area | Internal Table | 
 | ----------- | ----------- | ----------- |
 | **`Dữ liệu chứa`** | Chỉ chứa 1 dòng tại 1 thời điểm | Chứa nhiều dòng |
 | **`Sử dụng khi`** | Cần thao tác trên từng dòng | Cần thao tác, lưu trữ nhiều dòng dữ liệu |
 
<br>

👉 **How to create Work Area**

1. Khai báo Work Area từ một bảng dữ liệu
> `DATA wa_ak1 TYPE ak1. "Khai báo Work Area theo cấu trúc bảng AK1`
2.  Khai báo Work Area từ một cấu trúc dữ liệu ( Structure )
> `DATA wa_custom TYPE zcustom_struct. "Work Area theo cấu trúc tự định nghĩa`
3. Khai báo Work Area từ Internal Table
> `DATA: it_kna1 TYPE TABLE OF kna1,`
> `wa_kna1 TYPE kna1.`


👉 **SELECT INTO Internal Table và SELECT INTO Work Area**

| Tiêu chí | SELECT INTO Internal Table | SELECT INTO Work Area |
| ---------| ---------------------------| ----------------------|
| Cách lưu | Lưu nhiều dòng vào Internal Table | Lưu từng dòng vào Work Area |
| Hiệu suất | Nhanh hơn khi cần lưu nhiều dòng cùng một lúc | Chậm hơn nếu dữ liệu lớn vì phải lặp nhiều lần |
| Cách dùng | Phù hợp khi cần duyệt qua nhiều dòng sau khi truy vấn | Phù hợp khi chỉ lấy 1 dòng hoặc xử lý từng dòng sau khi truy vấn |
| Sử dụng với `LOOP AT` | Có thể duyệt qua toàn bộ bảng nội bộ | Không được dùng trực tiếp, phải đọc từng dòng riêng lẻ |

<br>

👉 **Move data between 2 Work Area**

> `MOVE-CORRESPONDING wa_1 TO wa_2.`

👉 **What is HEADER LINE?**
- Is a special Work Area
- Đóng vai trò như một Work Area đi kèm với Internal Table 
➡️ Tốt nhất không nên dùng Header line vì nó có cùng tên với internal table -> rất dễ nhầm và các lệnh cũng không phân biệt được là đang tương tác với `Work Area` hay `INTERNAL TABLE`