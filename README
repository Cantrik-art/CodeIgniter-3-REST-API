# CodeIgniter 3 REST API dengan chriskacerguis/RestServer

Proyek ini adalah implementasi REST API di CodeIgniter 3 menggunakan pustaka `chriskacerguis/RestServer`. API ini mendukung operasi CRUD (Create, Read, Update, Delete) untuk entitas `users`.

---

## 🚀 Instalasi dan Penyiapan

### 1. **Kloning Repository**
```sh
 git clone <repo_url>
 cd <repo_folder>
```

### 2. **Instalasi chriskacerguis/RestServer**
#### a) Jika menggunakan Composer (Direkomendasikan)
```sh
composer require chriskacerguis/codeigniter-restserver
```
Pastikan autoload Composer diaktifkan dalam `application/config/config.php`:
```php
$config['composer_autoload'] = TRUE;
```

#### b) Jika Tanpa Composer (Manual Install)
1. **Download dari GitHub:** [chriskacerguis/codeigniter-restserver](https://github.com/chriskacerguis/codeigniter-restserver)
2. **Pindahkan file ke `application/libraries/`**:
   - `REST_Controller.php`
   - `Format.php`
3. **Pastikan namespace dalam `REST_Controller.php`**:
   ```php
   namespace chriskacerguis\RestServer;
   ```

### 3. **Buat Controller API**
Buat file **`application/controllers/Api.php`**:
```php
<?php
namespace App\Controllers;

use chriskacerguis\RestServer\RestController;

class Api extends RestController {
    
    public function __construct() {
        parent::__construct();
        $this->load->database();
    }

    public function users_get() {
        $users = $this->db->get('users')->result();
        $this->response($users, 200);
    }

    public function user_get($id) {
        $user = $this->db->get_where('users', ['id' => $id])->row();
        if ($user) {
            $this->response($user, 200);
        } else {
            $this->response(['message' => 'User not found'], 404);
        }
    }

    public function user_post() {
        $data = [
            'name' => $this->post('name'),
            'email' => $this->post('email'),
            'password' => password_hash($this->post('password'), PASSWORD_BCRYPT)
        ];
        $this->db->insert('users', $data);
        $this->response(['message' => 'User created'], 201);
    }

    public function user_put($id) {
        $data = [
            'name' => $this->put('name'),
            'email' => $this->put('email')
        ];
        $this->db->where('id', $id)->update('users', $data);
        $this->response(['message' => 'User updated'], 200);
    }

    public function user_delete($id) {
        $this->db->delete('users', ['id' => $id]);
        $this->response(['message' => 'User deleted'], 200);
    }
}
```

### 4. **Konfigurasi Routes**
Tambahkan di `application/config/routes.php`:
```php
$route['api/users']['GET'] = 'api/users_get';
$route['api/user/(:num)']['GET'] = 'api/user_get/$1';
$route['api/user']['POST'] = 'api/user_post';
$route['api/user/(:num)']['PUT'] = 'api/user_put/$1';
$route['api/user/(:num)']['DELETE'] = 'api/user_delete/$1';
```

---

## 📌 Cara Menggunakan API

### **1. GET Semua User**
```http
GET /api/users
```
**Response:**
```json
[
    {"id": 1, "name": "John Doe", "email": "john@example.com"},
    {"id": 2, "name": "Jane Doe", "email": "jane@example.com"}
]
```

### **2. GET User berdasarkan ID**
```http
GET /api/user/1
```
**Response:**
```json
{"id": 1, "name": "John Doe", "email": "john@example.com"}
```

### **3. POST Tambah User Baru**
```http
POST /api/user
```
**Body (JSON):**
```json
{
    "name": "Alice",
    "email": "alice@example.com",
    "password": "password123"
}
```
**Response:**
```json
{"message": "User created"}
```

### **4. PUT Update Data User**
```http
PUT /api/user/1
```
**Body (JSON):**
```json
{
    "name": "John Updated",
    "email": "john.updated@example.com"
}
```
**Response:**
```json
{"message": "User updated"}
```

### **5. DELETE Hapus User**
```http
DELETE /api/user/1
```
**Response:**
```json
{"message": "User deleted"}
```

---

## 🛠 Debugging
Jika API tidak berfungsi, cek langkah-langkah berikut:
1. **Pastikan Composer Autoload diaktifkan**
   ```php
   $config['composer_autoload'] = TRUE;
   ```
2. **Cek namespace di `REST_Controller.php`**:
   ```php
   namespace chriskacerguis\RestServer;
   ```
3. **Aktifkan error reporting di `index.php`**:
   ```php
   error_reporting(E_ALL);
   ini_set('display_errors', 1);
   ```
4. **Pastikan database sudah dibuat dan koneksi berhasil**
5. **Jika masih error, coba jalankan perintah berikut:**
   ```sh
   composer dump-autoload
   ```

---

## 📜 Lisensi
Proyek ini menggunakan lisensi **MIT License**.

---

**🎯 Selamat Membuat API dengan CodeIgniter 3! 🚀**

