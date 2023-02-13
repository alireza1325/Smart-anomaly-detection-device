# Smart-anomaly-detection-device
A deep autoencoder is trained on the STM32 microcontroller to automatically detect the rotary machine's fault. 

In this repository, the code and summary of smart anomaly detection device developed in this paper (https://ieeexplore.ieee.org/document/9663495) is provided.

## Abstract
Nowadays, manufacturing companies are faced with many issues due to the growing demand for high-quality and reasonable price products. As maintenance expenses of industrial machines are around 60% to 70% of the production costs [1], an efficient and real-time method of fault detection is essential for reducing the cost of machine maintenance and prolonging the equipment's life, thereby decreasing the production expenses. In this article, a novel high-performance and precise anomaly detection framework based on edge computing technology is developed to enable real-time health monitoring of industrial assets. As such, hardware and firmware design is pursued to enable execution of all critical tasks such as data acquisition and preprocessing, feature extraction, and training the algorithm on the edge node, i-e. the microcontroller. This is a big challenge given the processing power and memory limitation of the microcontroller. The sensor used here is a 3-axis accelerometer for acquiring vibration signals. After storing enough training data in Flash memory of the MCU, an autoencoder with three hidden layers is trained on the edge to model the machine's healthy state. Finally, the reconstruction error of unseen data is used to detect anomalies. As far as we know, this is the first article that trains an artificial neural network (ANN) on an MCU and does the whole process of condition monitoring on edge. The design is validated by testing the framework on a centrifugal pump. The test result shows that the system can detect various pump faults with over 99.9% precision, recall, accuracy, and F1 Score. 


## Project summary 
Figure below shows the various components and the photo of the device. It consists of a microcontroller board (STM32H743ZI2) with ARM Cortex-M7 core, a digital 3-axis accelerometer (LIS3DSH), two lithium-ion batteries, Zigbee wireless module, Zigbee module antenna, and an enclosure. The MCU runs at 480 MHz and has 1 MB RAM
and 2 MB Flash memory used to store the code. Furthermore, the digital accelerometer acquires vibration signals along three axes with 1600-Hz sampling frequency and 16-bit resolution, and it has an onboard anti-aliasing filter with 800 Hz cut-off frequency. The Xbee module can send and receive data at 250,000 bps rate in a circle with a radius of around 90 meters. Owing to the low power consumption of the MCU in running and sleep mode and modules, the system can run approximately for two years with two lithium-ion batteries, each 4000 mAh capacity.
![image](https://user-images.githubusercontent.com/57262710/218365481-d11538e4-2dc7-49c5-90b7-9ec46cbc63e7.png)


Each vibration sample acquired via the accelerometer from each axis has 2048 sample points. After storing three axes raw vibration data into three different arrays, the DC gain of each axes has removed by subtracting the mean of the array from each sample point. Subsequently, the total 29 features are extracted from each axis and stored in an array with a length of 87. 

![image](https://user-images.githubusercontent.com/57262710/218366052-a137b7ba-5cc5-4c28-af8c-2520781d77b1.png)


