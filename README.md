<div align="center">
  <h1>OctoMap Server2</h1>
  <h3>Implementation of octomap for ROS2.0 </h3>
    <a href="https://travis-ci.com/iKrishneel/octomap_server2"><img src="https://travis-ci.com/iKrishneel/octomap_server2.svg?branch=master"></a>
</div>

Port of the ROS1 [octomap server](https://github.com/OctoMap/octomap_mapping) for ROS2.0 

#### Installation
Firstly make sure you have [octomap](https://github.com/OctoMap/octomap.git) installed on your system 

Next, clone this ros package to the appropriate ros2 workspace
```bash
$ git clone https://github.com/iKrishneel/octomap_server2.git
```
Clone the dependency repositories to the workspace
```bash
# will clone octomap_msgs to the workspace
$ vcs import . < deps.repos
```

#### Building
Use colcon to build the workspace
```bash
$ colcon build --symlink-install --packages-select octomap_msgs octomap_server2
```

#### Running
Launch the node with appropriate input on topic `cloud_in`
```bash
$ ros2 launch octomap_server2 octomap_server_launch.py
```

## Changelog by DeepX

1. Several PRs to make the fork work on ROS 2.
2. [Silence periodic debug logs (#6)](https://github.com/DeepX-inc/octomap_server2/commit/854f2cd7c14e5094ad1cbd76adb5de28303f0de9): Convert periodic spam logs to use DEBUG level.
3. Add `~/heartbeat` publisher ([4739b33](https://github.com/DeepX-inc/octomap_server2/commit/4739b33deab7f781bbf4c94c85c6d75c2952e628), [e1ab37d](https://github.com/DeepX-inc/octomap_server2/commit/e1ab37db151275027835698af499e72d3b214641)).
   1. Message type: [std_msgs::Header](https://docs.ros2.org/latest/api/std_msgs/msg/Header.html) (`frame_id` field is not used).
   2. Published periodically at 10 Hz (default).
   3. Publication period can be configured with the `heartbeat_period_ms` parameter.
4. [Disable parameter services (#8)](https://github.com/DeepX-inc/octomap_server2/commit/cef67a4cba0baf1cdedd5c7c297c52c0c8b41428): To mitigate network load due to DDS discovery over WiFi.
5. [Add health metrics for in/out PCD topics #10](https://github.com/DeepX-inc/octomap_server2/pull/10):
   1. Add `~/health/cloud_in` publisher: Signal that the `cloud_in` callback has been triggered.
   2. Add `~/health/cloud_out` publisher: Signal that `octomap_point_cloud_centers` has been published.
   3. Add `publish_health_metrics` boolean parameter (default: `false`).
   4. Message type: [std_msgs::Header](https://docs.ros2.org/latest/api/std_msgs/msg/Header.html) (`frame_id` field is not used).
