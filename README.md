# FAST_LIO_RoboSense

基于 FAST_LIO 的 ROS2 Humble 版本，支持 RoboSense Airy 雷达。

## 功能特性

- ✅ 基于 FAST_LIO ROS2 Humble 版本
- ✅ 支持 RoboSense Airy 雷达（lidar_type: 5）
- ✅ 支持 RSM1 和 RSM1_BREAK 模式
- ✅ 完整的 ROS2 参数配置
- ✅ ROS2 launch 文件支持

## 依赖

- ROS2 Humble
- PCL
- Eigen3
- ikd-Tree (git submodule)

## 安装

1. 初始化 git 子模块：
```bash
cd /home/wang/workfiles/testbot_ws/src/fast_lio_robosense
git submodule update --init --recursive
```

2. 编译：
```bash
cd /home/wang/workfiles/testbot_ws
colcon build --packages-select fast_lio_robosense
source install/setup.bash
```

## 使用方法

### 启动 RoboSense Airy 雷达建图

```bash
ros2 launch fast_lio_robosense mapping_robosense_airy.launch.py
```

### 参数配置

配置文件位于 `config/robosenseAiry.yaml`，主要参数：

- `preprocess.lidar_type: 5` - RoboSense Airy 雷达类型
- `preprocess.scan_line: 96` - 扫描线数
- `common.lid_topic: "/rslidar_points"` - 点云话题
- `common.imu_topic: "/rslidar_imu_data"` - IMU 话题

## 与原 fast_lio 包的区别

- 包名：`fast_lio_robosense`（避免与原包冲突）
- 添加了 RoboSense M1/Airy 点类型支持
- 添加了 `robosenseM1_handler` 处理函数
- 支持点云字段兼容处理（自动检测是否有 ring 和 timestamp 字段）

## 注意事项

1. 原 `fast_lio` 包已被阻止编译（通过 COLCON_IGNORE），避免重名冲突
2. 如果点云消息没有 `ring` 和 `timestamp` 字段，代码会自动使用标准 PointXYZI 格式处理
3. 确保 ikd-Tree 子模块已正确初始化

## Git 仓库

本包包含独立的 git 仓库，位于 `src/fast_lio_robosense/`。
