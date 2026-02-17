# REU-EventTriggeredSensing
Event-Triggered, Gesture-Assisted Human-Following Robot with Angle-Based Continuous Motion Control

# Objective
The goal of this project is to develop a semi-autonomous mobile robot that can:
Implement a four wheels robot based ROS2 
Autonomously follow a human under normal conditions
Safely recover from tracking failure
Request human assistance only when necessary
Be controlled using angle-based hand gestures for smooth and natural robot motion
The system focuses on robust tracking, safe recovery, and human-in-the-loop intervention under uncertainty, rather than building low-level detection models from scratch.

# Core System Concept
The robot operates mostly autonomously but switches to human guidance when tracking becomes unreliable.
Two-Level Intelligence
Autonomous Mode (Normal Operation)
Event-Triggered Human Assistance Mode
System States (4-State Machine)

1. Following State
Detect and track nearest human legs (LiDAR / vision)
Maintain safe distance using feedback control
Keep target centered using heading control
Control methods:
PID / PD / Visual Servoing / Pure Pursuit (alternative to PID)

2. Obstacle Avoidance State
Detect obstacles using LiDAR
Avoid collision
Use IMU to remember rotation angle
Return to original orientation after avoidance

3. Detecting (Re-acquisition) State
When target is lost:
Move toward last known direction for ~5 seconds
Efficient re-acquisition after tracking loss

4. Event State (Human-in-the-Loop)
Activated when:
Target lost
Safety uncertain
No detection for X seconds
Confidence below threshold
User guides robot using webcam-based hand gestures.
Once target is detected again → return to Following.

# Gesture Control System
Input
Webcam + MediaPipe Hand Tracking
Control Method (Angle-Based)
Hand Motion	Robot Behavior
Key feature: 
Continuous steering via gesture angle → differential wheel velocity

# Technical Components
1. Sensors
RGB camera 
LiDAR 
IMU
2. Software
ROS (robot control framework)
MediaPipe 
Existing human/leg detection models 
State machine controller
velocity control

# Control Strategy
Differential drive motion
Smooth velocity modulation
Curvature control via gesture angle
Safety-aware switching logic
Confidence / uncertainty thresholding

# Research Focus (Main Contribution)
Instead of building detectors, the project focuses on:
Efficient Re-acquisition After Tracking Loss
Event-Triggered Human Assistance
Safety-Aware Following Under Uncertainty
Human-Robot Shared Control
Angle-Based Continuous Gesture Steering

# Evaluation Metrics
Tracking success rate
Recovery time after loss
Gesture control accuracy
Real-time responsiveness
Safety (collision / instability)
Human intervention frequency

# Expected Outcome
A robust semi-autonomous robot that:
Follows a human safely
Recovers intelligently from failure
Uses human help only when necessary
Supports smooth gesture-based teleoperation
Demonstrates reliable real-time performance

# Optional Extension (Future Work)
Cross-platform transfer (ground robot → drone)
Confidence-aware adaptive control
Learning-based uncertainty estimation
Multi-modal human guidance (gesture + voice)
