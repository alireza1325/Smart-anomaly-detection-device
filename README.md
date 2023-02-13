# Smart-anomaly-detection-device
A deep autoencoder is trained on the STM32 microcontroller to automatically detect the rotary machine's fault. 

In this repository, the code and summary of the smart anomaly detection device developed in this paper (https://ieeexplore.ieee.org/document/9663495) are provided. The zip file contains the source code for training and testing the autoencoder on MCU with all required libraries. It should be noted that STM32CubeIDE and STM32CubeMX were utilized to program the microcontroller. 

## Abstract
Nowadays, manufacturing companies are faced with many issues due to the growing demand for high-quality and reasonable price products. As maintenance expenses of industrial machines are around 60% to 70% of the production costs [1], an efficient and real-time method of fault detection is essential for reducing the cost of machine maintenance and prolonging the equipment's life, thereby decreasing the production expenses. In this article, a novel high-performance and precise anomaly detection framework based on edge computing technology is developed to enable real-time health monitoring of industrial assets. As such, hardware and firmware design is pursued to enable execution of all critical tasks such as data acquisition and preprocessing, feature extraction, and training the algorithm on the edge node, i-e. the microcontroller. This is a big challenge given the processing power and memory limitation of the microcontroller. The sensor used here is a 3-axis accelerometer for acquiring vibration signals. After storing enough training data in Flash memory of the MCU, an autoencoder with three hidden layers is trained on the edge to model the machine's healthy state. Finally, the reconstruction error of unseen data is used to detect anomalies. As far as we know, this is the first article that trains an artificial neural network (ANN) on an MCU and does the whole process of condition monitoring on edge. The design is validated by testing the framework on a centrifugal pump. The test result shows that the system can detect various pump faults with over 99.9% precision, recall, accuracy, and F1 Score. 


## Project summary 
Figure below shows the various components and the photo of the device. It consists of a microcontroller board (STM32H743ZI2) with ARM Cortex-M7 core, a digital 3-axis accelerometer (LIS3DSH), two lithium-ion batteries, Zigbee wireless module, Zigbee module antenna, and an enclosure. The MCU runs at 480 MHz and has 1 MB RAM
and 2 MB Flash memory used to store the code. Furthermore, the digital accelerometer acquires vibration signals along three axes with 1600-Hz sampling frequency and 16-bit resolution, and it has an onboard anti-aliasing filter with 800 Hz cut-off frequency. The Xbee module can send and receive data at 250,000 bps rate in a circle with a radius of around 90 meters. Owing to the low power consumption of the MCU in running and sleep mode and modules, the system can run approximately for two years with two lithium-ion batteries, each 4000 mAh capacity.

![image](https://user-images.githubusercontent.com/57262710/218367282-8299a5da-f15d-458e-99e7-ac6846c26973.png)

Each vibration sample acquired via the accelerometer from each axis has 2048 sample points. After storing three axes raw vibration data into three different arrays, the DC gain of each axes has removed by subtracting the mean of the array from each sample point. Subsequently, the total 29 features are extracted from each axis and stored in an array with a length of 87. 

![image](https://user-images.githubusercontent.com/57262710/218367348-bfc3c47f-16f5-4d9b-94f0-c9750645d280.png)

As the goal of this research is to create a standalone device for real-time fault detection of rotating machines, the common classification methods can not be used because their training requires labeled data from both faulty and healthy states of the machine, which is not available in most cases. In this situation, novelty detection algorithms are the best choice. In this study, we utilized one of the most commonly used novelty detector algorithms, autoencoders. Autoencoders are feed forward fully connected artificial neural networks that can learn to reconstruct their unlabeled inputs. If an autoencoder is trained by healthy machine data, it can precisely reproduce every healthy data. However, when faulty data is fed to the autoencoder, it is not able to reconstruct it. So the mean squared error (MSE) between input and output of the autoencoder can be used as an indicator for discriminating the healthy and defective state of the machine. The algorithm flow chart can be seen in figure below.

![image](https://user-images.githubusercontent.com/57262710/218367410-004ddf2e-0b40-433a-9bfc-044ecd17fd44.png)

To prove the feasibility of this technology, another experiment was conducted on the setup, and the whole previously described process, including collecting the 
batches, teaching the network, and testing using unseen data, was done automatically by the MCU. After training the model by four batches of 100 sample healthy data in 10 distinguished pump operating points, 86 unseen healthy samples were fed to the network, and then the cavitation fault was introduced, and again 57 tests under healthy pump condition were conducted. The number of tests under cavitation conditions was 100. Figure below displays that the network has been successfully trained on the MCU and could differentiate the normal and abnormal machine conditions. 

![image](https://user-images.githubusercontent.com/57262710/218367091-35557f43-35df-44a2-a84c-8dd3fae06d4e.png)


