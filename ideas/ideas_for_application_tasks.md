# Ideas for application tasks

## Background

It is well known that applications and problem-solving task are very engaging and have motivational benefits. They help to demonstrate the importance of the theory at hand.

In mathematics, especially for engineers, applications are a crucial step in the process of formal education. They help broadening the picture but can also supply important insights into modelling, problem-solving, etc. that cannot be reached in purely mathematical tasks. Among others, mathematics is applied in

+ Physics
+ Economy
+ Biology
+ Chemistry
+ Optimization
+ Modelling complex systems like societies, illnesses, climate, etc. 

Based on the available tasks, some of these application areas seem to be within reach. In the following, a set of ideas will be embedded in the context of the respective field. This involves presentation of the problem, ideas what to test with it and ideas for implementation within the framework of STACK.

## Physics

### Electrodynamics: Lorentz-force

A well-known phenomenon in electrodynamics is the Lorentz-force. Typically, students are presented a 2D image of vectors and vector fields and are asked to make predictions about the temporal evolution of the system. We think that 3D visualization may help to graps the concept better and expand the horizon of such tasks.

#### <b>Brief introduction to the Lorentz-force</b>

The Lorentz-force $\vec{F}_L$ acts on moving charges in a magnetic field. The force is maximal, when the particle moves in a plane perpendicular to the magnetic field. It can be expressed as a vector product:
```math
\vec{F}_L = q\vec{v} \times \vec{B} 
```
In a homogeneous magnetic field, the force acts as a centripetal force, since it is always directed perpendicular to the component of $\vec{v}$ in the plane normal to $\vec{B}$. Hence the charge carrier with a charge $q$ is accelerated perpendicular to this velocity component. The result is a circular motion in the special case or a spiraling motion in the more general case.

#### <b>Applications of the Lorentz-force</b>

The Lorentz force is a very fundamental concept. Hence, it is used in a variety of fields:

+ Electro motors are driven by the Lorentz-force
+ Magnetic railways/rail guns are using it
+ Synchrotron particle accelerators bring particles in circular motion and accelerate them
+ Analog oscillators and vintage TV-systems deflect electron beams using Lorentz-force for image generation
+ In bubble chambers, radioactive particles are visible as circular paths due to their charge and earth's magnetic field

#### <b> Requirements for a task related to the Lorentz force</b>

It is not necessarily required to have a deep understanding of the vector product. Usually, in high school physics students are taught a rule to make out the direction of the Lorentz force with their hands. However, it is necessary to know what vectors are and, from a technical side, vectors need to be displayed.
Secondly, curves are needed to visualize the motion of the particle or it's $\textit{trajectory}$.

This means the software has to handle the following for visualization of Lorentz force:

+ display vector fields in 3D
+ display single vectors in 3D
+ calculate the vector product of two vectors
+ adjust a parametric curve based on the values of the vector product

#### <b> Interactive tasks using the Lorentz force </b>

The interactive component in the tasks is twofold: Firstly, the traditional multiple-choice and numerical tasks can be reproduced using an interactive display of the fields in 3D. This results in tasks like the following

+ Predicting the direction of the force based on the charge, velocity and magnetic field
+ Reconstructing the direction of the magnetic field from the trajectory and charge
+ Reconstructing the charge of the particle from the trajectory and magnetic field
+ Qualitative statements about the nature of the trajectory (such as helical, circular, straight,...)

Secondly, the traditional tasks can be expanded by interactively changing the properties of the particle, field, etc. This results in tasks such as the following

+ Making quantitative statements about the charge by varying it in order to match a curve displayed
+ Making changes to the magnetic field to obtain a given trajectory (such as rotating the direction or varying the strength)
+ Investigating inhomogeneous fields by input of functions
+ Simulating experiments

#### <b> What is currently available? </b>

As of now, there is no tasks addressing the problem. However most of the requirements are met by other tasks. You can find building bricks in the other tasks

+ Vector field visualisation in <b> Curl of a Vector Field </b>
+ Parametric curves in the task family <b> Parametric Curve Matchin </b>, especially the helix task

From that you can already create a few tasks by calculating the trajectory by hand and hard-coding it into the task. This will get you a long way.

#### <b>How can this be improved? </b>

You might want to increase the potential by adding a way to have arbitrary functions as an input to the magnetic field. Another way to make the task more interesting it so allow for dragging of the points constructing the velocity vector and have the trajectory changing accordingly.



## Engineering / Physics
### Fluid dynamics in 2D

Fluid dynamics is a very broad field. It is used in weather forecasts, motor racing, design of vacuums, clean rooms, oceanography and many more. At the core, fluid dynamics is the science of moving fluids, such as gases and liquids. The circulations can be expressed with the help of vector fields.

#### <b> Brief introduction to fluid dynamics </b>

There can be two types of flow distinguished from a temporal standpoint. A flow is called stationary, when the velocities at each point in space does not change with time. This is usually the case for systems that have had some time to reach a form of equilibrium. The contrary is instationary flow, where at each point the flow might vary over time. This can be e.g. be the case, when valves or windows are opened and the flow picks up.

Another way to distinguish flows is by its quality of predictability. Put simply, a flow is called laminar, when the evolution can be analytically obtained and turbulent, when the system is very chaotic predictions can be made only based on statistical probabilities. Of course the discrimination is much more nuanced, but a general understanding might be obtained already in this black-and-white picture.

Generally the flow is very dependend on the velocity field that can be influenced by the geometry of the system and other parameters. It might be of interest to see temporal changes when the geometry is altered.

#### <b> Requirements for fluid dynamics tasks</b>
It is necessary to display vector fields in at least 2D. Since they can become very complex, 2D will be a good start. It might be helpful to make them time-dependent for instationary flow. Additionally, curves such as the trajectories of floating particles need to be displayed. It is helpful to be able to calculate the divergence and curl of the field in order to make predictions about vortices and sources. This can of course be extended to allow for trajectories of extended objects. The software will need to handle:

+ (interactive) 2D vector fields
+ parametric curves in 2D
+ vector calculus such as curl and divergence
+ line integrals for work in an inconservatory force field


#### <b> Interactive tasks using fluid dynamics </b>



## Economy / Biology / Physics / Engineering
### Optimization problems

## General problemsolving using Mathematics
### Parametrization of curves, surfaces and volumes
