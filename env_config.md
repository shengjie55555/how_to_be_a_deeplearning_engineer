# Ubuntu环境配置：
__说明__：以下配置方法在Ubuntu20.04, 21.10, 22.04均可行。硬件配置为：i7-11800H和RTX3060.

## 安装中文输入法：
1. 安装google拼音
   ```shell
   sudo apt-get install fcitx-googlepinyin
   ```
2. 配置language support
   1. 打开language support：最下面一行Keyboard input method system，默认是iBus，点击下拉单切换到fcitx.
   2. 重启系统.
   3. 在右上角状态栏点击键盘图标，在下拉单里选择倒数第三个Configure进入配置界面.
   4. 点击输入方法设置左下角的+号，进入添加输入方法界面。取消“只显示当前语言”选项的勾选，输入pinyin搜索到系统现有的拼音输入法。选择Google Pinyin并点击OK确认.
## 安装electron-ssr
1. 下载: https://github.com/shadowsocksrr/electron-ssr/releases
2. 在终端输入python，如果默认是python2.7则直接下一步，如果为python3.x，那么需要安装python2,并且需要创建一个软链接指向python2
   ```shell
   cd /bin
   sudo ln -s python2.7 python
    ```
3. 安装electron-ssr所需要的依赖
   ```shell
   sudo apt install libcanberra-gtk-module libcanberra-gtk3-module gconf2 gconf-service libappindicator1
   sudo apt --fix-broken install  # 修复依赖关系
   ```
4. 安装electron-ssr:
   ```shell
   sudo dpkg -i electron-ssr.deb
   ```
## 安装cuda、cudnn
1. 下载cuda: https://developer.nvidia.com/cuda-toolkit-archive
2. 下载cudnn: https://developer.nvidia.com/rdp/cudnn-archive
3. 安装cuda
   1. 方法一
   ```shell
   sudo bash cuda_10.2.89_440.33.01_linux.run --toolkit --silent --override
   ```
   2. 方法二
   ```shell
   sudo sh cuda_11.7.0_515.43.04_linux.run  
   ```
   如果提示Existing package manager installation of the driver found，选择continue，在下一步中去除driver项，之后选择install（选项前面没有X代表取消勾选）。
4. 添加环境变量
   ```shell
   export PATH=/usr/local/cuda-11.1/bin:$PATH
   export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64:$LD_LIBRARY_PATH
   ```
5. 安装cudnn
   1. 解压cudnn
   2. 复制库文件和头文件到/usr/local/cuda-11.1/
      ```shell
      tar -xvf cudnn-linux-x86_64-8.5.0.96_cuda11-archive.tar.xz
      cd cudnn-linux-x86_64-8.5.0.96_cuda11-archive/
      sudo cp include/cudnn*.h /usr/local/cuda/include
      sudo cp -P lib/libcudnn* /usr/local/cuda/lib64
      sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
      ```
## 安装Anaconda
1. 下载: https://www.anaconda.com/
2. 安装
   ```shell
   bash Anaconda3-2021.11-Linux-x86_64.sh
   ```
3. 创建环境
   ```shell
   conda create -n motion python=3.8
   ```
## 安装pytorch
```shell
pip install torch==1.8.0+cu111 torchvision==0.9.0+cu111 torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html
```
## 安装pycharm
1. 下载: https://www.jetbrains.com/pycharm/download/download-thanks.html?platform=linux&code=PCC
2. 解压
3. 安装
   ```shell
   cd ./pycharm/bin/
   bash pycharm.sh
   ```
