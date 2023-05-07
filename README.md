Download Link: https://assignmentchef.com/product/solved-me227-assignment-1-the-kinematic-model
<br>
There is a lot we can learn about the design and control of vehicles using simple models. To start off, we have a few exercises to familiarize yourself with the notation of coordinate transformations and rotation matrices introduced on the first day of class and to gain some more insight into the kinematic model. You will also build a simple simulation and test controllers capable of tracking a path with the kinematic model.

<h1>Instructions</h1>

This and following homework assignments will be submitted using two different tools, Gradescope and MATLAB Grader. Throughout the assignment, each prompt will be marked with either <strong>Gradescope </strong>or <strong>MATLAB Grader </strong>to make it clear where you should be submitting the answer to that problem. MATLAB Grader questions will also be shown in <strong>Blue </strong>to make them easy to see.

All written portions must be turned in through Gradescope. We will provide three different homework formats on Canvas (a latex template, a pdf template, and a condensed pdf template). Whatever format you decide to use, please <strong>BOX </strong>all of your final answers.

Some problems will make use of the MATLAB Grader suite discussed in class. These problems are available directly from Canvas by clicking on each individual question. You are allowed to submit code to MATLAB Grader as many times as you want before the due date without penalty. In this way you can be sure each function or script passes all of the assessments that go along with it before moving on to the next problem. We encourage you to write your own test cases as well to ensure your code is working as expected.

1

<h1>Problem 1 – Rotation Matrices</h1>

Rotation matrices are an important component of any control of dynamical systems. They provide easy transformations of locations, velocities, and commands that occur in different frames. This problem will help you gain some intuition into rotation matrices as you practice creating them.

<h2>Question 1.A – Combining Rotation Matrices (Gradescope)</h2>

Show that rotating from the vehicle frame to the inertial frame and then into the path frame is equivalent to rotating directly from the vehicle frame to the path frame. In other words, demonstrate the result we used in class that

<em>A</em><em>POA</em><em>OV </em>= <em>A</em><em>PV</em>

<em>Write the expression showing A<sub>PO</sub>A<sub>OV </sub></em>= <em>A<sub>PV </sub></em><em>. Please include your work.</em>

<h2>Question 1.B – Creating Rotation Matrices (MATLAB Grader)</h2>

Implement a function that returns the rotation matrix <em>A<sub>vo </sub></em>for some heading angle Ψ<em><sub>V E</sub></em>. You can use this function to translate a point from the inertial frame, <em>O</em>, to the vehicle frame, <em>V </em>.

<h1>Problem 2 – Lateral Velocity and Sideslip Angle</h1>

In the kinematic bicycle model, the lateral velocity at the rear axle is zero under the assumption that the tire velocity is aligned with the tire’s longitudinal axis. The lateral velocity is nonzero at other points along the centerline of the kinematic vehicle, however.

<h2>Question 2.A – Velocity (Gradescope)</h2>

Derive an expression for the velocity at any point along the centerline of the kinematic model starting at the rear axle (<em>x </em>= 0) and ending at the front axle (<em>x </em>= <em>L</em>). You should express this only in terms related to the vehicle (the steer angle, the velocity and the wheelbase) and not the radius of the path. In our notation, we want an expression for the vector

at any point from 0 to <em>L </em>along the centerline.

<em>Write the expression for v<sub>ox,V </sub></em><em>. Please include your work.</em>

e

<h2>Question 2.B – Sideslip Angle (Gradescope)</h2>

Another way to think about the lateral velocity is in terms of the sideslip angle, <em>β</em>, of the vehicle which is the angle between the velocity vector and the vehicle’s centerline:

Using the kinematic bicycle model and assuming small angles, calculate an expression for the sideslip angle at any point on the vehicle centerline from <em>x </em>= 0 to <em>x </em>= <em>L</em>.

<em>Write the expression for β</em><em>. Please include your work.</em>

<h2>Question 2.C – Model Intuition (Gradescope)</h2>

Based on this velocity scenario and the geometry of the model, if the vehicle is tracing out a constant radius with point <em>v </em>on the centerline of the rear axle, is the front axle tracing the same path? If not, what is the shape of the path traced by the front axle and does it lie inside or outside the path traced by the rear axle?

<em>Select the correct answers below and give your explanation for these answers.</em>

The front axle will track a path which is                                      .

( Circular / Ellipsoidal / Same As The Rear Axle / Other)

The front axle will trace a path which is                                       the path traced by the rear axle.

( Inside / The Same As / Outside )

<h1>Problem 3 – Tracking a Path</h1>

Let’s start off on a straight road and assume that the vehicle will be close enough to the desired path that small angle assumptions are valid. Assume that we begin pointing along the centerline of the road (∆Ψ(0) = 0) but with an offset from our desired lateral position, (<em>e</em>(0) 6= 0).

<h2>Question 3.A – Lookahead Controller (Gradescope)</h2>

A common method for path tracking with vehicles is to use a lookahead controller. This can either look at the projected error some distance ahead on the path or, more commonly, approximate this error as a linear combination of the lateral error and heading error:

