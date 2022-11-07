# Using ROS with Docker
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
   docker exec -it your-docker-id /bin/bash  # 进入容器
   source ros_entrypoint.sh
   cd /data/code_space/ros/prediction_ws/
   catkin_make
   source ./devel/setup.bash
   ```