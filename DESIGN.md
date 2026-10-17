# BikeGuard Pro: Design

## Problem Statement

University students frequently rely on bicycles and electric bikes to commute to campus and travel between distant buildings to attend classes. Because these items are often parked in high-traffic, outdoor areas on campus, they face continuous exposure to theft and vandalism. According to UBC Vancouver's [2024 Campus Security Report](https://bog3.sites.olt.ubc.ca/files/2025/05/14ii_2025.06_Campus-Security-Annual-Report-UBCV.pdf), 96 bicycle theft incidents were reported to Campus Security in 2024, compared with 86 in 2023.

Although conventional bicycle locks provide a physical layer of security, they do not provide real-time alerts when the bicycle is being tampered with.  Students attending lectures, laboratory sessions, or other campus activities are often unable to monitor their bicycles throughout the day. Consequently, the lack of real-time information can result in financial loss, transportation disruptions, and anxiety about leaving personal transit items unattended.

## Solution

BikeGuard Pro is a bicycle monitoring system that combines hardware sensors, a microcontroller, a backend server, and a web-based application to help students monitor their parked bicycles. 

The system aims to detect potentially suspicious movement, notify bicycle owners of possible tampering, and maintain a history of security events. It will also maintain local motion detection and alarm functionality when network connection is unavailable.

### System Components

The system consists of four main components:

#### 1. Microcontroller

- An ESP32 microcontroller processes sensor readings to detect potentially suspicious movement.
- Controls a local buzzer to provide an audible alarm when suspicious activity is detected. 
- Communicates security events to the backend server over Wi-Fi.
- Continues monitoring locally when the network connection is unavailable.

#### 2. Sensors

- An accelerometer and gyroscope monitor bicycle movement, vibrations, and changes in orientation.
- Provide motion data to the microcontroller for detecting potential tampering.

#### 3. Backend Server

- Receives data transmitted from the microcontroller.
- Maintains security event history, timestamps, and monitoring information.
- Communicates with the web dashboard to provide updates, process user commands, and potentially support additional notification functionality.

#### 4. Web Dashboard

- Displays alerts when potentially suspicious movement is detected.
- Displays the bike's monitoring and connection status.
- Allows users to remotely arm or disarm the monitoring system
- Allows users to view historical security events and their timestamps.
- Indicates when the monitoring device is disconnected or unavailable.
- May support additional notification options, potentially through a Progressive Web App (PWA), allowing users to receive alerts even when the dashboard is closed, subject to feasibility and device compatibility.

### Alert Flow

When suspicious movement is detected, the system:

1. Activates a buzzer to provide an immediate audible alarm.
2. Sends an alert to the backend server through a REST API over Wi-Fi when connected.
3. Records the incident for future reference so that the user can view it in the security history.
4. Updates the web dashboard so the bicycle owner can view the alert.

### Offline Monitoring

If Wi-Fi connectivity is unavailable, the microcontroller continues monitoring bicycle movement, activating the local buzzer when suspicious activity is detected, and temporarily storing security events.

Once connectivity is restored, pending events are transmitted to the backend server and recorded in the security history, allowing users to review activity detected while the device was offline.

While the device is disconnected, the web dashboard indicates that remote monitoring information and commands are unavailable. Real-time notifications cannot be delivered during the interruption.

## UI Mockups

![BikeGuard Pro UI mockups](public/mockup.png)

### Main Dashboard

The main dashboard allows users to monitor their bicycle's security status, arm and disarm the system, and view recent security alerts.

### Security Alert Screen

This screen informs users when suspicious movement is detected, displays the time of the incident, and provides an option to disarm the alarm and monitoring system.

### Event History Screen

The event history screen displays previously recorded security alerts and their timestamps, allowing users to review past bicycle activity.