<em>δ </em>= <em>K</em><em>lae</em><em>la e</em><em>la </em>= <em>e </em>+ <em>d</em><em>la</em>∆<em>ψ</em>

Here <em>d<sub>la </sub></em>functions as the “lookahead distance” ahead of the reference point at which the error is calculated. This is exactly the projected error on a straight road and approximately the projected error on a curved road if the curvature is not too large relative to the lookahead distance.

During lecture, we also derived these equations assuming a small heading error and a small curvature:

Perform several Laplace transforms assuming small angles, a straight road, and <strong>constant velocity</strong>. Arrange this into a form where we can look at the response to the lateral error from the initial condition. In other words, calculate the relationship:

The denominator of this relationship is the characteristic equation of the system that we can use to design the performance of our tracking controller.

Note: <em>Where does the initial condition e</em>(0) <em>come from? Remember that initial conditions are a part of the Laplace transformation, we just often set them to zero when forming a transfer function. Leave them in your expression here.</em>

<em>Write the resulting relationship </em><em>. Please include your work.</em>

<h2>Question 3.B – Controller Stability (Gradescope)</h2>

If the lookahead distance (<em>d<sub>la</sub></em>) is a positive number, what can you immediately say about the sign of the lookahead gain (<em>K<sub>la</sub></em>) in order for the tracking system to be stable?

<em>Select the correct answer below.</em>

<strong>Solution:</strong>

The lookahead gain (<em>K<sub>la</sub></em>) must be                                       .

(Positive / Negative)

<h2>Question 3.C – Lookahead vs PD Control (Gradescope)</h2>

Show that for a constant vehicle speed, the lookahead controller is equivalent to a PD controller of the form:

Calculate the parameters <em>K<sub>p </sub></em>and <em>K<sub>d </sub></em>in terms of <em>K<sub>la </sub></em>and <em>d<sub>la</sub></em>. You should see that the lookahead control law provides a simple way of scaling, or gain scheduling, proportional and derivative gains as the vehicle speed changes.

<em>Write the parameters K<sub>p </sub></em><em>and K<sub>d </sub></em><em>in terms of K<sub>la </sub></em><em>and d<sub>la</sub></em><em>.</em>

<h2>Question 3.D – Controller Design (Gradescope)</h2>

Calculate values of <em>K<sub>la </sub></em>and <em>d<sub>la </sub></em>that will give the system a rise time of 2 seconds and a peak overshoot of 10% if the vehicle has a wheelbase, <em>L</em>, of 2<em>.</em>5<em>m </em>and travels at a speed, <em>V </em>, of 10<em>m/s</em>.

<em>Write the calculated values of K<sub>la </sub></em><em>and d<sub>la</sub></em><em>. Please include your work.</em>

<h1>Problem 4 – Building a Simulator</h1>

Now we want to see how well this controller developed using simple analysis works in simulation. You will build up a simulation environment in MATLAB by following the MATLAB Grader prompts available in Canvas. The prompts are also shown for reference in the questions below.

<h2>Question 4.A – Equations of motion (MATLAB Grader)</h2>

Follow the prompts in MATLAB Grader to create a function which calculates expressions for the vehicle state derivatives ˙<em>s</em>, ˙<em>e</em>, and ∆Ψ. Do˙ <strong><u>not </u></strong>assume small angles when writing expressions for the state derivative. You are to modify the state derivatives s_dot, e_dot, and dpsi_dot in the function template on MATLAB Grader.

<h2>Question 4.B – Euler Integration (MATLAB Grader)</h2>

Follow the prompts in MATLAB Grader to create a function which implements a simple Euler integration scheme with a given time step. For this function, don’t use built in MATLAB functions such as trapz. You are to modify the expression for the state at the next time step x1.

<h2>Question 4.C – Lookahead Controller (MATLAB Grader)</h2>

Follow the prompts in MATLAB Grader to create a function which implements the lookahead controller you designed in <strong>Problem 3</strong>. Use the lookahead gain and distance calculated in <strong>Question 3.D</strong>. You are to modify the lookahead controller parameters K_la and d_la, the lookahead error e_la, and the steering angle command delta.

In this function you should assume small angles, and that the road is straight.

<h1>Problem 5 – Simulate Various Road Geometries</h1>

Now we’ll use the simulator built in <strong>Problem 4 </strong>to analyze the controller’s performance. Follow the MATLAB Grader prompts available in Canvas for each question below. The prompts are copied here for reference. Once the simulations are working, answer the qualitative questions about each simulation case.

<h2>Question 5.A – Simulation with a Straight Road (MATLAB Grader)</h2>

Now we’ll use the simulator built in <strong>Problem 4 </strong>to analyze the controller’s performance. We’ll begin on a straight road with no intial heading error (∆Ψ) and a small path-tracking error (<em>e</em>). The simulation will use parameters from our research vehicle <strong>Niki </strong>which is a Volkswagen GTI. The simulation is set to run for 10 seconds. After the simulation is complete, plot the lateral error (<em>e</em>), the heading error (∆Ψ), and lookahead error (<em>e<sub>la</sub></em>) as a function of time. Follow the prompts in MATLAB Grader to create and run this simulation.

