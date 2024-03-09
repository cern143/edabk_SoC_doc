# Hướng dẫn sử dụng  server EDABK
## _A cookbook made with love, passion, and caffein_
> Làm ơn **đọc kĩ**, 90% trường hợp set up **thất bại là do bỏ bước**  
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
### <a name="ssh"></a>SSH
> Kết nối ssh sẽ chỉ cho phép bạn điều khiển server bằng command line  (CLI).
```
ssh $USER@100.68.93.47
```
Với `$USER` là tên user được cấp cho bạn có dạng `usrn`, `n` là 1 số 1-9. Nhập user password là 123 với mọi user.
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
hình
- Mở application (icon dưới cùng trong action center a.k.a cái thanh bên trái màn hình), nhấp chuột vào icon remmina để chạy app.
- Chọn chế độ kết nối (bên cạnh thanh tìm kiếm) là VNC. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.68.93.47:n (`n` là số thứ tự user xem ở [phần ssh](#ssh)) . Bấm enter để tiến hành kết nối. Nhập password vnc là @edabk với mọi user
##### Window
- Truy cập link `https://www.realvnc.com/en/connect/download/viewer/`, tải installer cho window và chạy nó
- Mở phần `start` (biểu tượng window góc trái dưới)
- Nhấn đúp vào biểu tượng RealVNC. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.68.93.47:n (`n` là số thứ tự user xem ở [phần ssh](#ssh)). Bấm enter để tiến hành kết nối. Nhập password vnc là @edabk với mọi user
## Extra: Chạy jupyter notebook bằng docker container
> Hướng dẫn sau được viết cho ubuntu, mình không dùng docker trong win nên các bạn trong trường hợp này tự thân vận động vậy :)) Nghe nói docker win cũng thao tác khá giống ubuntu trong CLI
> Trong server mình đã thực hiện hết phần set up
### Set up
- Tải docker
```
sudo apt update
sudo apt install docker.io
```
- Để chạy lệnh docker mà không cần `sudo`, các bạn add user mình đang dùng vào group docker
```
usermod -a -G docker $USER
```
với `$USER` là username của bạn
### Create container
- Tạo thư mục cho container trên host (máy tính chạy container)
> Bước này không bắt buộc nhưng rất hữu ích. Các file không gitclone được thì bạn tải vào thư mục này là nó sẽ xuất hiện trong container
```
mkdỉr yourdir
```
Với `yourdir` là tên thư mục tùy bạn chọn
- Tạo container với lệnh sau
```
docker run -it --rm -p 10000:8888 -v $YOURDIR:/home/jovyan/work quay.io/jupyter/scipy-notebook:latest
```
với `$YOURDIR` là đường dẫn tới thư mục bạn tạo ở trên. Bạn có thể chọn port khác như 8889,100001,... miễn sao port các container dùng khônghông trùng nhau Lần đầu chạy sẽ hơi lâu vì docker phải pull image về
> Giải thích: `-i` cho phép container hoạt động kể cả khi đóng terminal, `-t` tạo ra 1 terminal shell cho container, `-p` gắn port của container vào host theo cú pháp `-p host_port:container_port`, `-v` bind mount đường dẫn container và host theo cú pháp `-v host_dir:container_dir`
- Chạy lệnh trên sẽ ra 1 đống như ảnh dưới
![Screenshot from 2024-03-09 22-56-03](https://github.com/cern143/edabk_SoC_doc/assets/70802909/2242f7d7-65ce-4fd7-b0b8-cdaa4f8be621)
Copy dòng được hightlight ra đâu đó, thay 8888 bằng port bạn đã chọn rồi mở link trong browser của host. Thành quả như ảnh dưới
![Screenshot from 2024-03-09 23-01-20](https://github.com/cern143/edabk_SoC_doc/assets/70802909/4a6248b5-9dd3-46b5-9754-493a584fcb5f)
Chúc các bạn thực hiện thành công!
> Mọi thắc mắc xin tag em Sơn trên nhóm.
> Donate cho em Sơn 1 ly cà phê vì đã cày cả tuần để set up server và viết hướng dẫn này >.<






