# CarND-PIDControl-P9
PID Control project  
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Rubrics

**1. Compilation**   

The code compiles without errors

**2. Implementation**   
 
 The PID procedure follows what was taught in the lessons. I calculated a like we did at the lectures ( a = - Tp * CTE - Td * diff_CTE - Ti * Sum_CTE )
 
 **3. Reflection**  
 As a first step I initialized [Kp, Kd, Ki] to [0, 0, 0], to make sure the vehicle goes straight. Then, I started using each parameter separately to get a more visual idea of the affect of each on the final trajectory of the vehicle.  
 
* Proportional, P: After initializing to [1, 0, 0] and trying reducing and increasing the P value, I reached the conclusion that P is responsible for steering the vehicle towards the middle line. As also taught in the lectures, P is steering the vehicle against the cross-track error. This causes an overcorrection on the steering (overshooting)  

* Integral, I: After initializing to [0, 1, 0], the vehicle went immediately off road. This value is responsible for correcting any bias on the model that might affect the reduction of the error and the correction of the trajectory. In our case, I assumed that on the simulator there is no bias present, thus decided to keep Ki = 0  

* Differential, D: After initializing to [0, 0, 1], the vehicle went straight. Consequently, I reached the conclusion that D is the value responsible for "correcting" the overshooting caused by the proportional. This was off course taught in the lectures, but this exercise allowed me to get a more visual idea of the actual effect of these values.  


After those tries, I started changing the parameters' values until I find the best combination. The method I used was manual tuning - trial and error. My comments from the trials were:   
- [0.5, 0, 1]: Stays in the middle but overcorrects a lot - needs more D  
- [0.5, 0, 1.5]: Very sudden steering movements but less overcorrection - needs more D  
- [0.5, 0, 2.5]: Not smooth at all. Changed approach and started changing P  
- [0.25, 0, 2.5]: Smoother but the steering is very sharp on the corners  
- [0.1, 0, 2.5]: Smoother but still needs additional tuning  
- [0.1, 0, 3.5]: Very smooth but on the corners it tends to touch the apex  
- [0.15, 0, 3.5]: Still the same behaviour. Increase P, reduce D  
- [0.2, 0, 3]: Better but overcorrects. Reduce P  
- [0.15, 0, 3]: Very smooth  

Conclusion: [0.15, 0, 3]  

**Simulation:**  
The vehicle successfully drives a lap around the track

 
