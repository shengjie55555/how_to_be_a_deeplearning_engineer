# Install Docker
1. 安装教程
   1. https://docs.docker.com/engine/install/ubuntu/#uninstall-docker-engine
   2. 采用Install using the apt repository方法
   3. 不要用snap安装，否则会出现docker无法使用宿主机的gpu，即便安装了nvidia-container-toolkit
2. 解除sudo
   ```shell
   sudo groupadd docker
   sudo usermod -aG docker ${USER}
   # 或者采用如下方式
   sudo chmod 666 /var/run/docker.sock
   ```


# Using ROS with ROS official image
1. 下载image
   ```shell
   docker pull osrf/ros:melodic-desktop-full
   ```
2. 创建容器
   ```shell
   xhost +
   docker run -it -v$(pwd):/data --device=/dev/dri --group-add video --volume=/tmp/.X11-unix:/tmp/.X11-unix  --env="DISPLAY=$DISPLAY"  --name=catkin_rocker osrf/ros:melodic-desktop-full  /bin/bash  
   source ros_entrypoint.sh  # 每次进入容器都需要source
   roscore
   ```
   -v$(pwd):/data参数是指将当前目录挂载到ROS容器根目录data文件夹下，所以最好在/home/wsj/目录下运行docker run
3. 新建窗口进入容器
   ```shell
   docker ps -a  # 查看运行的容器
   docker exec -it container_id /bin/bash  # 进入容器
   source ros_entrypoint.sh
   cd /data/code_space/ros/prediction_ws/
   catkin_make
   source ./devel/setup.bash
   ```

# Build custom image with ROS and Python
1. 下载image
   ```shell
   docker pull nvidia/cuda:11.1.1-cudnn8-devel-ubuntu18.04
   ```
   dockerhub: https://hub.docker.com/r/nvidia/cuda/tags?page=1&name=11.1
2. 创建容器
   ```shell
   docker run -it -v$(pwd):/data --gpus all --network=host  d91fe8dffe66 /bin/bash
   ```
   1. 采用host模式直接共享本地主机网络，可以加快网络速度
   2. docker在19.03版本之后，可以不用安装nvidia-docker，就能获得GPU的计算支持，但是可能报如下错误:
      ```shell
      docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]].
      ```
      解决方法如下：
      ```shell
      apt-get install -y nvidia-container-toolkit
      systemctl restart docker
      ```
3. 安装anaconda和复制环境
   ```shell
   bash /data/anaconda.sh  # 注意路径尽量选择/root/anaconda3
   source ~/.bashrc
   conda create -n sf --clone /data/enter/envs/sf  # --clone后面是本地环境的路径
   ```
4. 安装ros
   ```shell
   echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros1-latest.list
   apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
   apt-get update
   apt install ros-melodic-desktop-full
   echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc && source ~/.bashrc
   conda activate sf
   pip3 install rosdep rospkg rosinstall_generator rosinstall wstool vcstools catkin_tools catkin_pkg
   rosdep init
   rosdep update
   ```
5. 制作镜像并打包
   ```shell
   docker commit -a="ShengjieWu" -m="Ubuntu18.04+cuda11.1+cudnn8+pytorch1.10+ros" 884e047ad5b3 myubuntu:1.0
   docker login  # 注册docker hub帐号，创建新的repo，shengjiewu/mybuntu
   docker tag myubuntu:1.0 shengjiewu/myubuntu:1.0  # 需要把本地镜像和repo对应上，才可以push
   docker push shengjiewu/myubuntu:1.0
   ```
参考链接：  
https://blog.csdn.net/weixin_42419002/article/details/103898124  
https://blog.csdn.net/Merokes/article/details/121364590  
https://blog.csdn.net/baidu_35692628/article/details/125252155  
https://blog.csdn.net/u013685264/article/details/123206768  

# Using ROS with custom image
1. 下载image
   ```shell
   docker pull shengjiewu/myubuntu:1.0  # 如果卡在Pulling fs layer，直接重启docker： systemctl restart docker
   ```
2. 创建容器
   ```shell
   xhost +
   docker run -it -v$(pwd):/data --device=/dev/dri --group-add video --volume=/tmp/.X11-unix:/tmp/.X11-unix  --env="DISPLAY=$DISPLAY" --network=host --gpus all  --name=catkin_rocker image_id  /bin/bash  
   roscore
   ```
3. 新建窗口进入容器
   ```shell
   docker ps -a  # 查看运行的容器
   docker exec -it container_id /bin/bash  # 进入容器
   cd /data/code_space/ros/prediction_ws/
   catkin_make
   source ./devel/setup.bash
   ```

# Using docker container with vscode
1. 安装插件
   1. Remote、Docker、ROS
2. 点击Docker插件start一个容器，或者命令行创建一个容器
3. 点击Remote Explore在上方[SSH Targets / Containers]中选择Containers
4. 在出现的Containers中选择相应的容器，右键然后Attach to Container即可进入容器开发环境

参考链接：https://blog.csdn.net/liu3612162/article/details/122878748  
