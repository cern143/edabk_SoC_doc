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
- Truy cập link `https://tailscale.com/download/windows`, bấm vào `Download Tailscale for Windows` để tải file cài đặt (tailscale setup)
![Screenshot (16)](https://github.com/user-attachments/assets/df874f87-b0b0-4b5b-a616-1295324502c8)
- Chạy tailscale setup
![Screenshot (15)](https://github.com/user-attachments/assets/6d7f23d8-7bc4-4fa9-820e-96e60e1133e6)
- Khi tải xong icon Tailscale sẽ hiện lên trong taskbar (góc phải dưới).  Chuột phải vào icon Tailscale ở task bar, bấm vào `log in`
![Screenshot (16)](https://github.com/user-attachments/assets/b0084eb3-eb76-4b9d-baa8-b6a4520d2917)
![Screenshot (18)](https://github.com/user-attachments/assets/d071b8c4-7ec4-46d6-9349-2480264ee947)
- Nhập email rồi bấm sign in để đăng nhập:
![Screenshot (19)](https://github.com/user-attachments/assets/67f29982-f47f-42a0-9706-0dddd65b545d)

- Thêm server EDABK vào network của bạn bằng cách bấm vào link được gửi

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
B1: Tải realvnc viewer 
- Truy cập link `https://www.realvnc.com/en/connect/download/viewer/`, tải installer cho window và chạy nó. Bấm next tất cả prompt 
![Screenshot (20)](https://github.com/user-attachments/assets/1cc92895-132f-4468-9617-f567b75aaacd)
![Screenshot (21)](https://github.com/user-attachments/assets/f04ba00d-0e37-4a1e-a712-674d3812dbf7)
![Screenshot (24)](https://github.com/user-attachments/assets/77ca4bfb-339b-4002-a405-d24226a502c4)
- Khởi chạy RealVNC viewer. Bấm vào log in rồi đóng cửa sổ khi được yêu cầu đăng nhập. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.75.44.97:n (`n` là số thứ tự user được cấp). Bấm enter để tiến hành kết nối
**Nếu không kết nối được hãy thử khởi động lại pc**
![Screenshot (28)](https://github.com/user-attachments/assets/f7e3708c-c69b-4078-b621-765b9952da29)
![Screenshot (30)](https://github.com/user-attachments/assets/909b0455-f93b-420c-bca6-2fb6da0ddecf)
- Nhập password vnc là @edabk với mọi user
**Pass user khác với pass vnc
![Screenshot (31)](https://github.com/user-attachments/assets/32727c46-639e-4f30-b4d2-5dc465947d92)
- Khi kết nối thành công sẽ hiện ra màn hình của server. Nhập password của user để đăng nhập
![Screenshot (32)](https://github.com/user-attachments/assets/468d3dd9-d92f-43df-ad6b-a9450e383668)
![Screenshot (33)](https://github.com/user-attachments/assets/88ed9b2d-c9ee-40a1-81d0-7f5882f6f521)
B2: Điều chỉnh thêm:
- Chỉnh picture quality lên medium để có màu bình 
![Screenshot (34)](https://github.com/user-attachments/assets/80254738-3fff-4682-b00a-c28f960337bb)
![Screenshot (35)](https://github.com/user-attachments/assets/cbd50030-b0f0-4260-a162-07b1ae1cb606)
- Chỉnh setting centos để có kích thước hiển thị phù hợp với màn hình (thường là 16:9)
![Screenshot (36)](https://github.com/user-attachments/assets/38e8115b-0bc2-408b-b6de-f8c332ade166)

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





