# SDBNetV2: Short-term Dense Bottleneck Network for Real-time Semantic Segmentation 
This is an official site for SDBNetV2 model. Currently, the model predictions and supplimentary materials are uploaded. Upon the acceptance of the paper, this repository will be updated.

## Datasets
For this research work, we used six different datasets for outdoor and indoor scene analysis.
# Outdoor datasets:
* Cityscapes - To access this benchmark, user needs an account. For test set evaluation, user needs to upload all the test set results into the server. https://www.cityscapes-dataset.com/downloads/ 
* BDD100K - To access this benchmark, user needs an account. Here is the link for this dataset: https://doc.bdd100k.com/download.html#k-images
* KITTI - To access this benchmark, user needs an account. Like Cityscapes, user needs to submit the test set result to the evaluation server.  http://www.cvlibs.net/datasets/kitti/eval_semseg.php?benchmark=semantics2015    
* CamVid - To access this benchmark, visit this link: http://mi.eng.cam.ac.uk/research/projects/VideoRec/CamVid/
* IDD and IDD-lite - To access this benchmark, user needs an account. Here is the link for this dataset: https://idd.insaan.iiit.ac.in/dataset/details/

# Indoor datasets:
* Indoor objects - To access this benchmark, visit the following link: https://data.mendeley.com/datasets/hs5w7xfzdk/3

## Class mapping
Different datasets provide different class annotations. For instance, Camvid dataset has 32 class labels. Refer this link to know about all 32 classes of Camvid: http://mi.eng.cam.ac.uk/research/projects/VideoRec/CamVid/#ClassLabels. However, literature have shown that all the existing models are trained by 11 classes (Sky, Building, Pole, Road, Sidewalk, Tree, TrafficLight, Fence, Car, Pedestrian, Bicyclist) of Camvid dataset. Thereby, first 32 class annotations of Camvid are converted into 11 class annotations and then model is trained with 11 class annotations. To improve model performance, we also converted Cityscapes 19 class annotations to 11 class anotation and trained the model first with Cityscapes 11 class annotation, then use the pre-trained weight of Cityscapes to train the model with Camvid 11 class annotations. The following table shows the convertion of 32 classes of Camvid dataset to 11 classes.

TrainId | Camvid 11 classes  | Camvid 32 classes   
--------|--------------------|-------------------
   0    |        Sky         | Sky
   1    |     Building       | Archway, Bridge, Building, Tunnel, Wall
   2    |    Column_Pole     | Column_Pole, Traffic Cone
   3    |        Road        | Road, LaneMkgsDriv, LaneMkgsNonDriv  
   4    |      Sidewalk      | Sidewalk, ParkingBlock, RoadShoulder 
   5    |        Tree        | Tree, VegetationMisc
   6    |   TrafficLight     | TrafficLight, Misc_Text, SignSymbol  
   7    |       Fence        | Fence
   8    |        Car         | Car, OtherMoving, SUVPickupTruck, Train, Truck_Bus 
   9    |     Pedestrian     | Animal, CartLuggagePram, Child, Pedestrain   
  10    |     Bicyclist      | Bicyclist, MotorcycleScooter
  
  Note: Void class is not included in the set of 11 classes.
  
  The following table shows the mapping of Cityscapes 19 classes to Camvid 11 classes.
  
TrainId | Camvid 11 classes  | Cityscapes classes   
--------|--------------------|-------------------
   0    |        Sky         | Sky
   1    |     Building       | Building, Wall
   2    |    Column_Pole     | Pole, Polegroup
   3    |        Road        | Road  
   4    |      Sidewalk      | Sidewalk 
   5    |        Tree        | Vegetation
   6    |   TrafficLight     | Traffic Light, Traffic Sign  
   7    |       Fence        | Fence
   8    |        Car         | Car, Truck, Bus, Caravan 
   9    |     Pedestrian     | Person   
  10    |     Bicyclist      | Rider, Bicycle, MotorCycle

The following table shows the mapping of Cityscapes 19 classes to IDD-lite 7 classes.
  
