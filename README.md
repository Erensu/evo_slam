本git作者更新了源作者的evo程序，并放入自己的数据及处理结果my_data里及所写的py文件my_txt_py供读者学习



github 下载后
安装
pip install evo --upgrade --no-binary evo
开始测试
evo_traj euroc data.csv --plot
报错：evo_traj 没有这个命令
此时，需要更新：
pip3 install evo --upgrade



##### 测试1：

evo_traj euroc data.csv --plot 

[ERROR] EuRoC MAV state ground truth must have 17 entries per row and no trailing delimiter at the end of the rows (comma)
原因是data.csv列数不对，需要17列
继续测试：
[ERROR] Unhandled error in evo.main_traj
Traceback (most recent call last):
  File "/usr/lib/python3.5/tkinter/__init__.py", line 36, in <module>
    import _tkinter
ImportError: No module named '_tkinter
解决：sudo apt-get install python3-tk
继续测试 ok
显示：
name:	data
infos:	36382 poses, 80.626m path length, 181.905s duration
/home/lyy/catkin_Evaluate/Evo/image.png
/home/lyy/catkin_Evaluate/Evo/image1.png
/home/lyy/catkin_Evaluate/Evo/image2.png

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image.png)

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image1.png)

##### 测试2：

evo_traj euroc data.csv --save_as_tum

name:	data

infos:	36382 poses, 80.626m path length, 181.905s duration

Trajectory saved to: data.tum
/home/lyy/catkin_Evaluate/Evo/evo/data.tum



##### 测试3：

evo_traj euroc data.csv --save_as_bag
报错：ImportError: No module named 'rospkg'
解决sudo apt-get install python-rospkg，没有用还是报上面的错误
继续解决： sudo apt-get install python3-rospkg
测试报新的错误：ImportError: No module named 'rosbag'
去你大爷的，安装rospkg后把我的ros搞坏了，想想测试3页没有用，不搞测试3了，妈也



##### 测试4：VIORB

evo_ape euroc data.csv no_SaveTrajectory.txt -va --plot 
报错：[ERROR] found no matching timestamps between data.csv and SaveTrajectory.txt with max. time diff 0.01 (s) and time offset 0.0 (s)
因为我用的SaveTrajectory.txt格式如下
1403636582313555456.000000 -0.002683 0.004363 -0.010236 0.999985 -0.004876 -0.002524 -0.000469
1403636582413555456.000000 -0.004578 0.013875 -0.033980 0.999985 0.003896 -0.003846 0.000437
1403636582463555584.000000 -0.013607 0.045442 -0.134066 0.999989 0.002634 -0.003093 0.002397
换成格式如下：yes_SaveTrajectory.txt,运行ok.
1403636581.013556 -0.000091891 -0.002907546 -0.008895828 0.007203280 0.000294416 -0.001041192 0.999973476
1403636581.063555 -0.000032670 -0.005313850 -0.017090926 0.013974291 -0.000294735 -0.000776108 0.999902010
1403636581.113555 -0.000375517 -0.009852243 -0.033186555 0.018218270 0.000033754 0.000549461 0.999833882
主要是时间戳的问题。

结果显示如下：

Loaded 36382 stamps and poses from: data.csv
Loaded 3642 stamps and poses from: SaveTrajectory.txt
Synchronizing trajectories...
Found 3620 of max. 36382 possible matching timestamps between...
	data.csv
and:	SaveTrajectory.txt

..with max. time diff.: 0.01 (s) and time offset: 0.0 (s).

Aligning using Umeyama's method...
Rotation of alignment:
[[-0.36148164 -0.86059522  0.35875743]
 [-0.93224672  0.34009048 -0.12350917]
 [-0.01571858 -0.37909674 -0.92522354]]
Translation of alignment:
[ 4.73088632 -1.87812632  0.89983517]

Scale correction: 1.0

Compared 3620 absolute pose pairs.

Calculating APE for translation part pose relation...

APE w.r.t. translation part (m)
(with SE(3) Umeyama alignment)

       max	0.228561
      mean	0.083928
    median	0.093531
       min	0.006836
      rmse	0.094039
       sse	32.013099
       std	0.042420

--------------------------------------------------------------------------------
Plotting results... 
/home/lyy/catkin_Evaluate/Evo/image3.png
/home/lyy/catkin_Evaluate/Evo/image4.png

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image3.png)

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image4.png)

##### 测试5：VIORB

evo_rpe euroc data.csv yes_SaveTrajectory.txt -va --plot 

结果如下：

