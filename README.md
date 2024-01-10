# redis-learning

## 1. What is Redis?

Redis là một open-source, cấu trúc dữ liệu lưu trữ in-memory và được sử dụng như một database, caching, message broker hoặc streaming engine.

## 2. Redis data types

### 2.1. Strings

- Redis strings lưu trữ các chuỗi bytes, bao gồm text, serialized objects, và binary arrays. Thường được sử dụng để caching, ngoài ra nó cũng được bổ sung các hàm để triển khai bộ đếm (counter) và các phép toán bitwise.
- Theo mặc định, một Redis string có thế lưu trữ tối đa 512MB
- Some commands:
  - **SET** và **GET**
  - **INCR**, **INCRBY**, **DECR** và **DECRBY**: dùng để tăng giảm giá trị nguyên (increment)

### 2.2 List

- Redis list là các **Linked List** của các giá trị string. Thường được sử dụng để:
  - Thực thi các stack và queue
  - Xây dựng hệ thống queue management cho background worker systems
- The max length of a Redis list is 2^32 - 1 (4,294,967,295) elements.
- Some commands:
  - **LPUSH**, **RPUSH**: thêm một hoặc nhiều phần tử vào bên trái (đầu) hoặc bên phải (cuối) của list
  - **LPOP**, **RPOP**: lấy một và loại bỏ nó từ bên trái (đầu) hoặc bên phải (cuối) của list
  - **LRANGE**: trích xuất các phần tử từ danh sách theo một phạm vi
  - **LTRIM**: trích xuất các phần tử tương tự như **LRANGE**. tuy nhiên, lệnh này sẽ đặt các phần tử này làm giá trị mới cho list và tất cả các phần tử nằm ngoài phạm vi sẽ được loại bỏ.
  - **BRPOP**, **BLPOP**: phiên bản blocking của **LPOP**, **RPOP**. Tức là nó sẽ chặn connection cho đến khi list không còn empty.
  - **LLEN**: trả về số phần tử của list