TrainId | IDD-lite 7 classes   |           Cityscapes classes   
--------|----------------------|---------------------------------------------
   0    |      Drivable        |                 Road
   1    |     Non-drivable     |                Sidewalk
   2    |    Living-things     |              Person, Rider
   3    |       Vehicles       |  Motorcycle, Bicycle, Car, Truck, Bus, Train  
   4    |   Roadside objects   |  Wall, Fence, Traffic sign, Traffic light, Pole 
   5    |     Far Objects      |           Building, Vegetation
   6    |         Sky          |        Traffic Light, Traffic Sign  

## Metrics
To understand the metrics used for model performance evaluation, please  refer here: https://www.cityscapes-dataset.com/benchmarks/#pixel-level-results

## Results
We trained our model by the above mentioned benchmarks at different input resolutions. For Cityscapes and KITTI datasets, we use 19 classes, however for Camvid dataset we trained the model with 11 classes (suggested by the literature). The following table exhibits the test results achieved by SDBNet.

Dataset    | No. of classes  | Input Size  |  Val/Test mIoU  | No. of parameters | FLOPs   
-----------|-----------------|-------------|-----------------|-------------------|--------
Cityscapes |        19       | 1024 * 2048 |  72.4% (test)   |    1.5 million    | 44.4 G
BDD100K    |        19       |  768 * 1280 |  57.0%  (val)   |    1.5 million    | 20.8 G
KITTI      |        19       |  384 * 1280 |  56.8% (test)   |    1.5 million    | 10.4 G
Camvid     |        11       |  640 * 896  |  75.0% (test)   |    1.5 million    | 12.1 G
IDD-lite   |         7       |  128 * 256  |  71.3% (val)    |    1.5 million    |  0.7 G
IDD        |         7       |  128 * 256  |  72.7% (val)    |    1.5 million    |  0.7 G
Indoor ob. |         9       |  768 * 1408 |  60.4% (val)    |    1.5 million    | 22.9 G

### Cityscapes test results
The output of the test set is submitted to Cityscapes evaluation server. To view the test set result evaluated by the server, click the following link: https://www.cityscapes-dataset.com/anonymous-results/?id=4d35fe35555ed7b145ebcaaa6d45275b5ea3e1a18c6cf43734a8d7bde6495224
This is an anonymous link given by the Cityscapes server. Upon the acceptance of the paper, test result will be cited by the paper and will be published in the evaluation server.

### KITTI test set results
Like Cityscapes, KITTI test set result is also sumbitted to the evaluation server. Click the following link to see the result:
https://github.com/tanmaysingha/SDBNetV2/blob/main/other_files/best_results_KITTI_mIoU.pdf

### Color map of Cityscapes dataset and model prediction using validation sample
![cityscapes_val_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/City_color_map.png?raw=true)  

### Color map of CamVid dataset and model prediction using validation sample
![CamVid_val_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/camvid_color_map.png?raw=true)

### Color map of IDD-lite dataset and model prediction using validation sample
![IDDLite_val_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/color_map_IDD.png?raw=true)

### Color map of Indoor objects dataset and model prediction using validation sample
![Indoor_val_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/color_map_indoor.png?raw=true)

### SDBNetV2 prediction on Cityscapes test samples
![Cityscapes_test_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/city_test_pred.png?raw=true)

### SDBNetV2 prediction on BDD100K test samples
![BDD100K_test_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/BDD_test_pred.png?raw=true)

### SDBNetV2 prediction on CamVid validation sample
![CamVid_val_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/fig_CamVid_test.png?raw=true)

### SDBNetV2 prediction on KITTI test samples
![KITTI_test_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/fig_KITTI_test.png?raw=true)

### SDBNetV2 prediction on IDD-lite validation samples
![IDDLite_test_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/Idd_lite_test_pred.png?raw=true)

### SDBNetV2 prediction on IDD (part1 and part2) and Cityscapes validation samples
![IDD_City_test_set](https://github.com/tanmaysingha/SDBNetV2/blob/main/Figures/IDD_Cityscapes_1ID_pred.png?raw=true)