Loaded 36382 stamps and poses from: data.csv
Loaded 3642 stamps and poses from: SaveTrajectory.txt
Synchronizing trajectories...
Found 3620 of max. 36382 possible matching timestamps between...
	data.csv
and:	SaveTrajectory.txt

..with max. time diff.: 0.01 (s) and time offset: 0.0 (s).

Aligning using Umeyama's method...
Rotation of alignment:
[[-0.36148164 -0.86059522  0.35875743]
 [-0.93224672  0.34009048 -0.12350917]
 [-0.01571858 -0.37909674 -0.92522354]]
Translation of alignment:
[ 4.73088632 -1.87812632  0.89983517]

Scale correction: 1.0

Found 3619 pairs with delta 1 (frames) among 3620 poses using consecutive pairs.
Compared 3619 relative pose pairs, delta = 1 (frames) with consecutive pairs.

Calculating RPE for translation part pose relation...

RPE w.r.t. translation part (m)
for delta = 1 (frames) using consecutive pairs
(with SE(3) Umeyama alignment)

       max	0.208138
      mean	0.032291
    median	0.029176
       min	0.000003
      rmse	0.042154
       sse	6.430810
       std	0.027097

--------------------------------------------------------------------------------
Plotting results...
/home/lyy/catkin_Evaluate/Evo/image5.png
/home/lyy/catkin_Evaluate/Evo/image6.png 

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image5.png)

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image6.png)

##### 测试6：比较不同算法下的真值与估计值的关系

 evo_traj euroc ORB_SaveTrajectory.txt VINS_SaveTrajectory.txt --ref=data.csv -p --plot_mode=xz
报错：[ERROR] EuRoC MAV state ground truth must have 17 entries per row and no trailing delimiter at the end of the rows (comma)
//未解决
去你妈的，用下面代替即可，官网也说了，EUROC需要转成tum在evo_traj上方可使用，见下面连接
浪费我的时间找错，不过这个过程中用python写了data.txt中的，全部转成空格，存在new.txt中, 程序放在了txt.py,以后很有用！！！！！！！！！！
In euroc mode, evo's metrics require you to give the reference in the EuRoC format and the estimated trajectory in the TUM format.
https://github.com/MichaelGrupp/evo/wiki/Formats


但是我用测试2中转换的data.tum格式可以运行成功
evo_traj tum ORB_SaveTrajectory.txt VINS_SaveTrajectory.txt --ref=data.tum -p --plot_mode=xz

结果如下：

name:	ORB_SaveTrajectory

infos:	3642 poses, 83.078m path length, 182.800s duration

name:	VINS_SaveTrajectory

infos:	3642 poses, 83.078m path length, 182.800s duration

name:	data
infos:	36382 poses, 80.626m path length, 181.905s duration
/home/lyy/catkin_Evaluate/Evo/image10.png
/home/lyy/catkin_Evaluate/Evo/image11.png
/home/lyy/catkin_Evaluate/Evo/image12.png

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image10.png)

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image11.png)

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image12.png)

##### 测试7：

给的例子： evo_traj kitti KITTI_00_ORB.txt KITTI_00_SPTAM.txt --ref=KITTI_00_gt.txt -p --plot_mode=xz

结果如下：

name:	KITTI_00_ORB

infos:	4541 poses, 3705.098m In euroc mode, evo's metrics require you to give the reference in the EuRoC format and the estimated trajectory in the TUM format.path length

name:	KITTI_00_SPTAM

infos:	4541 poses, 3718.501m path length

name:	KITTI_00_gt
infos:	4541 poses, 3724.187m path length
/home/lyy/catkin_Evaluate/Evo/image7.png
/home/lyy/catkin_Evaluate/Evo/image8.png
/home/lyy/catkin_Evaluate/Evo/image9.png

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image7.png)

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image8.png)

![image9](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image9.png)

#### 下面开始各位知友最关心的问题，评测VINS

VINS源程序肯定不行

##### 测试8：

