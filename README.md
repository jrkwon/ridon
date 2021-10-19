# Ridon - BIMI Vehicle

The Ridon - BIMI Vehicle is a ROS workspace for a Drive-By-Wire system for a scaled vehicle.

## Contributors
- Jaerock Kwon, Ph.D., Assistant Professor at University of Michigan-Dearborn
- Girma Tewolde, Ph.D., Professor at Kettering University
- Aws Khalil, Ph.D. student at University of Michigan-Dearborn
- Shobit Sharma, MS student at Kettering University
- Ahmed Essam AbdELhamed, MS student at Kettering University
- Li Dang, MS student at Kettering University

## Folder Structure

- `arduino_driver`: I2C master/slave code
- `evaluation`: drift evaluation from the center
- `train`: neural network training module
- `src`
  - `data_acquisition`: data collection
  - `joy_control`: joy stick control 
  - `bimi_bmw`: 
  - `bimi_bmw_urdf`: robot description file for 'bmw' model
  - `realsense-2.2.0`: Intel Real Sense driver
  - `run_model`: steering angle prediction module using a trained neural network model

## Environment

The `bimi_vehicle` runs with ROS Melodic on Ubuntu 18.04 LTS.

## Data Collection 

The image data locations for the collected images can be configured at 
`src/data_acquisition/config/parameters.yaml`.

```
$ roslaunch bimi_vehicle data_acquisition.launch
```

## Training a Neural Network

```
$ cd /path/to/ridon/train
$ python train.py /path/to/data/folder <network_model_name>
```

`<network_model_name>` will be used to create a trained network model. 

## Running the trained model

To launch the vehicle model in Gazebo

```
$ roslaunch bimi_vehicle bringup.launch
```

To control the vehicle using the trained model, open another terminal and execute the below commands.

```
$ roslaunch bimi_vehicle model_run.launch
```
By default, `model_run` runs `camera_model`. You need to change the module name, `camera_model_run.py` inside `model_run.launch` to `lidar_model_run.py`.

## Acknowledgements

This project was possible with the works of Kettering University's `mir_vehicle`, Arizona University's the CAT Vehicle Testbed, and Dataspeed Inc's ADAS system (dbw_mkz).


