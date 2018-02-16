# CarND-Controls-PID
## Self-Driving Car Engineer Nanodegree Program

---
### Objective: Develop a PID controller that adjusts steering angle to drive a simulated vehicle around a track. The input driven into the controller is the cross track error (CTE) and the velocity (mph).  


### Effect of PID
---
The PID controller is a functionally simple controller that has very useful and practical applications. It functions by adjusting the control input of a dynamic system in order to converge its future states to a nominal one. The way this is performed is that the control input is dependent on some error between the present state and the nominal state. The control input is then adjusted by the sum of three variables of which each involves the error value. In the case of the driving simulation the error value is the cross track error which is the lateral distance between the current position and the centre line of the road. The three terms that affect the control input are what make up the PID controller and they are as follows:

P - Proportional - -tau_p * cte - This term is the product between a constant and the cross track error which allows the car to direct itself towards the centre. The larger the error, the larger the control input. The constant tau_p determines the magnitude or influence of this term on the control input.

I - Integration - -tau_i * integral or summation of cte - This term is the product between a constant and the integral of the cross track error which directs the car towards the centre if it has behaved in some assymetrical fashion due to either misalignment or process noise. The constant tau_i determines the magnitude of this term on the control input. 

D - Derivative - -tau_d * derivate of cte - This term is the product between a constant and the derivative of the cross track error which directs the car towards the nominal by calculating differences between the rates of change in the cross track error. This is effectively the term that provides damping towards the cyclic nature of the system. When the error is large the difference between the change in error rates will be larger than when it is close which allows the system to converge towards the nominal state.

There are videos uploaded in the videos folder that show the effect of each term added towards the control input.

### Hyperparameters
The hyperparameters were chosen by fine-tuning as it was found to be the most efficient process if the program received the coefficients as arguments in program start up. The first value that was determined was the proportinal gain - tau_p - where the value was determined based on reasonable steering motion during the initial straight path. However the proportional gain was simply not enough as the vehicle sped up during the initial straight path and hence the system quickly becomes unstable and falls off the track. The integration value appeared to be negligible as it was found that no biases or noise was inherent in the simulation yet a small coefficient was added in the case that it may have an effect. Finally the derivative value was the parameter that was tuned the most in order to find the coefficient that provided the necessary damping to stay on the road and clear turns effectively. The final derivative parameter was identified by increasing the value until an acceptable run was achieved.


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

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