<h3>Question 5.B – Simulation with a Straight Road (Gradescope)</h3>

Examine the plots you created in <strong>Question 5.A</strong>. Is the vehicle able to track the path with zero error?

<em>Describe the controller’s performance in terms of tracking error.</em>

<h2>Question 5.C – Simulation with a Curved Road (MATLAB Grader)</h2>

Now we are going to let the road curve. Simulate your controller here for the same gains and initial conditions as <strong>Question 5.A </strong>on a curved road with a constant radius of 20 meters. After the simulation is complete, plot the lateral error (<em>e</em>), the heading error (∆Ψ), and lookahead error (<em>e<sub>la</sub></em>) as a function of time. Follow the prompts in MATLAB Grader to create and run this simulation.

<h3>Question 5.D – Simulation with a Curved Road (Gradescope)</h3>

Examine the plots you created in <strong>Question 5.C</strong>. Is the vehicle able to track the path with zero error?

<em>Describe the controller’s performance in terms of tracking error compared to Question 5.A.</em>

<h2>Question 5.E – Simulation with an Undulating Road (MATLAB Grader)</h2>

Now we’ll run the simulation on an undulating road which curves left and right. Simulate your controller here for the same gains and initial conditions as <strong>Question 5.A</strong>. After the simulation is complete, plot the lateral error (<em>e</em>), the heading error (∆Ψ), and lookahead error (<em>e<sub>la</sub></em>) as a function of time. Follow the prompts in MATLAB Grader to create and run this simulation.

<h3>Question 5.F – Simulation with an Undulating Road (Gradescope)</h3>

Examine the plots you created <strong>Question 5.E</strong>. Is the vehicle able to track the path with zero error?

<em>Describe the controller’s performance in terms of tracking performance compared to Question</em>

<em>5.A and Question 5.C.</em>

<h2>Question 5.G – Compensating for Non-Zero Curvature (MATLAB Grader)</h2>

One way to handle tracking in the event of non-zero (and possibly changing) curvature is to use nonlinear feedback to compensate. The yaw dynamics take the form of:

Compensate for the curvature term in this equation by changing the commanded steer angle to:

<em>,</em>

Create a function called lookahead_lateral_control_curvature that implements this modified lookahead controller. Follow the MATLAB Grader prompts to create this function.

<h2>Question 5.H – Simulation with Curvature Compensation (MATLAB Grader)</h2>

Now use your updated version of the lookahead controller with curvature compensation to control the vehicle on the undulating road. Simulate your controller here for the same gains and initial conditions as <strong>Question 5.A</strong>. After the simulation is complete, plot the lateral error (<em>e</em>), the heading error (∆Ψ), and lookahead error (<em>e<sub>la</sub></em>) as a function of time. Follow the prompts in MATLAB Grader to create and run this simulation.

<h3>Question 5.I – Simulation with Curvature Compensation (Gradescope)</h3>

Examine the plots you created in <strong>Question 5.H</strong>. Is the vehicle able to track the path with zero error?

<em>Describe the controller’s performance in terms of tracking error compared to Question 5.E.</em>

<h3>Question 5.J – Understanding Curvature Compensation (Gradescope)</h3>

Explain how the additional term in our control law, from <strong>Question 5.G</strong>, is compensating for curvature.

<em>Please provide both a mathematical and qualitative explanation of our curvature compensation.</em>

<h1>Appendix A – Vehicle Parameters</h1>

<table width="502">

 <tbody>

  <tr>

   <td width="116"><strong>Variable Name</strong></td>

   <td width="60"><strong>Value</strong></td>

   <td width="53"><strong>Units</strong></td>

   <td width="273"><strong>Description</strong></td>

  </tr>

  <tr>

   <td width="116">veh.m</td>

   <td width="60">1926.2</td>

   <td width="53">kg</td>

   <td width="273">Mass (Includes 4 passengers)</td>

  </tr>

  <tr>

   <td width="116">veh.Iz</td>

   <td width="60">2763.49</td>

   <td width="53">kgm<sup>2</sup></td>

   <td width="273">Yaw Moment of Inertia</td>

  </tr>

  <tr>

   <td width="116">veh.a</td>

   <td width="60">1.264</td>

   <td width="53">m</td>

   <td width="273">Distance from Center of Mass to Front Axle</td>

  </tr>

  <tr>

   <td width="116">veh.b</td>

   <td width="60">1.367</td>

   <td width="53">m</td>

   <td width="273">Distance from Center of Mass to Rear Axle</td>

  </tr>

  <tr>

   <td width="116">veh.L</td>

   <td width="60">2.631</td>

   <td width="53">m</td>

   <td width="273">Wheelbase</td>

  </tr>

 </tbody>

</table>

Table 1.1: Vehicle Parameters and Values