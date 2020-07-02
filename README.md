## UAV-Vehicle-Detection-Dataset

### For step by step fine-tuning the vehicle detector, please refer to [Fine-tune-YOLOv3](https://github.com/jwangjie/Fine-tune-YOLOv3)
---

There are plenty of proposed datasets for training CNN based vehicle detector, also many pre-trained weights that can be directly applied for the vehicle detection tasks. Because the majority of the vehicle detections tasks were conducted on or near the ground, these image datasets were collected by ground vehicles or CCTV cameras. However, vehicle detectors trained on these datasets collected by the ground cameras perform badly for the vehicle detections in UAV video applications, image datasets created from UAV videos are needed for creating a reliable traffic monitoring pipeline on UAVs.
We conducted fine-tuning on YOLOv3 using the [aerial-cars-dataset](https://github.com/jekhor/aerial-cars-dataset). The trained CNN vehicle detector recognized most vehicles near the UAV camera, but not vehicles far away from the camera. This is due to the training dataset contains bird's-eye view images only. 

Images of the M0606 of [UAV-benchmark-M](https://sites.google.com/site/daviddo0323/projects/uavdt) were added to train the CNN, the improvement was very limited. This is because the dataset was created by labeling cars near to the cameras only, cars far away from the cameras were ignored. Another reason is images resolution of both [aerial-cars-dataset](https://github.com/jekhor/aerial-cars-dataset) and [UAV-benchmark-M](https://sites.google.com/site/daviddo0323/projects/uavdt) are relatively low (1024x540) compared to our aerial videos (2720x1530). 

A new dataset was created by labeling our UAV video images. The final dataset used for fine-tuning YOLOv3 vehicle detector is composed of **154** images from [aerial-cars-dataset](https://github.com/jekhor/aerial-cars-dataset), 1374 images from the [UAV-benchmark-M](https://sites.google.com/site/daviddo0323/projects/uavdt), and our custom labeled 157 images. The complete dataset is provided in dataset1, dataset2, dataset3, and dataset4.

### Here are the key steps of fine tuning our UAV vehicle detector: 

  1. **Install YOLOv3:** [AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)   
     
     a.	For cuda complie issues: execute this [line](https://github.com/pjreddie/darknet/issues/200#issuecomment-329692411) `export     PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}`, before `make`
     
  2. **Install OpenCV:** NOT opencv-python! following [How to install OpenCV 3.4.0 on Ubuntu 16.04](https://www.pytorials.com/how-to-install-opencv340-on-ubuntu1604/)
  
  3. **Custom dataset labeling:** the dataset is created from our aerial videos by [Yolo_mark](https://github.com/AlexeyAB/Yolo_mark)
  
  4. **Fine-tune YOLOv3:** [How to Train](https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects)
     
     a. if error `Out of memory` shows, in `.cfg-file`, increase `subdivisions = 16, 32 or 64` following [this](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L4)
     
Important command lines:

**Training:**  `./darknet detector train data/dji.data cfg/yolov3_dji.cfg darknet53.conv.74`

**Testing:**  `./darknet detector demo data/dji.data cfg/yolov3_dji.cfg backup/yolov3_dji_final.weights DJI_0003.MOV -out_filename DJI_0003_dji.avi`

---  
##### The whole dataset can also be downloaded at [here](https://drive.google.com/file/d/10rZw87pUsLurctEfLeWgYbj_pYn54S9o/view?usp=sharing).

## Reference
Please kindly cite this paper in your publications if this helps your research:

```
@article{wang2019orientation,
  title={Orientation-and Scale-Invariant Multi-Vehicle Detection and Tracking from Unmanned Aerial Videos},
  author={Wang, Jie and Simeonova, Sandra and Shahbazi, Mozhdeh},
  journal={Remote Sensing},
  volume={11},
  number={18},
  pages={2155},
  year={2019},
  publisher={Multidisciplinary Digital Publishing Institute}
}
```
