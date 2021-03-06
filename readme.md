## readme 

This repo is used in OrcVIO [project website](http://me-llamo-sean.cf/orcvio_githubpage/), [Journal version](https://arxiv.org/abs/2007.15107)

If you find this repo useful, kindly cite our publications 

```
@article{orcvio,
  title={OrcVIO: Object residual constrained Visual-Inertial Odometry},
  author={M. {Shan} and Q. {Feng} and N. {Atanasov}},
  url = {http://erl.ucsd.edu/pages/orcvio.html},
  pdf = {https://arxiv.org/abs/2007.15107},
  journal={IEEE Transactions on Robotics},
  volume={},
  number={},
  pages={},
  year={2021},
  publisher={IEEE}
}    
```

## about  

* this repo implements bbox tracking using sort
* original version uses IOU, but if the overlap is 0, cannot re-identify the same object and lead to ID switch 
* this version add centroid distance, so that we could use a threshold to determine whether the two centroids belong to the same object 

## dependencies 

- opencv
- [catkin simple](https://github.com/catkin/catkin_simple)
- [darknet ros](https://github.com/leggedrobotics/darknet_ros)
- [darknet ros bridge](https://github.com/shanmo/OrcVIO-Darknet-ROS)
- [wm_od_interface_msgs](https://github.com/kschmeckpeper/object_detection/tree/main/wm_od_interface_msgs) or [this link](https://github.com/shanmo/OrcVIO-Darknet-ROS)

## how to run 

- to run demo, download [outdoor_demo_test_2020-11-04-15-48-26.bag](https://drive.google.com/file/d/1IGFBNmGfRKs2cQgWPY9BtWZwlkCk4hi8/view?usp=sharing), [MIT video demo](https://drive.google.com/file/d/1CaUvrl5Zv_wmZtFvNYnEU4-qYAkV2R-y/view?usp=sharing)
```script
roslaunch sort_ros sort_ros_test_dcist.launch
```

- another demo is using [medfield_ft2_2020-11-06-11-58-28.bag](https://drive.google.com/file/d/1pSXG3R4_fK4BxNGixZNyEFWh3uliUKMg/view?usp=sharing), and video is [Medfield demo video](https://drive.google.com/file/d/15JFBNeN7NzU752RM2gZVeDb-7FRbVQqO/view?usp=sharing)

## notes 

* we only track valid class, e.g. barrel, which can be set in `gen_class` function 
* the `centroid_dist_threshold` determines whether we consider two centroids belong to same object, which can be tuned in launch file. set to a large value if we only need to detect barrels to accommodate jackal's aggressive motion 
* the output topic is `/SortRos/tracked_bbox`, here is the output from `rostopic echo /SortRos/tracked_bbox`

```
header: 
  seq: 49
  stamp: 
    secs: 1317067372
    nsecs: 169100046
  frame_id: "tracked bboxes"
bounding_boxes: 
  - 
    xmin: 433
    ymin: 164
    xmax: 455
    ymax: 453
    id: 18
    Class: "car"
    lost_flag: False
```

## references 

- https://github.com/tryolabs/norfair
