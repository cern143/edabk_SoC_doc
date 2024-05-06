# Hướng dẫn sử dụng server EDABK (bản chi tiết)
> Trước đây mình nghĩ 1 bản hướng dẫn đơn giản, step by step là tối ưu để hướng dẫn mn sử dụng server. Nhưng thực tế thì khá đắng lòng khi mn hầu hết k tự set up và sử dụng được mà vẫn dí mình (╥﹏╥).
> Đó là lý do cho sự ra đời của bản hướng dẫn này. Điểm khác biệt lớn nhất của bản này là mình sẽ giải thích chứ k chỉ viết dạng mỳ ăn liền kiểu programming cookbook nữa.
## I. Network and remote access:
> Disclaimer: Toàn bộ kiến thức của phần này là mình tự tìm hiểu và cũng k phải chuyên môn (thậm chí mình còn k học mạng máy tính). Nếu có chỗ nào sai sót rất hoan nghênh góp ý của mn.
### Ports:
1 mạng internet gồm nhiều thiết bị kết nối với nhau. Câu hỏi đặt ra là chúng kết nối với nhau kiểu gì? Với pc thì câu trả lời là thông qua các **ports**(cổng). Có 2 loại ports là physical ports (.i.e các port vật lý như usb-c, vga,...) và virtual port. Trong hướng dẫn này ports mặc định hiểu là **virtual port**.
Để kết nối 2 pc bằng physical port, ta chỉ cần cắm dây. Nhưng với virtual port ta sẽ phải open port trong tường lửa nếu muốn kết nối bằng port đó. Ví dụ ta muốn mở port 2888:
##### CentOS:
```
firewall-cmd --add-port=2888/tcp
```
Sở dĩ phải open port vì nó mặc định là đóng. Điều này ngăn 1 pc kết nối với pc của bạn mà chưa được phép.
###### Important note: 2 kết nối **KHÔNG THỂ DÙNG CHUNG 1 CỔNG!**
###### Ứng dụng: vì mỗi (docker) container được coi là 1 thiết bị ảo, nên ta cần mở 1 cổng trên pc và kết nối cổng đó với container để truy cập vào 1 số tính năng của nó (e.g jupyter notebook)
