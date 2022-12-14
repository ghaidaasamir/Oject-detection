# Complex YOLOv4 3d Object detection

The PyTorch Implementation based on YOLOv4 of the paper: [Complex-YOLO: Real-time 3D Object Detection on Point Clouds](https://arxiv.org/pdf/1803.06199.pdf)<br/>
Comlpex Yolov4 used for 3D object detection to detect cars using pretrained model, trained on kitti dataset<br/>
**3D object car detection notebook**<br/>
# Yolov5 Pedestrians and Crosswalks detection

Detection of pedestrians, crosswalks and whether it's safe for cars to cross the crosswalk using green bounding boxes or unsafe to cross using red bounding boxes.<br/>
Yolov5 weights were used for detection of pedestrians <br/>
Training on custom dataset obtained using roboflow tool to detect crosswalks<br/>
Yolov5 custom trained weights (best.pt) weights were used for detection of crosswalks<br/>
TensorBoard tool was used for providing the measurements and visualizations needed during the training workflow for tracking experiment metrics like loss and accuracy and precision/recall graphs.<br/>
**Pedestrians and Crosswalks detection notebook**<br/>



## Data Preparation

3D KITTI detection dataset  [here](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d).

- Camera calibration matrices of object data set (16 MB)
- Training labels of object data set (5 MB)
- Velodyne point clouds (29 GB)
- Left color images of object data set (12 GB)

Crosswalk dataset

- 20 images and labels for training
- 9 images and labels for validation  
- 100 images for testing

## Folder structure for Complex YOLOv4 3d Object detection

```
${ROOT}
└── checkpoints/    
    ├── complex_yolov3/
    └── complex_yolov4/
└── src/
    ├── config/
    ├── cfg/
        │   ├── complex_yolov3.cfg
        │   ├── complex_yolov3_tiny.cfg
        │   ├── complex_yolov4.cfg
        │   ├── complex_yolov4_tiny.cfg
    │   ├── train_config.py
    │   └── kitti_config.py
    ├── data_process/
    │   ├── complex_yolov4_mse_loss.pth
    │   ├── kitti_bev_utils.py
    │   ├── kitti_dataloader.py
    │   ├── kitti_dataset.py
    │   ├── kitti_data_utils.py
    │   ├── train_val_split.py
    │   └── transformation.py
    ├── models/
    │   ├── darknet2pytorch.py
    │   ├── darknet_utils.py
    │   ├── model_utils.py
    │   ├── yolo_layer.py
    └── utils/
    │   ├── evaluation_utils.py
    │   ├── iou_utils.py
    │   ├── logger.py
    │   ├── misc.py
    │   ├── torch_utils.py
    │   ├── train_utils.py
    │   └── visualization_utils.py
    └── dataset/kitti/
        ├──ImageSets/
        │   ├── train.txt
        │   └── val.txt
        │   └── test.txt <-- list of names of test data
        ├── training/
        │   ├── image_2/ <-- for visualization
        │   ├── calib/
        │   ├── label_2/
        │   └── velodyne/
        └── testing/  
        │   ├── image_2/ <-- for visualization
        │   ├── calib/
        │   └── velodyne/ 
        └── classes_names.txt
    ├── test.py
    ├── test.sh
    ├── train.py
    └── train.sh
├── README.md 
└── requirements.txt
```


Data Format Description for 3d object detection 
===================================================
The data for training can be found in the corresponding folders.<br/>
The sub-folders are structured as follows:<br/>

  - image_02/ contains the left color camera images (png)<br/>
  - label_02/ contains the left color camera label files (plain text files)<br/>
  - calib/ contains the calibration for all five cameras (plain text file)<br/>
  - velodyne/ contains the velodyne point cloud (bin)<br/>
  
```
Values    Name      Description
----------------------------------------------------------------------------
   1    type         Describes the type of object: 'Car', 'Van', 'Truck',
                     'Pedestrian', 'Person_sitting', 'Cyclist', 'Tram',
                     'Misc' or 'DontCare'
   1    truncated    Float from 0 (non-truncated) to 1 (truncated), where
                     truncated refers to the object leaving image boundaries
   1    occluded     Integer (0,1,2,3) indicating occlusion state:
                     0 = fully visible, 1 = partly occluded
                     2 = largely occluded, 3 = unknown
   1    alpha        Observation angle of object, ranging [-pi..pi]
   4    bbox         2D bounding box of object in the image (0-based index):
                     contains left, top, right, bottom pixel coordinates
   3    dimensions   3D object dimensions: height, width, length (in meters)
   3    location     3D object location x,y,z in camera coordinates (in meters)
   1    rotation_y   Rotation ry around Y-axis in camera coordinates [-pi..pi]
```


Data Format Description for pedestrians and crosswalk object detection 
==========================================================================
The data for training of crosswalk can be found in the corresponding folder.<br/>
Crosswalk folder:<br/>

  - images/ contains images of crosswalks<br/>
  - labels/ contains label files (2d bounding boxes)<br/>
  - data.yaml/ contains the directory of train and validation data, number and name of classes (crosswalk)<br/>
 
