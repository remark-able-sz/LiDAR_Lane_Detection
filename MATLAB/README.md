## Matlab
1. ROS pointcloud2 object to pointcloud object
```
bag = rosbag(filepath);
pointcloud2_message = select(bag,'Topic','/rslidar_points');
% msg:cell
% msg{1}:pointcloud2 object
msg = readMessages(pointcloud2_message,i);
xyz = readXYZ(msg{1}); 
intensity = readField(msg{1},'intensity');
intensity(find(intensity>100)) = 100;
% pt_ori:pointcloud object
pt_ori = pointCloud(xyz);
pt_ori.Intensity = intensity;
```
to be continued ...
