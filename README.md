# Estimator-for-quad-flight
Quad flying estimator with custom controller


Scenario 1: Sensor Noise

GPS and IMU measurements, with standard deviation(sigma) for those sensors.

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/scenario1.png?raw=true)

Scenario 2: Attitude Estimation

Errors of Linear approximation

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image2.png?raw=true)

Errors after non-linear implementation

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image3.png?raw=true)

Passing scenario 

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image4.png?raw=true)

PASS: ABS(Quad.Est.E.MaxEuler) was less than 0.100000 for at least 3.000000 seconds

- Implemantation: line 99 to line 121 (Implement a better rate gyro attitude integration)


Scenario 3: Prediction Step

Prediction of the state based on the acceleration measurement

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image5.png?raw=true)

First part implementation

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image6.png?raw=true)

Prediction implementation

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image7.png?raw=true)

- Implementation:  

PredictState method: line 180 to line 192.
GetRbgPrime method: line 216 to line 234.
Predict method: line 277 to line 288.

Scenario 4: Magnetometer Update

Update implementation with equation usage ( Estimation for Quadrotors paper)

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image8.png?raw=true)

Passing scenario

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image9.png?raw=true)


PASS: ABS(Quad.Est.E.Yaw) was less than 0.120000 for at least 10.000000 seconds
PASS: ABS(Quad.Est.E.Yaw-0.000000) was less than Quad.Est.S.Yaw for 67% of the time

- Implementation:  line 341 to line 353 (magnetometer update)


Scenario 5: Closed Loop + GPS Update

Update the GPS by eliminating the ideal estimator and equations from Estimation for Quadrotors paper

Gps Update

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image10.png?raw=true)


Passing scenario

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image11.png?raw=true)

PASS: ABS(Quad.Est.E.Pos) was less than 1.000000 for at least 20.000000 seconds


- Implementation: line 310 to line 322 (GPS update)

Scenario 6: Custom controller 

Adding the custom controller created in the previous project 

Parameters with custom controller 

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image12.png?raw=true)


Passing scenario

![alt text](https://github.com/pavlossk/Estimator-for-quad-flight/blob/master/image%2013.png?raw=true)

PASS: ABS(Quad.Est.E.Pos) was less than 1.000000 for at least 20.000000 seconds



Implementation Explanation:

- QuadEstimatorEKF.cpp: This is the EKF implementation
- QuadEstimatorEKF.txt: This file contains the parameters for tuning the EKF
- QuadControl.cpp: Cascade PID control implemented on the previous project
- QuadControlParams.txt: This file contains the parameters for the control code
