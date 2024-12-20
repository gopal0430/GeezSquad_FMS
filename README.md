Chainer Realtime Multi-Person Pose Estimation
Based on the paper Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields, we implement a model to recognize FMS movements (Deep Squat, Hurdle Step, In-line Lunge, Active Straight-leg Raise, Trunk Stability Push-up, Rotary Stability, Shoulder Mobility) and measure posture with the goal of creating an evaluation index similar to the FMS score.

time
Converting caffe model
Testing
About FMS
Requirements
Python 3.0+
Chainer 2.0+
NumPy
Matplotlib
OpenCV
Convert Caffe model to Chainer model
You can convert it by referring to the caffe model in the referenced project .

> cd models
> wget http://posefs1.perception.cs.cmu.edu/OpenPose/models/pose/coco/pose_iter_440000.caffemodel
> wget http://posefs1.perception.cs.cmu.edu/OpenPose/models/face/pose_iter_116000.caffemodel
> wget http://posefs1.perception.cs.cmu.edu/OpenPose/models/hand/pose_iter_102000.caffemodel

> python convert_model.py posenet pose_iter_440000.caffemodel coco_posenet.npz
> python convert_model.py facenet pose_iter_116000.caffemodel facenet.npz
> python convert_model.py handnet pose_iter_102000.caffemodel handnet.npz
Test using the trained model
First, we use the existing trained model with image files to evaluate whether the motion is recognized properly.

> python pose_detector.py posenet models/coco_posenet.npz --images data/image/deep_squat.jpg data/image/hurdle_step.jpg data/image/in_line_lunge.jpg data/image/rotary_stability.jpg
If your GPU is supported, --gpuyou can use the option.

> python pose_detector.py posenet models/coco_posenet.npz --images data/image/deep_squat.jpg data/image/hurdle_step.jpg data/image/in_line_lunge.jpg data/image/rotary_stability.jpg --gpu 0
   
   
   
   
If your computer supports a camera, you can perform a real-time motion recognition test. And you can analyze the video. To exit, qjust press .

> python video_pose_detector.py --video data/video/hurdle_step_video.mp4

About FMS
This is a movement pattern assessment designed to evaluate stability and mobility created by Cook. It is an examination method that can evaluate joint restrictions, imbalances, asymmetries, and compensations through seven movement patterns using extreme postures that show imbalances and weaknesses.

The process is as follows.

Through 7 movement movements (Deep Squat, Hurdle Step, In-line Lunge, Active Straight-leg Raise, Trunk Stability Push-up, Rotary Stability, Shoulder Mobility), functional problems in body movement are identified and scored.
The full score for each item is 3 points.
If the total score after the 7 movement tests is 14 points or less, it can be determined that a physical problem is exposed and the physical problem can be improved through corrective exercises.
*. FMS can check mobility, stability, and movement patterns.

ASLR, SM tests the range of motion of joints, the length of tissues and the flexibility of muscles.
Stability exercises (TSPU, RS) target postural control at the start and end positions of each movement pattern.
Movement Patterns (DS, HS, IL) integrate the use of fundamental mobility and stability into specific movement patterns to enhance coordination and timing.
Reference Repository
CVPR'16, Convolutional Pose Machines.
CVPR'17, Realtime Multi-Person Pose Estimation.
Citation
Please cite the original paper in your publications if it helps your research:

@InProceedings{cao2017realtime,
  title = {Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields},
  author = {Zhe Cao and Tomas Simon and Shih-En Wei and Yaser Sheikh},
  booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  year = {2017}
 }