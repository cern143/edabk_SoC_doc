# Hướng dẫn sử dụng  server EDABK
## _A cookbook made with love, passion, and caffein_
> Làm ơn **đọc kĩ**, 90% trường hợp set up **thất bại là do bỏ bước**  
## Step I: Tailscale
### Tải Tailscale:
##### Ubuntu
- Thêm vào Tailscale’s package signing key vàvà repository:
```
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```
- Tải Tailscale:
```
sudo apt-get update
sudo apt-get install tailscale
```
##### Window
- Truy cập page `https://pkgs.tailscale.com/stable/#windows`
- Tải file `.exe` bản mới nhất tương thích với máy tính của bạn (thường là bản amd64)
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
https://login.tailscale.com/admin/invite/bk2XQGhQXiV
```
Server sẽ được tự động thêm vào network của bạn.
## Step II: SSH và VNC
### <a name="ssh"></a>SSH
> Kết nối ssh sẽ chỉ cho phép bạn điều khiển server bằng command line  (CLI).
```
ssh $USER@100.75.44.97
```
Với `$USER` là tên user được cấp cho bạn cùng password tương ứng (hiện tại được cấp bằng cách ib cho tác giảgiả :>)
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
Làm như win nhưng tải installer cho ubuntuubuntu
##### Window
- Truy cập link `https://www.realvnc.com/en/connect/download/viewer/`, tải installer cho window và chạy nó
- Mở phần `start` (biểu tượng window góc trái dưới)
- Nhấn đúp vào biểu tượng RealVNC. Nhập địa chỉ ip máy chủ vào thanh tìm kiếm là: 100.75.44.97:n (`n` là số thứ tự user được cấp). Bấm enter để tiến hành kết nối.
- Nhập password vnc là @edabk với mọi user
#### Trong trường hợp server đang không hoạt động (unable to connect to server):
- Log in vào [ssh](#ssh)
- Chạy lệnh:
```
vncserver -n
```
Với `n` là số thứ tự user được cấp.
- Nó sẽ ra thông báo kiểu:
```
Warning: localhost.localdomain:n is taken because of /tmp/.X11-unix/X1
```
Lưu ý: không phải lúc nào tên file cũng là `/tmp/.X11-unix/X1`
- Xóa cái file nó bảo đi
```
sudo rm -rf /tmp/.X11-unix/X1
```
- Rồi khởi động server là xong:
```
vncserver -n
```
## Extra: Chạy jupyter notebook bằng docker container
> Hướng dẫn sau được viết cho ubuntu/centos, mình không dùng docker trong win nên các bạn trong trường hợp này tự thân vận động vậy :)) Nghe nói docker win cũng thao tác khá giống ubuntu trong CLI. Trong server mình đã thực hiện hết phần set up và mở port. Có thể tham khảo 1 số câu lệnh thường dùng ở phần [phụ lục](#phụ-lục-những-câu-lệnh-cơ-bản-trên-docker)
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
- Liệt kê các container đã tồn tại và port tương ứng chúng sử dụng:
```
docker ps -a
```
- Tạo container với lệnh sau
```
docker run -it --rm -p 10000:8888 -v $YOURDIR:/home/jovyan/work quay.io/jupyter/scipy-notebook:latest
```
với `$YOURDIR` là đường dẫn tới thư mục bạn tạo ở trên. Bạn có thể chọn port khác như 8889,100001,... miễn sao **không trùng port** của các container đã tồn tại. Lần đầu chạy sẽ hơi lâu vì docker phải pull image về
> Giải thích: `-i` cho phép container hoạt động kể cả khi đóng terminal, `-t` tạo ra 1 terminal shell cho container, `-p` gắn port của container vào host theo cú pháp `-p host_port:container_port`, `-v` bind mount đường dẫn container và host theo cú pháp `-v host_dir:container_dir`
- Chạy lệnh trên sẽ ra 1 đống như ảnh dưới
![Screenshot from 2024-03-09 22-56-03](https://github.com/cern143/edabk_SoC_doc/assets/70802909/2242f7d7-65ce-4fd7-b0b8-cdaa4f8be621)
Copy dòng được hightlight trong ảnh ra đâu đó, thay 8888 bằng port bạn đã chọn.
- Mở port trên host:
> Ubuntu
```
sudo ufw allow 100000
```
> CentOS:
```
firewall-cmd --permanent --zone=docker --add-port=10000/tcp
```
thay 100000 bằng port bạn đã chọn.
- Truy cập vào container bằng cách nhập link đã copy ra lúc trước vào browser. Thành quả như ảnh dưới:
![Screenshot from 2024-03-09 23-01-20](https://github.com/cern143/edabk_SoC_doc/assets/70802909/4a6248b5-9dd3-46b5-9754-493a584fcb5f)
Chúc các bạn thực hiện thành công!
### Phụ lục: Những câu lệnh cơ bản trên docker
- Liệt kê các container đang chạy:
```
docker ps
```
- Liệt kê tất cả container (kể cả không chạy):
```
docker ps -a
```
- Chạy terminal container trong terminal của host (hữu ích nếu quên không lưu token):
```
docker exec -it ID /bin/bash
```
với ID là id của container muốn chạy
- Show token (chạy trong terminal của container):
```
jupyter list
```
> Mọi thắc mắc xin tag em Sơn trên nhóm. Donate cho em Sơn 1 ly cà phê vì đã cày cả tuần để set up server và viết hướng dẫn này >.<






