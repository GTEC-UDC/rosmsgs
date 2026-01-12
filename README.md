# GTEC ROS Messages

This package contains a set of custom ROS message definitions used in several GTEC ROS nodes. The package supports both ROS 1 and ROS 2, with message definitions located in `msg-ros1/` and `msg-ros2/` directories respectively.

## Message Types

### Ranging Messages

* **`Ranging`** - Basic message that models a range value between a tag and an anchor, including RSS and error estimation.

* **`GenericRanging`** - Generic ranging message with anchor ID, tag ID, range, sequence number, and RX power.

* **`UWBRanging`** - Ultra-Wideband ranging message with detailed DW1000 parameters including raw range, bias correction, noise measurements, first path amplitude, CIR (Channel Impulse Response) data, and channel configuration.

* **`PozyxRanging`** - Ranging message for Pozyx tag/anchor systems. Encapsulates parameters provided by the DW1000, including ranging values, quality measurements, channel configuration, and angle information.

* **`PozyxRangingWithCir`** - Extended Pozyx ranging message that includes CIR (Channel Impulse Response) data.

* **`DWRanging`** - Ranging message for EBV1000 tag/anchor systems. Includes detailed DW1000 parameters such as noise measurements, first path amplitude, CIR data, and channel configuration.

* **`RangingDiff`** - Message for representing ranging differences or differential ranging measurements.

* **`ESP32S2FTMRanging`** - Ranging message for ESP32-S2 FTM (Fine Time Measurement) systems. Includes RTT (Round Trip Time) estimates, raw RTT values, distance estimates, and frame data.

* **`ESP32S2FTMFrame`** - Individual frame data for ESP32-S2 FTM ranging.

* **`ESP32S2FTMRangingExtra`** - Extended ESP32-S2 FTM ranging message with additional parameters.

### Radar Messages

* **`RadarCube`** - 3D radar data cube with FFT size, angle bins, and data array.

* **`RadarRangeAzimuth`** - 2D radar data with range and azimuth information, including number of range bins and virtual antennas.

* **`RadarRangeDoppler`** - 2D radar data with range and Doppler information.

* **`RadarFusedPointStamped`** - Timestamped fused radar point data.

### Event and Occupancy Messages

* **`DoorCounterEvent`** - Event message for door counter systems, including low-to-high and high-to-low transitions.

* **`ZoneOccupancy`** - Message for zone occupancy detection, including zone ID, target IDs, and count.

## Dependencies

* `std_msgs` - Standard ROS message types
* `geometry_msgs` - Geometry-related message types

## Building

### ROS 1 (Catkin)

```bash
catkin_make
# or
catkin build
```

### ROS 2 (Ament)

```bash
colcon build --packages-select gtec_msgs
```

## License

MIT License
