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

### 2.2. Lists

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

### 2.3. Sets

- Redis set là một tập hợp các unique string không có thứ tự. Có thể sử dụng set để:
- The max size of a Redis set is 2^32 - 1 (4,294,967,295) members.
- Some commands:
  - **SADD** adds a new member to a set.
  - **SREM** removes the specified member from the set.
  - **SISMEMBER**: kiểm tra xem 1 chuỗi có phải là phần tử của set hay không.
  - **SINTER**: trả về một tập hợp các phần tử có chung ở 2 hoặc nhiều set.
  - **SDIFF**: trả về tập hợp các phần tử riêng nhất từ 2 hay nhiều set.
  - **SCARD**: trả về số phần tử của một set.
  - **SUNION**: trả về tập hợp hợp nhất từ 2 hay nhiều set.

### 2.4. Hashes

- Redis hash là loại bản ghi được cấu trúc dưới dạng tập hợp các cặp field-value. Nó có thể được dùng để đại diện cho một basic object hoặc lưu giữ một nhóm các bộ đếm (counter) và nhiều thứ khác.
- Every hash can store up to 4,294,967,295 (2^32 - 1) field-value pairs.
- Some commands:
  - **HSET**, **HGET**
  - **HINCRBY**: Increment giá trị integer của một field trong một hash bởi một số integer. Dùng giá trị 0 để khởi tạo nếu field không tồn tại.
  - **HLEN**: trả về số field của hash
  - **HKEYS**: trả về toàn bộ fields của hash
  - **HEXISTS**: kiểm tra xem 1 field có tồn tại trong hash ko
  - **HVALS**: trả về toàn bộ value trong hash 

### 2.5. Sorted sets

- Sorted set là tập hợp các unique strings được sắp xếp theo thứ tự liên quan để điểm. Khi có nhiều string có cùng số điểm (score) thì sẽ được sắp xếp theo thứ tự từ điển.
- Các trường hợp sử dụng sorted set như:
  - Leaderboards.
  - Rate limits
- Sorted set có thể được coi là được mix giữa **Sets** và **Hashes**. Nó giống với **Sets** bởi vì đều lưu trữ unique string và giống với **Hashes** bởi vì mỗi value trong **Sorted sets** đều được ánh xạ với một **score**.
