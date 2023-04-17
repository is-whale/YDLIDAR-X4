
# YDLIDAR ROS Driver
## Clone ydlidar_ros_driver

1. 克隆后本地编译

   ```
   cd ydlidar_ws
   catkin_make
   ```
   `source ./devel/setup.sh`

2. 添加到环境变量
    ```
    $echo "source ~/ydlidar_ws/devel/setup.bash" >> ~/.bashrc
    $source ~/.bashrc
    ```
3. 检查环境变量
    ```
    $ echo $ROS_PACKAGE_PATH
    ```

5. 设置串口
    ```
	$chmod 0777 src/ydlidar_ros_driver/startup/*
	$sudo sh src/ydlidar_ros_driver/startup/initenv.sh
    ```
## Run ydlidar_ros_driver

##### Run ydlidar_ros_driver using launch file

The command format is : 

 `roslaunch ydlidar_ros_driver [launch file]`

1. Connect Triangle LiDAR uint(s).
   ```
   # G4, G5
   roslaunch ydlidar_ros_driver lidar_view.launch 
   ```

2. Connect to TOF LiDAR uint(s).
   ```
   # TG15, TG30, TG50
   roslaunch ydlidar_ros_driver TG.launch 
   # TX8, TX20
   roslaunch ydlidar_ros_driver TX.launch 
   ```
3. Connect to TOF NET LiDAR uint(s).
   ```
   # T5, T15
   roslaunch ydlidar_ros_driver T15.launch 
   ```

#####  Launch file introduction

The driver offers users a wealth of options when using different launch file. The launch file directory    

is `"ydlidar_ws/src/ydlidar_ros_driver/launch"`. All launch files are listed as below : 

| launch file               | features                                                     |
| ------------------------- | ------------------------------------------------------------ |
| G1.launch         | Connect to G1 LiDAR<br/>Publish LaserScan message on `scan` topic |
| G2.launch         | Connect to G2 LiDAＲ<br/>Publish LaserScan message on `scan` topic |
| G6_G7.launch      | Connect to G6/G7 LiDAR<br />Publish LaserScan message on `scan` topic |
| lidar.launch      | Connect to G4/G5 LiDAR<br />Publish LaserScan message on `scan` topic |
| lidar_view.launch | Connect to G4/G5 LiDAR<br />Publish LaserScan message on `scan` topic <br/>Automatically load rviz |
| T15.launch        | Connect to T5/T15 LiDAR<br />Publish LaserScan message on `scan` topic |
| TG.launch         | Connect to TG15/TG30/TG50 LiDAR<br />Publish LaserScan message on `scan` topic |
| TX.launch         | Connect to TX8/TX20 LiDAR<br />Publish LaserScan message on `scan` topic |
| X2.launch         | Connect to X2/X2L LiDAR<br />Publish LaserScan message on `scan` topic |
| X4.launch         | Connect to X4 LiDAR<br />Publish LaserScan message on `scan` topic |

## Publish Topic
| Topic                | Type                    | Description                                      |
|----------------------|-------------------------|--------------------------------------------------|
| `scan`               | sensor_msgs/LaserScan   | 2D laser scan of the 0-angle ring                |
| `laser_fan`           | ydlidar_ros_driver::LaserFan   | 2D Raw laser fan of the 0-angle ring                |

## Subscribe Service
| Service                | Type                    | Description                                      |
|----------------------|-------------------------|--------------------------------------------------|
| `stop_scan`          | std_srvs::Empty   | turn off lidar                                         |
| `start_scan`         | std_srvs::Empty   | turn on lidar                                          |



## Configure ydlidar_ros_driver internal parameter

The ydlidar_ros_driver internal parameters are in the launch file, they are listed as below :

| Parameter name | Data Type | detail                                                       |
| -------------- | ------- | ------------------------------------------------------------ |
| port         | string | Set Lidar the serial port or IP address <br/>it can be set to `/dev/ttyUSB0`, `192.168.1.11`, etc. <br/>default: `/dev/ydlidar` |
| frame_id     | string | Lidar TF coordinate system name. <br/>default: `laser_frame` |
| ignore_array | string | LiDAR filtering angle area<br/>eg: `-90, -80, 30, 40` |
| baudrate     | int | Lidar baudrate or network port. <br/>default: `230400` |
| lidar_type     | int | Set lidar type <br/>0 -- TYPE_TOF<br/>1 -- TYPE_TRIANGLE<br/>2 -- TYPE_TOF_NET <br/>default: `1` |
| device_type     | int | Set device type <br/>0 -- YDLIDAR_TYPE_SERIAL<br/>1 -- YDLIDAR_TYPE_TCP<br/>2 -- YDLIDAR_TYPE_UDP <br/>default: `0` |
| sample_rate     | int | Set Lidar Sample Rate. <br/>default: `9` |
| abnormal_check_count     | int | Set the number of abnormal startup data attempts. <br/>default: `4` |
| fixed_resolution     | bool | Fixed angluar resolution. <br/>default: `true` |
| reversion     | bool | Reversion LiDAR. <br/>default: `true` |
| inverted     | bool | Inverted LiDAR.<br/>false -- ClockWise.<br/>true -- CounterClockWise  <br/>default: `true` |
| auto_reconnect     | bool | Automatically reconnect the LiDAR.<br/>true -- hot plug. <br/>default: `true` |
| isSingleChannel     | bool | Whether LiDAR is a single-channel.<br/>default: `false` |
| intensity     | bool | Whether LiDAR has intensity.<br/>true -- G2 LiDAR.<br/>default: `false` |
| support_motor_dtr     | bool | Whether the Lidar can be started and stopped by Serial DTR.<br/>default: `false` |
| angle_min     | float | Minimum Valid Angle.<br/>default: `-180` |
| angle_max     | float | Maximum Valid Angle.<br/>default: `180` |
| range_min     | float | Minimum Valid range.<br/>default: `0.1` |
| range_max     | float | Maximum Valid range.<br/>default: `16.0` |
| frequency     | float | Set Scanning Frequency.<br/>default: `10.0` |
| invalid_range_is_inf     | bool | Invalid Range is inf.<br/>true -- inf.<br/>false -- 0.0.<br/>default: `false` |
More paramters details, see [here](details.md)







