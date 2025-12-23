# GalaxyRVR Setup Guide

This guide will help you set up and run the GalaxyRVR autonomous navigation system, whether you're using the simulation environment or real hardware.

## Prerequisites

### Hardware Requirements (for real robot)
- GalaxyRVR robot chassis
- Arduino microcontroller
- Ultrasonic sensors (HC-SR04)
- IR sensors (GP2Y0A21YK0F)
- Onboard camera (USB or built-in)
- Overhead webcam
- Power supply
- USB cables for communication

### Software Requirements
- Python 3.8+
- OpenCV 4.0+
- NumPy
- PySerial
- Arduino IDE (for firmware upload)
- Git (for version control)

## Installation Steps

### 1. Clone the Repository

Clone the repository and navigate to the project directory.

### 2. Install Python Dependencies

Install the required Python dependencies from the respective requirements files.

### 3. Set Up Arduino Firmware

Open the Arduino IDE, navigate to the firmware directory, select your board and port, then upload the firmware.

## Quick Start

### Option 1: Simulation Mode (No Hardware Required)

Simulation mode allows you to test the navigation algorithms without physical hardware.

#### Run a Basic Simulation

Navigate to the autonomous navigation directory and run the simulation script.

#### Run with Custom Configuration

Run the simulation with custom configuration parameters.

#### Available Simulation Commands

- `--config <config_name>`: Choose simulation configuration (basic, complex, dynamic)
- `--speed <factor>`: Adjust simulation speed (1.0 = real time)
- `--visualize`: Enable real-time visualization
- `--output <file>`: Save simulation results to file

### Option 2: Real Hardware Mode

#### Connect the Hardware
1. Connect Arduino to computer via USB
2. Connect ultrasonic and IR sensors to Arduino
3. Connect cameras (onboard and overhead)
4. Power on the robot

#### Find the Arduino Port

Identify the Arduino port using system-specific commands.

#### Run the Navigation System

Navigate to the autonomous navigation directory and run the main navigation script with appropriate port settings.

#### Available Navigation Commands

- `--robot-port <port>`: Arduino port (e.g., /dev/ttyUSB0, COM3)
- `--webcam-port <port>`: Webcam port number (default: 0)
- `--mode <mode>`: Navigation mode (waypoint, line_follow, dynamic)
- `--speed <speed>`: Maximum robot speed (cm/s)

## Calibration

### Camera Calibration

Run the camera calibration script to calibrate the camera.

### Color Calibration for Target Detection

Run the color calibration script to calibrate target colors.

### Sensor Calibration

Run the sensor calibration scripts for ultrasonic and IR sensors.

## Testing

### Run Unit Tests

Run the unit tests to verify individual components.

### Run Integration Tests

Run the integration tests to verify system components work together.

### Run Visual Tests

Run the visual tests to verify visual processing capabilities.

### Run Simulation Tests

Run the simulation tests to verify simulation functionality.

## Troubleshooting

### Common Issues

1. **Robot not responding**
   - Check USB connection
   - Verify Arduino port
   - Ensure firmware is uploaded correctly

2. **Camera not working**
   - Check webcam port number
   - Ensure camera is not in use by another application
   - Test camera with other software

3. **Target detection failed**
   - Check lighting conditions
   - Recalibrate color targets
   - Verify target is within camera field of view

4. **Obstacle avoidance not working**
   - Check sensor connections
   - Recalibrate sensors
   - Verify sensor placement

### Log Files

Check the log files for debugging information.

## Next Steps

1. **Explore Simulation**: Try different simulation configurations
2. **Test with Real Hardware**: Set up and calibrate your robot
3. **Modify Navigation Algorithms**: Experiment with path planning parameters
4. **Add New Features**: Extend the system with custom functionality
5. **Contribute**: Share your improvements with the community

## Documentation

- [System Architecture](../architecture/ARCHITECTURE.md)
- [Navigation Features](../features/navigation.md)
- [Simulation Environment](../features/simulation.md)
- [Vision System](../features/vision.md)
- [Sensor Integration](../features/sensors.md)

## Support

If you encounter issues or have questions, please:
1. Check the troubleshooting section above
2. Review the documentation files
3. Look at example usage files
4. Contact the development team
