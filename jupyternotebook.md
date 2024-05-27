# Hướng dẫn chạy jupyter notebook trên server
## I. Tải miniforge:
### 1. Giới thiệu:
- Miniforge gồm miniconda và micromamba:
+ Miniconda là quản lý các môi trường ảo của python. Một môi trường ảo thực chất là những đường dẫn tới các phiên bản python khác với phiên bản của máy. **LUÔN CHẠY PYTHON TRONG MÔI TRƯỜNG ẢO** vì nếu không có thể dẫn tới xung đột với python mặc định của OS => Liệm.
+ Micromamba là package manager. Conda đã có sẵn package manger là pip nhưng theo document của họ thì micromamba resolve package nhanh hơn và ít xung đột hơn.
### 2. Các bước tải:
Paste đoạn sau vào file `.bashrc`
```
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/edabk/miniforge3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/edabk/miniforge3/etc/profile.d/conda.sh" ]; then
        . "/home/edabk/miniforge3/etc/profile.d/conda.sh"
    else
        export PATH="/home/edabk/miniforge3/bin:$PATH"
    fi
fi
unset __conda_setup

if [ -f "/home/edabk/miniforge3/etc/profile.d/mamba.sh" ]; then
    . "/home/edabk/miniforge3/etc/profile.d/mamba.sh"
fi
# <<< conda initialize <<<
```
Mở 1 terminal mới. Nếu thấy hiện môi trường hiện tại là base thì là thành công.
## II. Chạy jupyter notebook:
### 1. Tải jupyter:
```
pip install jupyter
```
### 2. Chạy notebook: 
- Mở terminal tại đường dẫn chứa jupyter notebook cần chạy:
![Screenshot from 2024-05-25 21-27-19](https://github.com/cern143/edabk_SoC_doc/assets/70802909/9b8832ec-6bdd-46a9-952d-592d783e5fd2)

Rồi chạy lệnh:
```
jupyter notebook ip=0.0.0.0 --port=8889
```
Chúc mn thành công!
  

