---
layout: page
title: About me
permalink: /about/
---

## Harim Seong
<p>halim9512@gmail.com</p><p style="text-align: left"><a href="https://github.com/harimseong">https://github.com/harimseong</a></p>

### Summary
<hr style="border: none; border-bottom: 1px solid white;">
I am software engineer with a strong interest in low-level areas such as embedded softwares and operating systems. Developing and debugging such things is challenging but gives rewarding experience.

### Skills
<hr style="border: none; border-bottom: 1px solid white;">
C/C++, shell script, Makefile, git, Docker, x86 


### Projects
<hr style="border: none; border-bottom: 1px solid white;">

##### [Unix Shell](https://github.com/harimseong/shell_project)
Project Detail
- Implemented a subset of the POSIX shell according to the POSIX documents.
- Handwrote a recursive descent parser for better readability and flexibility compared to other parsing methods.
- Used `fork`, `execve` and `pipe` system calls to create processes and manage IPC. 
- Debugged syntax by printing out the syntax structure.

Experience
- Conducted integration test using shell script that compares the shell with bash to see if it conforms to the standard.
- Improved Makefile for portability across macOS and Linux. This project was done using a few C standard functions, UNIX system call and libreadline. I had to handle only libreadline for portable compile.
- In macOS environment, I used docker to use tools available in Linux such as valgrind, gcc sanitizer.

##### [HTTP Webserver](https://github.com/harimseong/HTTP_server)
Project Detail
- Implemented a web server supporting HTTP/1.1 and a subset of the nginx configuration.

Experience
- Used Xcode Instruments tools to increase the software quality, Leaks for memory usage monitoring and fixing memory leaks, and Profiler to make sure every parts are consuming CPU as expected and find bad logics such as unnecessary copy and infinite loop.

- Optimized the HTTP message processing pipeline to minimize memory footprint. Upon receiving an incomplete HTTP message, partial body is sent to the destination(e.g. CGI process) immediately. It led to significant performance gain, especially when the message body is large, because it didn't wait until the entire message is fully received.


### Education
<hr style="border: none; border-bottom: 1px solid white;">

##### 42 Seoul, Cadet
2021\. 10 - 2023\. 10
- Peer evaluation system
- Project based learning
- Autonomous learning and problem solving


##### Seongkyunkwan University (SKKU), Bachelor's in Physics
2025\. 2

### Experience
<hr style="border: none; border-bottom: 1px solid white;">

##### SKKU High Energy Nuclear Physics Lab, Intern
2024\. 2 - 2025. 1

- Automated EIC ePIC simulation configuration, job batching and data processing using [shell script](https://github.com/harimseong/henpl/tree/main/eic) and writing [C++](https://github.com/harimseong/henpl/tree/main/eic/fsam).
- Participated Geant4 project for BIC simulation. Changed detector geometry according to requirements
- Provided debugging support for C++, ROOT, and research library build errors for researchers in the lab.


### Achievements
<hr style="border: none; border-bottom: 1px solid white;">
##### SKKU Next-generation Automotive Network SW Team Competition, 3rd place
2025\. 2

Project Detail
- Assembled hardware for zonal architecture using a HPC, 3 ZCUs, 3 Arduinos and 12 ultrasonic sensors.
- Gained experience to network layer. Ethernet for HPC and ZCU communication, and CAN for ZCU and Arduino communication.
- Developed a FreeRTOS task for parking logic based on state machine running on HPC (RA6M3 ECU).

Experience
- There was severe fluctuations of sensor value. To mitigate this, reduced the time interval of the task to receive 20 sensor response in the same time frame and derived an average of 20 consecutive values from an ultrasonic sensor.
- Had to move the car by hand to starting point whenever a test is done. To minimize labor, added new functionalities to buttons in HPC. Motor stop and reverse, state initialization to skip unnecessary states that succeeded before.
