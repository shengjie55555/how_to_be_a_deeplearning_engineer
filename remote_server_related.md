1. Screen
   1. 创建screen会话:
      1. 在terminal中运行命令前加上screen 
        ```shell
        screen roscore
        ``` 
      2. ```Screen -S session_name```
   2. 暂时离开:Ctrl + a + d
   3. 恢复screen会话
        ```shell
        screen -ls  # 列出所有会话
        screen -r XXX  # 恢复会话XXX 
        ``` 
   4. 关闭screen会话 
      1. 进入要关闭会话, 直接Ctrl + c退出 
      2. ```screen -X -S session_name quit```
   5. 进入回滚模式 
      1. ctrl+a+Esc进入 
      2. 再按Esc退出   