evo_ape euroc data.csv vins_result_loop.txt -va --plot
报错：[ERROR] TUM trajectory files must have 8 entries per row and no trailing delimiter at the end of the rows (space)
报错格式1：
1403636580413555456,-0.01632,0.00815,-0.21970,-0.04041,0.83359,0.02732,0.55023,-0.04845,0.01219,-0.28032,
1403636580463555584,-0.01847,0.00887,-0.23163,-0.04029,0.83807,0.02782,0.54336,-0.04074,0.01526,-0.19377,
1403636580513555456,-0.02006,0.00961,-0.23880,-0.03989,0.84238,0.02801,0.53668,-0.02621,0.01464,-0.06092,
格式2：
1403636580 -0.01632 0.00815 -0.21970 -0.04041 0.83359 0.02732 0.55023 
1403636580 -0.01847 0.00887 -0.23163 -0.04029 0.83807 0.02782 0.54336 
1403636581 -0.02006 0.00961 -0.23880 -0.03989 0.84238 0.02801 0.53668
格式3：
1403636580963555584,-0.01127,0.01323,-0.01032,0.82282,0.02867,0.56731,-0.01741,
1403636581013555456,-0.01072,0.01428,0.02579,0.81861,0.02953,0.57334,-0.01685,
1403636581113555456,-0.01052,0.01519,0.09127,0.81059,0.02827,0.58463,-0.01883,

改源程序posegraph.cpp

​    if (SAVE_LOOP_PATH)
​        {
​            ofstream loop_path_file(VINS_RESULT_PATH, ios::app);
​            loop_path_file.setf(ios::fixed, ios::floatfield);
​            loop_path_file.precision(6);//时间戳精度
​            //loop_path_file << (*it)->time_stamp * 1e9 << ",";
​            loop_path_file << (*it)->time_stamp << " ";
​            loop_path_file.precision(9);//位姿态精度
​            loop_path_file  << P.x() << " "
​                  <<P.y() << " "
​                  << P.z() << " "
​                  << Q.w() << " "
​                  << Q.x() << " "
​                  << Q.y() << " "
​                  << Q.z() 
​                  << endl;
​            loop_path_file.close();
​        }

但是不知道为啥保存的结果后面几行格式变了
还是报错如上：
格式变得如下：
1403636761.5636 -0.6331 0.4081 -0.1077 -0.1100 0.8032 0.1583 0.5637
1403636761.7136 -0.6284 0.4365 -0.1046 -0.1203 0.7994 0.1497 0.5692
1403636761.8136 -0.6263 0.4532 -0.1006 -0.1293 0.8001 0.1427 0.5681
1403636761.9136 -0.6248 0.4655 -0.0947 -0.1304 0.8008 0.1414 0.5672
1403636762.0636 -0.6222 0.4749 -0.0828 -0.1112 0.7985 0.1536 0.5713
1403636762,-0.62555,0.48968,-0.06594,0.80410,0.16742,0.56342,-0.08916,
1403636762,-0.62700,0.49627,-0.06463,0.80898,0.16618,0.55657,-0.09037,

把含有逗号的删除后一切0k:

Loaded 36382 stamps and poses from: data.csv
Loaded 1366 stamps and poses from: vins_result_loop.txt
Synchronizing trajectories...
Found 1366 of max. 36382 possible matching timestamps between...
	data.csv
and:	vins_result_loop.txt

..with max. time diff.: 0.01 (s) and time offset: 0.0 (s).

Aligning using Umeyama's method...
Rotation of alignment:
[[-0.9048993  -0.42554641  0.00821641]
 [ 0.42548915 -0.90492936 -0.00786311]
 [ 0.01078139 -0.00361933  0.99993533]]
Translation of alignment:
[ 4.52514999 -1.4887612   0.85545997]

Scale correction: 1.0

Compared 1366 absolute pose pairs.

Calculating APE for translation part pose relation...

APE w.r.t. translation part (m)
(with SE(3) Umeyama alignment)

       max	0.443170
      mean	0.211338
    median	0.196105
       min	0.043851
      rmse	0.235135
       sse	75.523902
       std	0.103075

--------------------------------------------------------------------------------
Plotting results... 
/home/lyy/catkin_Evaluate/Evo/image13.png
/home/lyy/catkin_Evaluate/Evo/image14.png

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image13.png)

![image14](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image14.png)

##### 测试9：

ORB和VINS对比
evo_traj tum ORB_SaveTrajectory.txt yes_vins_result_loop.txt --ref=data.tum -p --plot_mode=xz

结果如下：

name:	yes_vins_result_loop

infos:	1366 poses, 80.369m path length, 181.100s duration

name:	ORB_SaveTrajectory

infos:	3642 poses, 83.078m path length, 182.800s duration

name:	data
infos:	36382 poses, 80.626m path length, 181.905s duration
/home/lyy/catkin_Evaluate/Evo/image15.png
/home/lyy/catkin_Evaluate/Evo/image16.png
/home/lyy/catkin_Evaluate/Evo/image17.png

![](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image15.png)

![image16](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image16.png)

![image17](/home/lyy/catkin_Evaluate/Evo/evo/my_pictures/image17.png)