---
title: Spherical Coordinates Rotating
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows the transformation from cartesian to spherical coordinates  (Handling mathematical symbols and formalism)
+	Student can take a volume with spherical geometry and reconstruct the limits of its radius and angles (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://user-images.githubusercontent.com/120648145/210994640-325cf839-9f6e-4fbd-8428-bda50e42b8e2.PNG) |
|:--:|
| *First impression of the question* |

## Question description

A 3D volume is plotted. It is a randomly generated section of a ball in spherical coordinates.

The task is to find the correct intervalls for $r$, $\phi$ and $\psi$ in real numbers that construct the generated volume in sperical coordinates.


### Student perspective


The student sees a cartesian coordinate system and a volume with spherical geometry.

It is the task to reconstruct the intervals of a 3D integration in spherical coordinates that results in the volume given. In order to do this they have to find out the radius and angles by rotating the volume with the sliders. That way they can look at different projections of the volume and deduce the limits.

| ![Click draw button](https://user-images.githubusercontent.com/120648145/210994658-7a5c5535-748a-4bfb-948d-82273aa49f4b.PNG) |
|:--:|
| *When the student solves the problem* |

### Teacher perspective
The teacher is able to give a list of possible values for interval bounds. In order to do this, they simply need to modify the entries in the lists specified e.g. change `psiranger:rand([1/6,1/4,1/3,1/2,2/3])` to `psiranger:rand([1/8,1/7,1/3])`. However, if they change this, they have to make sure $\psi$, composed by `phistartr+phiranger` is not larger than 1, since it will be multiplied by $\pi$.

Another example - in the case of the radius - is the following: change `radius1:rand(6)/2` to `radius1: rand(8)/2` in order to select numbers from 0 to 4 in steps of 1/2.

For an explanation of the processing of the values read **Question variables** and **Question text**.

**It is important to make sure that $\psi \le \pi$ and $\phi \le 2 \pi$, when changing values!** 


| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/210994627-72084c36-bbad-45ff-acc2-3ca758ee235f.PNG) |
|:--:|
| *The above image shows which values the teacher may wish to change* |



## Question code

### Question Variables
+	phiranger and phistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	psiranger and psistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	radius1 and radius2 are randomly selected in steps of 1/2 and radius2 is always bigger than radius1  
+	psiranger, phiranger, psistartr and phistartr are multiplied by pi and saved as numerical values. This is done in between `numer:true` and `numer:false`.



#### Question variable code
```jacascript
psiranger:rand([1/6,1/4,1/3,1/2,2/3]);
/* check, that psiranger+psistartr<=1 */
if psiranger>=1/2 then psistartr:rand([1/6,1/4,1/3]) else psistartr:rand([1/6,1/4,1/3,1/2,2/3]);
phiranger:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);
phistartr:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);

radius1: rand(6)/2;
radius2: radius1+(rand(6)+1)/2;

/* Multiply with PI */
/* numerical data for plotting */
numer:true
phirange:phiranger*%pi;
phistart:phistartr*%pi;
psirange:psiranger*%pi;
psistart:psistartr*%pi;
numer:false
/* symbolic data for checking */
phiranger:phiranger*%pi;
phistartr:phistartr*%pi;
psiranger:psiranger*%pi;
psistartr:psistartr*%pi;
```

### Question Text
+	"Given is a 3D volume with spherical geometry. It is defined by the intervals for each of the spherical coordinates $r$, $\phi$ and $\psi$. Here $r$ is the radial coordinate and $\phi$ is the azimuthal angle starting at the $x$-axis oriented counterclockwise with $\phi\in [0, 2 \pi]$. Lastly, $\psi$ is the polar angle measured from the $z$-axis with $\psi\in [0, \pi]$. 

	 The volume is contained in the interval between a smaller and a bigger value of the coordinates.

	 The point of view can be rotated with help of the sliders in the plot. </p>

	**Reconstruct the intervals that define the given volume.** 

	 Write the interval in the form $r\in$`[r1,r2]` and  $\phi\in$ `[phi1,phi2]`, e.g. `[1/2,2]` and `[1/2*pi,2*pi]`.
”
+ Task explanation using LaTex
+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the 3D volume given by the coordinates phi, psi and r
+	`[[input:ans1]]`, `[[input:ans2]]`, `[[input:ans3]]` at the end of JSXGraph code to allow input of  answers of the student for r, phi and psi respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` , `[[validation:ans3]]`  checking of answer

#### Question text code


```javascript
<p>Given is a 3D volume with spherical geometry. It is defined by the intervals for each of the spherical coordinates \(r\), \(\phi\) and \(\psi\). Here \(r\) is the radial coordinate and \(\phi\) is the azimuthal angle starting at the \(x\)-axis oriented counterclockwise with \(\phi\in [0, 2 \pi]\). Lastly, \(\psi\) is the polar angle measured from the \(z\)-axis with \(\psi\in [0, \pi]\). </p>
<p> The volume is contained in the interval between a smaller and a bigger value of the coordinates. </p>
<p> The point of view can be rotated with help of the sliders in the plot. </p>

<p> <b>Reconstruct the intervals that define the given volume. </b> </p> 

<p> Write the interval in the form \(r\in\)<code>[r1,r2]</code> and  \(\phi\in\)<code>[phi1,phi2]</code>, e.g. <code>[1/2,2]</code> and <code>[1/2*pi,2*pi]</code>.</p>

[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

                        var view = board.create('view3d',
		                            [[-6, -3], [8, 8],
		                            [[-5, 5], [-5, 5], [-5, 5]]],
		                            {});

		                       // Transform components of the vector function

		                       var TF1 = (u,v,w) => u * Math.cos(v)* Math.sin(w) ;
		                       var TF2 = (u,v,w) => u * Math.sin(v)* Math.sin(w) ;
		                       var TF3 = (u,v,w) => u * Math.cos(w);

		                     // define Variables init=[xlower, xinit, xupper]

		                     var u1init = [0,1,4];
		                     var u2init = [0,2,4];
		                     var v1init = [0, 0, 6.28];
		                     var v2init = [0, 2, 6.28];
		                     var w1init = [0, 0, 3.14];
		                     var w2init = [0, 2, 3.14];

		// Generate box, !!!! slider adjusted to the init of the board above//
		                        // Create Slider
		                       var u1 = {#radius1#};
		                       var u2 = {#radius2#};
		                       var v1 = {#phistart#};
		                       var v2 = {#phistart#}+{#phirange#};
		                       var w1 = {#psistart#};
		                       var w2 = {#psistart#}+{#psirange#};

		                       // Create transformed box
		                        var c1 = view.create('parametricsurface3d', [
		                            (u, v) => TF1(u,v,w1),
		                            (u, v) => TF2(u,v,w1),
		                            (u, v) => TF3(u,v,w1),
		                            () => [u1, u2],
		                            () => [v1, v2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: true } });

		                        var c2 = view.create('parametricsurface3d', [
		                            (u, v) => TF1(u,v,w2),
		                            (u, v) => TF2(u,v,w2),
		                            (u, v) => TF3(u,v,w2),
		                            () => [u1, u2],
		                            () => [v1, v2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		                        var c3 = view.create('parametricsurface3d', [
		                            (u, w) => TF1(u,v1,w),
		                            (u, w) => TF2(u,v1,w),
		                            (u, w) => TF3(u,v1,w),
		                            () => [u1, u2],
		                            () => [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c4 = view.create('parametricsurface3d', [
		                            (u, w) => TF1(u,v2,w),
		                            (u, w) => TF2(u,v2,w),
		                            (u, w) => TF3(u,v2,w),
		                            () => [u1, u2],
		                            () => [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c5 = view.create('parametricsurface3d', [
		                            (v, w) => TF1(u1,v,w),
		                            (v, w) => TF2(u1,v,w),
		                            (v, w) => TF3(u1,v,w),
		                            () => [v1, v2],
		                            () => [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c6 = view.create('parametricsurface3d', [
		                            (v, w) => TF1(u2,v,w),
		                            (v, w) => TF2(u2,v,w),
		                            (v, w) => TF3(u2,v,w),
		                            () => [v1, v2],
		                            () => [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
board.update();
[[/jsxgraph]]
<p>\(r\in\) [[input:ans1]] [[validation:ans1]]</p>
<p>\(\phi \in\) [[input:ans2]] [[validation:ans2]]</p>
<p>\(\psi\in\)  [[input:ans3]] [[validation:ans3]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[radius1, radius2]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 2
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[phistartr,phistartr+phiranger]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[psistartr,psistartr+psiranger]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|

## Potential response tree
### prt1

Feedback variables:
```
r1:ans1[1]
r2:ans1[2]
phi1:ans2[1]
phi2:ans2[2]
psi1:ans3[1]
psi2:ans3[2]
```

| ![prt1](https://user-images.githubusercontent.com/120648145/210994656-4c46ce7a-ada8-4cc1-8f34-00b47834c019.PNG) |
|:--:|
| *Visualization of **prt1*** |





### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `r1`|
|TAns | `radius1`| 
|Node 1 true feedback | `<p>Nice, you found the correct value for \(r_1\)! Good job! </p>`|
|Node 1 false feedback |`<p>The value you gave for \(r_1\) is not correct. Try rotating the volume such that you see the relevant surface head-on and read the smaller radius from the coordinate system. This is the lower bound of the interval of possible radiuses. Make sure, you're giving the values in the format specified in the task explanation.</p>`|

| ![node1](https://user-images.githubusercontent.com/120648145/210994646-bf7b7a12-ca44-4954-a72b-7522018ac6a7.PNG) |
|:--:|
| *Values of **node 1*** |

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `r2`|
|TAns | `radius2`| 
|Node 2 true feedback | `<p>Nice, you found the correct value for \(r_2\)! Good job!</p>`|
|Node 2 false feedback |`<p>The value you gave for \(r_2\) is not correct. Try rotating the volume such that you see the relevant surface head-on and read the smaller radius from the coordinate system. This is the upper bound of the interval of possible radiuses. Make sure, you're giving the values in the format specified in the task explanation.</p>`|

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `phi1`|
|TAns | `phistartr`| 
|Node 3 true feedback | `<p>Nice, you found the correct value for \(\phi_1\)! Good job!<p>`|
|Node 3 false feedback |`<p>The value you gave for \(\phi_1\) is not correct. Try rotating the volume such that you see the relevant surface head-on and read the smaller angle from the coordinate system taking into account its orientation. This is the lower bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

### Node 4
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `phi2`|
|TAns | `phistartr+phiranger`| 
|Node 4 true feedback | `<p>Nice, you found the correct value for \(\phi_2\)! Good job!<p>`|
|Node 4 false feedback |`<p>The value you gave for \(\phi_2\) is not correct. Try rotating the volume such that you see the relevant surface head-on and read the larger angle from the coordinate system taking into account its orientation. This is the upper bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

### Node 5
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `psi1`|
|TAns | `psistartr`| 
|Node 5 true feedback | `<p>Nice, you found the correct value for \(\psi_1\)! Good job!<p>`|
|Node 5 false feedback |`<p>The value you gave for \(\psi_1\) is not correct. Try rotating the volume such that you see the relevant surface head-on and read the smaller angle from the coordinate system taking into account its orientation. This is the lower bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

### Node 6
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `psi2`|
|TAns | `psistartr+psiranger`| 
|Node 6 true feedback | `<p>Nice, you found the correct value for \(\psi_2\)! Good job!<p>`|
|Node 6 false feedback |`<p>The value you gave for \(\psi_2\) is not correct. Try rotating the volume such that you see the relevant surface head-on and read the larger angle from the coordinate system taking into account its orientation. This is the upper bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|


## Todo:
* [x] Explain orientation of angles
* [x] Give maximal intervalls
* [x] Check in code whether maximal intervalls are correct
* [x] Check whether model solutions are correct
* [x] Replace theta with correct angle
* [ ] Print JSXGraph applet bigger
* [ ] Improve PRT
