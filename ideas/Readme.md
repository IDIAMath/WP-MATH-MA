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

The first kind of interactive task might involve interactive treatment of the vector fields present in fluid dynamics and might include

+ reconstructing vector fields with specific properties
+ judging, whether vector fields have fulfil certain properties such as having no curl or no divergence

The second kind might involve treatment of objects under influence of the flow, such as

+ Prediciting the trajectory of a particle in the vector field and parametrizing it or drawing an estimation
+ Predicting the change of orientation of simple objects such as boxes


#### <b> What is currently available? </b>

Currently, the visualization of 2D vector fields is possible in JSXGraph.
Mathematical operations such as calculation of a curl or a divergence can be done with STACK, as demonstrated in the task <b> Curl of a vector field </b>.

Also, JSXGraph provides a method to draw in an applet by recognizing cursor movement and reconstructing lines from it.


#### <b>How can this be improved? </b>

As of now, we have not seen an implementation of any of the functions mentioned above into a 2D vector field task. However, the first kind of tasks mentioned should be possbile to implement with relative ease. Some of the problems have already been solved in the progress of creation of 3D tasks.

On the other side, we have no knowledge about the drawing being included into a vector field task. It might be necessary to implement a way to extract the drawn curve from the applet in order to compare it to a reference solution. A simple fix in formative assessment could be to have the student draw the line and consequently present a correct solution. Then the student could judge by himself, whether the task was solved correctly. In this case no implementation of the drawn curves into STACK would be necessary.

## Economy / Biology / Physics / Engineering
### Optimization problems
#### <b> Brief introduction to optimization </b>
Optimization is a mathematical discipline in applied mathematics. In essence an optimization problem consists of the following steps
+ formalizing the problem
+ finding a function within the formalism that describes the feature of interest
+ finding restrictions based on the formalization of the problem
+ minimizing the function in the set defined by the restrictions
+ translating the mathematical result into possible actions

As this is a very general procedure, it can be applied to many fields in life and science. This makes it a very potent tool and desirable for engineers to pick up and master. Some of the applications include

+ minimizing material in 3D printing
+ minimizing material loss in CNC routing or turning of parts
+ minimizing time of production in machines
+ minimizing distances travelled in logistics
+ cutting costs in productions by optimizing the processes in factories
+ finding physical results based on minimization priciples

#### <b> Requirements for optimization tasks</b>
Optimization tasks require a way of demonstrating the function. Consequently, maxima and minima need to be able to be determined or extremal points selected in a graphic. The processes of formalization of the problems should be guided step by step with examples. The determined restrictions should be visualized by constraining the function to the corresponding points. Lastly, mathematical operations leading to the solution of optimization tasks should be visualzied step by step in the graphics in order to facilitate generalization for the students.

#### <b> Interactive tasks using optimization </b>
Interactive tasks using optimization might be tackled from multiple perspectives. The general themes of the tasks could be
+ formulating a problem and formalizing the given informations into a mathematical model
+ working with a given model and finding optimal solutions
+ understanding processes of optimization algorithms graphically
+ making use of optimization results in applied contextes or giving advice based on the solutions

From these general topics, more specific tasks can be deduced. For example a task could be to formulate a linear optimization problem by giving the function and restrictions in an algebraic manner. If the answer is not correct the task becomes adaptive and a series of intermediate tasks is presented.

For a 2D optimization problem a task could be to drag planes on the graphic to fit the restrictions given in a text and visualizing the restriction of the functio.
Additionally, the concepts of stationary points, maxima and minima can be demonstrated in an interactive manner.

It could be helpful to have the students go step by step with an algorithm like the Simplex. They follow the calculations and experience how the points move on the functions until the optimal value is found.



#### <b> What is currently available and how could it be improved? </b>
Currently, the visualization of stationary points, maxima and minima using Taylor approximations to the functions in an environment of the selected points is available. It can be found in the tasks <b> Stationary point of a 2D function </b>, <b> Point of a 2D function with negative definite hessian </b> and  <b> Point of a 2D function with positive definite hessian </b>.

It will be relatively easy to include restrictions such as adjustable vertical planes into the graphics and create visualization tasks from it.

With respect to the formulation of problems, no tasks are currently available. However, the concept of adaptive tasks has already been demonstrated in tasks such as <b> Rotation of a curve about two axis adaptive </b> and <b> Curl of a vector field adaptive </b> as well as many more examples created at Ruhr Universität Bochum by Kallweit and colleagues.

Lastly, the demonstration of the Simplex has not been included in an interactive task so far. However points on a function can easily be displayed, dragged and read out into answers. It is therefore only a matter of including the correct algorithm into STACK and making the step-by-step process feasable. This could be done with methods similar to those used in the adaptive tasks.



## General problemsolving using Mathematics
### Parametrization of curves, surfaces and volumes

#### <b> Brief introduction to parametrization </b>
Paramtrization is the process of expressing geometrical objects such as curves, surfaces and volumes by mathematical expression that are dependent on a set of parameters. By varying the parameters, the geometrical shape can be generated from the image of a mathematical function. This is a step necessary in basically every modelling process in mathematics. Since mathematics is used to describe real-world problems, a translation between spatial properties and mathematical entities is necessary. This translation is provided by parametrizations of the objects in a chosen frame of reference.

#### <b> Requirements for parametrization tasks</b>
In order to visualize parametrizations, geometrical objects will need to be displayed in 2D and 3D. Additionally, changes may need to be made to geometrical objects interactively in order to get a better idea of how the individual parameter affects the object. Lastly, parametrization will be given algebraically, so the corresponding expressions need to be interpreted and compared to the reference solutions.

#### <b> Interactive tasks using parametrization </b>
Interactive tasks for the topic of parametrization can have many different facettes. A few of them include
+ matching exercises in order to obtain the value of parameters
+ exercises helping in the decision process of which functions describe the problem best
+ finding expressions to the set of points that implicitly define the object or reconstruct the object from the implicit representation
+ making predictions about the changes to an object for a given parameter change



#### <b> What is currently available? </b>
Especially the matching exercises have been extensively investigated. Examples range from curves to volumes and can be found in tasks such as <b> Parametric Curve Matching circular/elliptic/elliptic helix</b> and <b> Spherical Coordinate Matching</b> among others.

#### <b>How can this be improved? </b>
From the tasks mentioned before, tasks for making predicitons about the effect of parameter changes can easily be obtained. It is only a matter of getting rid of the sliders for the student to use and putting in the new values in the functions used in the STACK tasks.

The other kinds of tasks have not been investigated. It will be necessary to include some basic priciples of displaying the objects that have been used in the tasks mentioned before. However the didactical progress will have to be found from scratch. In the progress some concepts of the existing tasks such as adaptive tasks may be helpful.
