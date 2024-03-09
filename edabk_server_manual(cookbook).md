# Hướng dẫn sử dụng  server EDABK
## _A cookbook made with love, passion, and caffein_
> Làm ơn **đọc kĩ**, 90% trường hợp set up thất bại là do bỏ bước  
## Step I: Tailscale
### Tải Tailscale:
##### Ubuntu
```
sudo apt-get update
sudo apt-get install tailscale
```
##### Window
- Truy cập page `https://pkgs.tailscale.com/stable/#windows`
- Tải file `.exe` bản mới nhất tương thích với máy tính của bạn (thường là amd64)
- Nháy đúp vào file để thực thi, khi tải xong icon Tailscale sẽ hiện lên trong taskbar (góc phải dưới)

### Đăng nhập:
##### Ubuntu
```
sudo tailscale up
```
Sau khi gõ lệnh sẽ hiện ra một link, bấm  vào link này để đăng nhập.
##### Window:
- Chuột phải vào icon Tailscale ở task bar, bấm vào `log in`
### Thêm server vào network của bạn
Mở link sau trong browser:
```
https://login.tailscale.com/admin/invite/7oM6QiZAmkX
```
Server sẽ được tự động thêm vào network của bạn.
## Step II: SSH và VNC
### SSH
> Kết nối ssh sẽ chỉ cho phép bạn điều khiển server bằng command line  (CLI).

Kết nối ssh tới server:
```
ssh $USER@100.68.93.47
```
Với `$USER` là tên user được cấp cho bạn có dạng `usrn`, n là 1 số 1-9
Password là 123 với mọi user.
### X-forwarding
> Cũng dựa trên ssh, nhưng cho phép bạn dùng giao diện đồ họa (GUI) với  1 số app. X-forwarding  **rất chậm** với các kết nối mạng ngoài, chỉ sử dụng X-forwarding với các máy trên lab.

Sửa file `/etc/ssh/ssh_config` bằng cách bỏ comment và sửa nội dung như sau:
```
#   ForwardAgent no
    ForwardX11 yes
    ForwardX11Trusted yes
#   PasswordAuthentication yes
```
### VNC
#### Tải viewer cho VNC:
##### Ubuntu

```
sudo apt update
sudo apt install remmina
```

- ![Mở application](https://www.google.com/url?sa=i&url=https%3A%2F%2Fsupport.system76.com%2Farticles%2Fubuntu-basics%2F&psig=AOvVaw15YMmTJ4WuOEpCOR3qoHy3&ust=1710063959321000&source=images&cd=vfe&opi=89978449&ved=0CBIQjRxqFwoTCMjAn-ny5oQDFQAAAAAdAAAAABAa), nhấp chuột vào icon remmina để chạy app.
- Chọn chế độ kết nối (bên cạnh thanh tìm kiếm) là VNC. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.68.93.47:n. Bấm enter để hoàn tất kết nối
##### Window
- Truy cập link `https://www.realvnc.com/en/connect/download/viewer/`, tải installer cho window và chạy nó
- Mở phần `start` (biểu tượng window góc trái dưới)
- Nhấn đúp vào biểu tượng RealVNC. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.68.93.47:n. Bấm enter để hoàn tất kết nối





