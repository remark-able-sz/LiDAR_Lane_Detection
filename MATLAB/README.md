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
pt_ori = pointCloud(xyz,'Intensity',intensity);
```
2. Find the single line data from 80 lines and use Median Filter to smooth data
```
% Line 4 from the bottom to the top
xyz_4 = double(xyz(1:80:144000,:));
intensity_4 = double(intensity(1:80:144000,:));
% remove nan data in xyz and intensity
idx = all(~isnan(xyz_4),2);
[sphere_theta_line_4,sphere_phi_line_4,sphere_row_line_4]=cart2sph(xyz_4(:,1), xyz_4(:,2), xyz_4(:,3));
row = sphere_row_line_4(idx,:);
phi = mean(sphere_phi_line_4(idx,:));
theta = sphere_theta_line_4(idx,:);
intensity_4_real = intensity_4(idx,:);
window = 9;
xyz_median = medianFilter(row,phi,theta,window);
```
to be continued ...
