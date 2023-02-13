# Smart-anomaly-detection-device
A deep autoencoder is trained on the STM32 microcontroller to automatically detect the rotary machine's fault. 

In this repository, the code and summary of smart anomaly detection device developed in this paper (https://ieeexplore.ieee.org/document/9663495) is provided.

## Abstract
Nowadays, manufacturing companies are faced with many issues due to the growing demand for high-quality and reasonable price products. As maintenance expenses of industrial machines are around 60% to 70% of the production costs [1], an efficient and real-time method of fault detection is essential for reducing the cost of machine maintenance and prolonging the equipment's life, thereby decreasing the production expenses. In this article, a novel high-performance and precise anomaly detection framework based on edge computing technology is developed to enable real-time health monitoring of industrial assets. As such, hardware and firmware design is pursued to enable execution of all critical tasks such as data acquisition and preprocessing, feature extraction, and training the algorithm on the edge node, i-e. the microcontroller. This is a big challenge given the processing power and memory limitation of the microcontroller. The sensor used here is a 3-axis accelerometer for acquiring vibration signals. After storing enough training data in Flash memory of the MCU, an autoencoder with three hidden layers is trained on the edge to model the machine's healthy state. Finally, the reconstruction error of unseen data is used to detect anomalies. As far as we know, this is the first article that trains an artificial neural network (ANN) on an MCU and does the whole process of condition monitoring on edge. The design is validated by testing the framework on a centrifugal pump. The test result shows that the system can detect various pump faults with over 99.9% precision, recall, accuracy, and F1 Score. 


## Project summary 
![image](https://user-images.githubusercontent.com/57262710/218365481-d11538e4-2dc7-49c5-90b7-9ec46cbc63e7.png)
![image](https://user-images.githubusercontent.com/57262710/218365542-c35d99a9-71ce-4a11-adc5-3d63b2287077.png)


