Cookie Session Authentication - POSTMAN TEST

## Cách chạy

```bash
node app.js
```

---

### PHẦN 1: USER REGISTRATION TEST

**Bước 1: Test đăng ký user mới**  
**Method:** `POST`  
**URL:** `http://localhost:3000/auth/register`  
**Headers:** `Content-Type: application/json`  
**Body (raw JSON):**
```json
{
    "username": "testuser",
    "password": "testpass123"
}
```
**Kết quả:** User registered successfully!  
**Status:** 200  
![alt text](public/img/1.png)  
![alt text](public/img/m1.png)

**Bước 2: Test đăng ký user đã tồn tại**  
**Method:** `POST`  
**URL:** `http://localhost:3000/auth/register`  
**Headers:** `Content-Type: application/json`  
**Body (raw JSON):**
```json
{
    "username": "testuser",
    "password": "anypass"
}
```
**Kết quả:** User registration failed  
**Status:** 400  
![alt text](public/img/2.png)

---

### PHẦN 2: LOGIN TEST

**Bước 3: Test login sai username**  
**Method:** `POST`  
**URL:** `http://localhost:3000/auth/login`  
**Headers:** `Content-Type: application/json`  
**Body (raw JSON):**
```json
{
    "username": "wronguser",
    "password": "testpass123"
}
```
**Kết quả:** Invalid username or password  
**Status:** 400  
![alt text](public/img/3.png)

**Bước 4: Test login sai password**  
**Method:** `POST`  
**URL:** `http://localhost:3000/auth/login`  
**Headers:** `Content-Type: application/json`  
**Body (raw JSON):**
```json
{
    "username": "testuser",
    "password": "wrongpass"
}
```
**Kết quả:** Invalid username or password  
**Status:** 400  
![alt text](public/img/4.png)

**Bước 5: Test login đúng credentials**  
**Method:** `POST`  
**URL:** `http://localhost:3000/auth/login`  
**Headers:** `Content-Type: application/json`  
**Body (raw JSON):**
```json
{
    "username": "testuser",
    "password": "testpass123"
}
```
**Kết quả:** Login successful!  
**Status:** 200  
**CHÚ Ý:** Postman tự động lưu session cookie `connect.sid`  
![alt text](public/img/5.png)  
![alt text](public/img/m2.png)

**Bước 6: Kiểm tra session cookie**  
Vào tab Cookies trong Postman  
Tìm cookie `connect.sid`  
Xem giá trị session ID  
![alt text](public/img/6.png)

---

### PHẦN 3: PROTECTED ROUTE TEST

**Bước 7: Test profile route không có session**  
Mở Postman tab/window mới (hoặc xóa cookies)  
**Method:** `GET`  
**URL:** `http://localhost:3000/auth/profile`  
**Kết quả:** Unauthorized  
**Status:** 401  
![alt text](public/img/7.png)

**Bước 8: Test profile route có session hợp lệ**  
**Method:** `GET`  
**URL:** `http://localhost:3000/auth/profile`  
**CHÚ Ý:** Dùng tab đã login ở Bước 5  
**Kết quả:** Thông tin user (không có password)  
**Status:** 200  
![alt text](public/img/8.png)

---

### PHẦN 4: LOGOUT TEST

**Bước 9: Test logout**  
**Method:** `GET`  
**URL:** `http://localhost:3000/auth/logout`  
**Kết quả:** Logout successful!  
**Status:** 200  
**CHÚ Ý:** Session và cookie bị xóa  
![alt text](public/img/9.png)

**Bước 10: Test profile sau khi logout**  
**Method:** `GET`  
**URL:** `http://localhost:3000/auth/profile`  
**Kết quả:** Unauthorized  
**Status:** 401  
![alt text](public/img/10.png)  
![alt text](public/img/m3.png)

