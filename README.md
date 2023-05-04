# clearpath_config
Clearpath Configuration YAML Parser

# Configration Examples
## A200 Sample Configuration
You can find the following file under `/sample/a200_config.yaml`:
```yaml
system: # These are system level configs
    self: A200-1
    hosts: # These are the hosts that are involved in this system
        platform: # The main computer for this system, ie the robot's computer
            A200-1: 192.168.131.1
        onboard: # These are additional on-board computers such as a secondary computer or software kit
            A200-B: 192.168.131.5
            ONAV-KIT: 192.168.131.10
        remote: # These are remote machines which need to interact with this system such as laptops or other robots
            CPR12345: 10.10.10.101
            USERS-PC: 10.10.10.1
    ros2:
        namespace: HOSTNAME
        domain_id: 123
        rmw_implementation: rmw_fastrtps_cpp

platform: # These are are parameters specific to a a platform
    serial_number: cpr-a200-0001
    controller: logitech # ps4 or logitech
    decorations: # Platform specific accessories
        front_bumper:
            extension: 0.1
            model: wibotic
            xyz: [0.0, 0.0, 0.0]
            rpy: [0.0, 0.0, 0.0]
        rear_bumper:
            extension: 0
            model: default
            xyz: [0.0, 0.0, 0.0]
            rpy: [0.0, 0.0, 0.0]
        top_plate:
            model: pacs
            xyz: [0.0, 0.0, 0.0]
            rpy: [0.0, 0.0, 0.0]
        structure:
            model: sensor_arch_510
            xyz: [0.0, 0.0, 0.0]
            rpy: [0.0, 0.0, 0.0]
    extras:
        urdf: /fake/path/empty.urdf.xacro
        control: /fake/path/empty.yaml

accessories:
    link:
      - name: test_link
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
    box:
      - name: test_box
        size: [0.01, 0.01, 0.01]
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
    cylinder:
      - name: test_cylinder
        radius: 0.01
        length: 0.01
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
    sphere:
      - name: test_sphere
        radius: 0.01
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
    mesh:
      - name: test_mesh
        visual: fake_mesh.stl
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]

mounts:
    fath_pivot:
      - parent: "top_plate_mount_a1"
        angle: 1.5707
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
      - parent: "top_plate_mount_a2"
        angle: 0.0
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
    flir_ptu:
      - {}
      - {}
    riser:
      - rows: 8
        columns: 7
        thickness: 0.00635
        parent: "top_plate_mount_a1"
        xyz: [0.0, 0.0, 0.1]
        rpy: [0.0, 0.0, 0.0]
      - rows: 1
        columns: 7
        thickness: 0.00635
        parent: "top_plate_mount_a6"
        xyz: [0.0, 0.0, 0.2]
        rpy: [0.0, 0.0, 0.0]
    bracket:
      - model: "horizontal"
        parent: "riser_1_mount_g6"
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
      - model: "vertical"
        parent: "riser_1_mount_a6"
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]

# Sensors: grouped by sensor types.
#  - model: unique model of that sensor type
#  - urdf_enabled: toggle to add model to description
#  - launch_enabled: toggle to add node to launch file
sensors:
    # List of Cameras
    camera:
      - model: flir_blackfly
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          connection_type: USB3
          encoding: BayerRG8
          fps: 30
          serial: 0
      - model: intel_realsense
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          serial_no: 12345
          device_type: d435
          enable_color: true
          rgb_camera:
            profile: "640,480,30"
          enable_depth: true
          depth_module:
            profile: "640,480,30"
          pointcloud:
            enable: true
          anything: true
    gps:
      - model: swiftnav_duro
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          ip_address: 192.168.131.30
          port: 55555
          gps_receiver_frame_id: duro
          imu_frame_id: duro
    lidar3d:
      - model: velodyne_lidar
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          device_ip: 192.168.131.20
          port: 2368
          model: VLP16
    lidar2d:
      - model: sick_lms1xx
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          hostname: 192.168.131.20
          port: 6000
          min_ang: -3.1415
          max_ang: 3.1415
      - model: hokuyo_ust10
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          ip_address: 192.168.131.21
          ip_port: 6000
          angle_max: -3.1415
          angle_min: 3.1415
    imu:
      - model: microstrain_imu
        urdf_enabled: true
        launch_enabled: true
        parent: base_link
        xyz: [0.0, 0.0, 0.0]
        rpy: [0.0, 0.0, 0.0]
        ros_parameters:
          imu_frame_id: test_link
          port: /dev/test
          use_enu_frame: false

```

# Unit Tests
All unit tests are written using **PyTest** following the [Good Integration Practices](https://docs.pytest.org/en/6.2.x/goodpractices.html#goodpractices).

Therefore, `clearpath_config_test` is a package that mirrors the `clearpath_config` package structure. Each file from `clearpath_config` that is to be tested should have a corresponding file with the same name and the suffix `_test.py`.

To run the tests:
```bash
cd .../clearpath_config
python3 -m pytest
```
> **PyTest** will automatically search for the suffix `_test` throughout the current directory and run the tests.
