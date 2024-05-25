# Hướng dẫn chạy jupyter notebook trên server
## I. Tải miniforge:
### 1. Giới thiệu:
- Miniforge gồm miniconda và micromamba:
+ Miniconda là quản lý các môi trường ảo của python. Một môi trường ảo thực chất là những đường dẫn tới các phiên bản python khác với phiên bản của máy. **LUÔN CHẠY PYTHON TRONG MÔI TRƯỜNG ẢO** vì nếu không có thể dẫn tới xung đột với python mặc định của OS => Liệm.
+ Micromamba là package manager. Conda đã có sẵn package manger là pip nhưng theo document của họ thì micromamba resolve package nhanh hơn và ít xung đột hơn.
### 2. Các bước tải:
- Bước 1: Truy cập vào github miniforge `https://github.com/conda-forge/miniforge`
- Bước 2: Tải về miniforge installer
/home/cern/Downloads/Screenshot from 2024-05-25 21-13-24.jpg
- Bước 3: Cấp quyền thực thi và chạy installer: (**thay thế /path/to/installer bằng đường dẫn thật tới Miniforge3-Linux-x86_64.sh**)
```
sudo chmod +x /path/to/installer
/path/to/installer
```
Bấm enter và chọn yes khi được yêu cầu.
Mở 1 terminal mới. Nếu thấy hiện môi trường hiện tại là base thì là thành công.
## II. Chạy jupyter notebook:
### 1. Tải jupyter:
```
pip install jupyter
```
### 2. Chạy notebook: 
- Mở terminal tại đường dẫn chứa jupyter notebook cần chạy:
/home/cern/Pictures/Screenshot from 2024-05-25 21-27-19.png
Rồi chạy lệnh:
```
jupyter notebook ip=0.0.0.0 --port=8889
```
Chúc mn thành công!
  

