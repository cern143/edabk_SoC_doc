# Hướng dẫn sử dụng server EDABK

## I. Tải Tailscale
#### Ubuntu
Chạy các lệnh sau trong terminal:
- Thêm vào Tailscale’s package signing key và repository:
```
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```
- Tải package
```
sudo apt-get update
sudo apt-get install tailscale
```
- Đăng nhập:
```
sudo tailscale up
```
Sau khi gõ lệnh sẽ hiện ra một link, bấm vào link này để đăng nhập.
#### Window
- Truy cập link `https://tailscale.com/download/windows`, bấm vào `Download Tailscale for Windows` để tải file cài đặt
![Screenshot from 2024-11-06 18-14-15](https://github.com/user-attachments/assets/ddb109fb-421c-458c-aab7-6a3a15217774)

- Nháy đúp vào file để thực thi, khi tải xong icon Tailscale sẽ hiện lên trong taskbar (góc phải dưới)

- Đăng nhập: Chuột phải vào icon Tailscale ở task bar, bấm vào `log in`

#### Thêm server EDABK vào network của bạn
Dùng link được gửi

## II. SSH và VNC
### <a name="ssh"></a>SSH
> Kết nối ssh sẽ chỉ cho phép bạn điều khiển server bằng command line (CLI).
```
ssh $USER@100.75.44.97
```
Với `$USER` là tên user được cấp (bởi admin) cùng password tương ứng

### <a name="vnc"></a>VNC
**Trong trường hợp vnc không hoạt động, vui lòng xem mục [sửa lỗi](#fix) và thử trước khi báo lỗi với admin**
> Hướng dẫn này sử dụng VNC client là realvnc viewer, nếu không thích user có thể dùng những client khác
#### Ubuntu
Làm như hướng dẫn cho win (bên dưới) nhưng tải installer cho ubuntu

#### Window
B1: Khởi chạy session vncserver trên server
- Kết nối tới server bằng [ssh](#ssh)
- Chạy lệnh:
```
vncserver :n
```
Với `n` là port được cấp.

B2: Tải realvnc viewer 
- Truy cập link `https://www.realvnc.com/en/connect/download/viewer/`, tải installer cho window và chạy nó
- Mở phần `start` (biểu tượng window góc trái dưới)
- Nhấn đúp vào biểu tượng RealVNC. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.75.44.97:n (`n` là số thứ tự user được cấp). Bấm enter để tiến hành kết nối.
- Nhập password vnc là @edabk với mọi user

****
### <a name="fix"></a> Sửa lỗi:
#### Port bị chiếm bởi 1 session khác
> Đây là 1 lỗi khá thường gặp, xảy ra khi session vnc không được kết thúc đúng cách
```
Warning: 100.75.44.97:n is taken because of /tmp/.X11-unix/X1
```
Lưu ý: tên file có thể khác so với ví dụ
- Xóa tất cả file lock
```
sudo rm -rf /tmp/.X11-unix/X1
```
- Sau đó khởi động session mới:
```
vncserver -n
```
- Truy cập vào server bằng [vnc](#vnc)





