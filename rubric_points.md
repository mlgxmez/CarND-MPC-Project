## Implementation of model predictive control

In this project, a controller has been designed by modelling the vehicle dynamics of a car. The controller must be able to control the **sterring wheel** and the **throttle** of the car in order to complete a lap on the track without crossing the road boundaries.

### The model
As from previous lessons, the dynamics of the car are based on the kinematic model. The state vector contains:

* the *X* and *Y* position of the car
* the orientation of the car
* its velocity
* the cross-track error, which is the distance between the current position of the car and the reference trajectory
* the error of the oriention of the car with respect to the orientation of the trajectory (a value that can be obtained from the derivative of any point of the trajectory)

The actuators are:

* Steering angle
* Throttle

And the model is defined with the following equations:

Since we know the behavior of the car depending on the input values of the actuators fed into the model. We can estimate those subject to minimizing a cost function. Multiplying each cost by a factor we can achieve that the steering wheel turns smoothly.

### Time elapsed and length duration

There are some guidelines to choose the proper values. The most straightforward choice would be the time step (dt) between states as short as possible and the number of steps (N) as large as to sum up a couple of seconds. Having a huge number of steps is a waste of resources because the car moves in an evolving environment. Having said that, the choice in this particular case has been dt = 0.05 seconds and N = 10 steps. 

It is possible to take also into account the speed of the car. If the car decreases slows down you could rise dt and reduce N so that the product of the time step and the number of steps remains constant.

### Polynomial fitting and MPC processing

Waypoints are fitted into third degree polynomial. Although, it is required to transform firstly the waypoints from global coordinates to car coordinates with an homogeneous transformation (which includes a translation and rotation. Take into account that the orientation for this project has the positive values when rotating clockwise.

### Model Predictive Control with Latency

Due to the latency generated between sending the inputs to the simulator and the moment the actuators are applied to the car this factor has to be taken into account. The latency is 100ms which is translated to 2*dt. Since we know the car's state at that moment (becuase we have the model) we assume that the current state of the car will be the one that happens 0.1s into the future.

So in the equations we change dt by the latency parameters. The equations are expressed in car coordinates.

## Results

By runnning the simulator, the model predictive controller is able to control the car despite the abrupt turns of the track after crossing the bridge.
