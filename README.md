# velo2cam_gz

Gazebo (Ignition/Gazebo Sim) models and worlds for benchmarking LiDAR-camera extrinsic calibration algorithms, as originally described in:

**Automatic Extrinsic Calibration Method for LiDAR and Camera Sensor Setups**  
[Jorge Beltrán](https://beltransen.github.io/), [Carlos Guindel](https://cguindel.github.io/), Arturo de la Escalera, Fernando García  
IEEE Transactions on Intelligent Transportation Systems, 2022  
**\[[Paper](https://ieeexplore.ieee.org/abstract/document/9733276)\] \[[Preprint](https://arxiv.org/abs/2101.04431)\]**

> This fork is a stripped down version of the original work which is available [here](https://github.com/beltransen/velo2cam_gazebo)

![gazebo screenshot](screenshots/velo2cam_calibration_setup.png)

## Package: `velo2cam_gz_worlds`

A single ROS 2 package providing Gazebo calibration target models and a simulation world.

```
velo2cam_gz_worlds/
├── models/                          # Gazebo calibration target models
│   ├── calibration_wood_pattern/    # Checkerboard on wood/maple texture
│   ├── calibration_whiteqr_pattern/ # White QR calibration target
│   ├── calibration_bigqr_pattern/   # Large QR calibration target
│   ├── checkerboard_5_8_0_2/        # 5×8 checkerboard (0.2 m squares)
│   ├── checkerboard_6_8_0_2/        # 6×8 checkerboard (0.2 m squares)
│   └── chess_plane/                 # Chess plane for KIT/
└── worlds/
    └── calibration_scene.world      # Default calibration scene
```

## Requirements

- ROS 2 (Jazzy or newer recommended)
- Gazebo Sim (formerly Ignition Gazebo) — `ros_gz_sim`

## Build

```bash
cd <your_ros2_ws>/src
git clone <this_repo>
cd ..
colcon build --packages-select velo2cam_gz_worlds
source install/setup.bash
```

After sourcing, `GZ_SIM_RESOURCE_PATH` is automatically extended to include the installed models and world.

## Usage

Launch the calibration scene:

```bash
gz sim $(ros2 pkg prefix velo2cam_gz_worlds)/share/velo2cam_gz_worlds/worlds/calibration_scene.world
```

Reference calibration target models by name in your own world files:

```xml
<include>
  <uri>model://calibration_wood_pattern</uri>
  <pose>2.0 0.0 1.1 0 0 3.14159</pose>
</include>
```

## Calibration Target Models

| Model | Description |
|-------|-------------|
| `calibration_wood_pattern` | Checkerboard on maple wood texture |
| `calibration_whiteqr_pattern` | White QR-style calibration target |
| `calibration_bigqr_pattern` | Large QR-style calibration target |
| `checkerboard_5_8_0_2` | 5×8 checkerboard, 0.2 m squares |
| `checkerboard_6_8_0_2` | 6×8 checkerboard, 0.2 m squares |
| `chess_plane` | Chess plane for KIT/Matlab calibration toolboxes |

## Known Issues

- Gazebo can take longer to load with large or complex meshes.

## Citation

This work is derived from the [original work](https://github.com/beltransen/velo2cam_gazebo) by Beltrán et al.
If you use this package, consider citing the original work:

```bibtex
@article{beltran2022,
  author  = {Beltrán, Jorge and Guindel, Carlos and de la Escalera, Arturo and García, Fernando},
  journal = {IEEE Transactions on Intelligent Transportation Systems},
  title   = {Automatic Extrinsic Calibration Method for LiDAR and Camera Sensor Setups},
  year    = {2022},
  doi     = {10.1109/TITS.2022.3155228}
}
```

