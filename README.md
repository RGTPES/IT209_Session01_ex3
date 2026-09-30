# Hướng dẫn Cài đặt Nginx & Cấu hình Website Tĩnh (Session 02 - Ex3)

## 1. Cập nhật hệ thống & Cài đặt Nginx
```bash
sudo apt update
sudo apt install -y nginx
```

Kiểm tra trạng thái Nginx:
```bash
sudo systemctl status nginx
```

## 2. Tạo thư mục chứa mã nguồn tĩnh & file index.html
Tạo thư mục website:
```bash
sudo mkdir -p /var/www/ptit-web/html
```

Phân quyền cho thư mục:
```bash
sudo chown -R $USER:$USER /var/www/ptit-web/html
sudo chmod -R 755 /var/www/ptit-web
```

Tạo file `index.html`:
```bash
sudo nano /var/www/ptit-web/html/index.html
```
*(Hoặc copy nội dung từ file `index.html` trong thư mục bài tập này)*

## 3. Tạo cấu hình Server Block cho website
Tạo file cấu hình tại `/etc/nginx/sites-available/ptit-web.conf`:
```bash
sudo nano /etc/nginx/sites-available/ptit-web.conf
```
*(Copy nội dung từ file `ptit-web.conf`)*

## 4. Kích hoạt Server Block & Hủy kích hoạt trang mặc định
Tạo liên kết tượng trưng (symlink) sang `sites-enabled`:
```bash
sudo ln -s /etc/nginx/sites-available/ptit-web.conf /etc/nginx/sites-enabled/
```

Hủy kích hoạt default config để tránh xung đột cổng 80:
```bash
sudo rm -f /etc/nginx/sites-enabled/default
```

## 5. Kiểm tra cú pháp và tải lại Nginx
Kiểm tra cú pháp cấu hình:
```bash
sudo nginx -t
```
*(Kết quả yêu cầu: `syntax is ok` và `test is successful`)*

Reload lại dịch vụ Nginx:
```bash
sudo systemctl reload nginx
```

## 6. Kiểm tra kết quả
Từ máy cá nhân, mở trình duyệt và truy cập:
```text
http://<IP_ADDRESS_DROPLET>
```
Kết quả hiển thị dòng chữ:
**"Welcome to PTIT DevOps Course - Session 02"**
