# Hướng dẫn chạy genus trên server
## I. Set up environment:
B1: Truy cập vào directory `/home/edabk/cadence_script` trên server

B2: Copy file run.csh vào đường dẫn `$HOME` của mình

B3: Mở terminal ở , nhập lệnh 
```
csh
``` 
Lệnh này để chuyển shell bạn đang dùng từ bash sang csh, do script này được viết bằng ngôn ngữ của shell csh

B4: Nhập lệnh: 
```
source run.csh
``` 
Check xem đã chạy được genus chưa:
```
genus -version
```
Ngoài ra nếu không muốn dùng shell csh, bạn có thể edit script 1 chút. Lệnh `setenv` trong csh tương đương với `export` trong bash và zsh

