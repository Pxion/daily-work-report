### 2024.5.12
今晚得知任务分配后，找学长咨询了一下，叫先把ros2过一遍，刚好感觉好多忘了，所以准备着手更加深入细致系统化学习ros2。
但由于今晚有ddl要赶，来不及学太多，就先做了一个后续内容学习的大致规划，希望后续自己能严格跟着规划去完成相应的学习内容。

### 2024.5.13
今天虚拟机打不开了，疯狂搜集了一堆解决方法都没有解决，这个小男孩狠狠地碎掉了。搞了n久后，只能先暂时搁置。
然后转而去看了一下ros2的一些前置知识以及了解ROS2的核心概念并学习ROS2的基本架构。

### 2024.5.14
还是无法启动虚拟机，最终选择重装。
然后粗略了解了一下DDS架构和C++依赖查找机制，学习了如何使用g++、make、cmake三种方式来编译ros2的C++节点，但由于虚拟机还未安装完成，打算安装完成后再进行实践加深印象。

### 2024.5.15
屋漏偏逢连夜雨，电脑出问题了。想die。

### 2024.5.16
先暂时转向理论学习，学习了使用面向对象方式编写ros2节点，了解ros生态中的构建系统和构建工具并进阶学习colcon工具，还了解了ros2的DOMAIN_ID概念及在没有ROSMASTER的情况下，ros2如何实现互相发现。

### 2024.5.18
学习工作空间的创建、编译和配置；功能包的创建、编译及结构；创建节点流程。

### 2024.5.19
了解节点创建流程的案例；学习使用发布者、订阅者流程并了解相关案例。

### 2024.5.21
学习服务端、客户端实现流程及其相关实践案例。

### 2024.5.23
了解了通信接口的概念。

### 2024.5.28
在虚拟机上安装ros2；ros2小案例体验；ros2构建工具之colcon的使用。

### 2024.5.29
使用RCLCPP编写节点；colcon编译失败，寻求解决方法暂未果。

### 2024.5.30
成功解决colcon编译问题，重新把文件删除重走了一遍用rclcpp编写过程（可能是一开始在修改CMakeLists.txt时把第二段使用install指令将其安装到install目录的代码写到了package.xml里）；使用面向对象方法编写ros2节点。

### 2024.5.31
colcon使用进阶；ros2话题入门；创建一个话题控制节点，第一次编译成功，但找不到可执行文件，后来发现CMakeLists.txt中有个文件名打错了，修改后第二次编译失败，明天找找原因。

### 2024.6.1
查看了完整报错日志，重打代码后显示不存在某个函数，意识到可能是没保存（遇到过多次），Ctrl+S保存后果然编译成功；编写发布者，编写完毕后不出意外地又出意外了————编译再次失败，似乎是package.xml的问题，检查后尝试把添加depend标签并将消息接口写入的代码放在了</package>里（原来我直接放在最后），继续编译仍然错误。看来明天又是检查错误的一天。

### 2024.6.2
几经波折，多次试错，终于发现昨天编译失败的原因：
1. package.xml中rclcpp 依赖项存在冗余，存在重复声明；
2. CMakeLists.txt 文件中也存在重复的声明;
3. 代码存在几个语法和格式上的错误。
  ##### 解决方法：
1. 删除了重复的 <buildtool_depend>ament_cmake</buildtool_depend> 和 <depend>rclcpp</depend> 声明；
2. 确保每个 add_executable 和 ament_target_dependencies 只声明一次；
3. 修改有误代码，并确保所有必要的头文件都被包含。
最终成功编译！测试也成功运行。
