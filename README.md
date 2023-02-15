# StemGNN_env

---

## Environment

- OS : Ubuntu 18.04 LTS
- GPU : NVDIA RTX A6000 (48GB x 2)
- Architecture : x86_64
- NVIDIA Driver : 510.54
- CUDA : 11.5

## Version

- Torch v1.7.1
- CUDA 11.0 / 10.2 / 10.1 / 9.2 [1]
- cuDNN 8.8.0 for CUDA 11.x

## Installaion

1. del cuda

```
sudo apt-get purge nvidia* 
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*
```

2. install nvidia driver

```
sudo apt update
sudo apt install -y ubuntu-drivers-common
ubuntu-drivers devices : 그래픽카드와 설치 가능한 드라이버 확인
sudo ubuntu-drivers autoinstall : 권장 드라이버 자동으로 설치
sudo apt install nvidia-driver-xxx : 원하는 버전의 드라이버 수동으로 설치
sudo reboot : pc 재부팅
nvcc --version (or nvidia-smi: 추천)
```

3. install cuda 11.0.3 [3]

```
wget https://developer.download.nvidia.com/compute/cuda/11.0.3/local_installers/cuda_11.0.3_450.51.06_linux.run

sudo sh cuda_11.0.3_450.51.06_linux.run
```

4. trouble shooting

​	driver 수동설치 후 cuda 중 driver 선택해제

5. bashrc

```
~./profile 개인 /etc/profile 모든

sudo gedit ~/.profile
export PATH=/usr/local/cuda-11.0/bin:$PATH

export LD_LIBRARY_PATH=/usr/local/cuda-11.0/lib64:$LD_LIBRARY_PATH
```

```
$ source ~/.bashrc
$ nvcc --version
```

6. cudnn [4]

```
	tar –xzvf cudnn-11.0-linux-x64-v8.1.1.33.tgz
 
  sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
  sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64
  sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*

  cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
  ldconfig -N -v $(sed 's/:/ /' <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn

```

7. check
   1. nvidia  : nvidia-smi
   2. cuda  : nvcc -V
   3. cudnn  : ldconfig -N -v $(sed 's/:/ /' <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn

## Reference

[1] https://pytorch.org/get-started/previous-versions/

[2] https://developer.nvidia.com/cuda-toolkit-archive

[3] https://developer.nvidia.com/cuda-11-0-3-download-archive?target_os=Linux&target_arch=x86_64

[4] https://developer.nvidia.com/cudnn

## Note

```
# CUDA 11.0
pip install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

# CUDA 10.2
pip install torch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2

# CUDA 10.1
pip install torch==1.7.1+cu101 torchvision==0.8.2+cu101 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

# CUDA 9.2
pip install torch==1.7.1+cu92 torchvision==0.8.2+cu92 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

# CPU only
pip install torch==1.7.1+cpu torchvision==0.8.2+cpu torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html
```