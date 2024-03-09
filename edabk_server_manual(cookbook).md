# Hướng dẫn sử dụng  server EDABK (alpha version)
## _A cookbook made with love, passion, and caffein_
> Chất lượng tốt hơn khi xem trên github hoặc  các markdown viewer 
## Step I: Tailscale
### Tải Tailscale:
```
sudo apt-get update
sudo apt-get install tailscale
```
### Đăng nhập:
```
sudo tailscale up
```
Sau khi gõ lệnh sẽ hiện ra một link, bấm  vào link này để đăng nhập.
### Thêm server vào network của bạn
Mở link sau trong browser:
```
https://login.tailscale.com/admin/invite/7oM6QiZAmkX
```
Server sẽ được tự động thêm vào network của bạn.
## Step II: SSH và VNC
#### SSH:
> Kết nối ssh sẽ chỉ cho phép bạn điều khiển server bằng command line  (CLI).

Kết nối ssh tới server:
```
ssh $USER@100.68.93.47
```
Thay thế $USER bằng tên user được cấp cho bạn.
Password là 123 với mọi user.
#### X-forwarding:
> Cũng dựa trên ssh, nhưng cho phép bạn dùng giao diện đồ họa (GUI) với  1 số app. X-forwarding  **rất chậm** với các kết nối mạng ngoài, chỉ sử dụng X-forwarding với các máy trên lab.

Sửa file /etc/ssh/ssh_config bằng cách bỏ comment và sửa nội dung như sau:
```
#   ForwardAgent no
    ForwardX11 yes
    ForwardX11Trusted yes
#   PasswordAuthentication yes
```
#### VNC:
##### Tải Reminna:
```
sudo apt update
sudo apt install remmina
```

![Mở application](https://www.google.com/url?sa=i&url=https%3A%2F%2Fsupport.system76.com%2Farticles%2Fubuntu-basics%2F&psig=AOvVaw15YMmTJ4WuOEpCOR3qoHy3&ust=1710063959321000&source=images&cd=vfe&opi=89978449&ved=0CBIQjRxqFwoTCMjAn-ny5oQDFQAAAAAdAAAAABAa), nhấp chuột vào icon remmina để chạy app. Chọn chế độ kết nối (bên cạnh thanh tìm kiếm là VNC). Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.68.93.47:1. Bấm enter để hoàn tất kết nối





