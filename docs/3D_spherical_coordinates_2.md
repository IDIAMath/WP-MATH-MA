---
title: Example Spherical Coordinates (2)
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows the transformation from cartesian to spherical coordinates  (Handling mathematical symbols and formalism)
+	Student can take a volume with spherical geometry and reconstruct the limits of its radius and angles (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://user-images.githubusercontent.com/120648145/209998772-0bdef5e1-4e5e-46b4-bca4-25798398254f.PNG) |
|:--:|
| *First impression of the question* |

## Question description

A 3D volume is plotted. It is a randomly generated section of a ball in spherical coordinates.
An additional 3D section of a ball is plotted that can be varied using sliders.
That way, by matching the two volumes, the intervalls of radius and angles can be interactively obtained.
The task is to find the correct intervalls for $r$, $\phi$ and $\psi$ in real numbers that construct the generated volume in sperical coordinates.


### Student perspective

[describe what the student will see]

| ![Click draw button](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
[describe what the teacher needs to do and can do]

| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/209998765-cc7196b5-bc98-44b8-906c-72f1c5d953e3.PNG) |
|:--:|
| *The above image shows which values the teacher may wish to change* |

### Questions and answers examples

[insert examples]

## Question code

### Question Variables
+	phiranger and phistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	psiranger and psistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	radius1 and radius2 are randomly selected in steps of 1/2 and radius2 is always bigger than radius1  
+	psiranger, phiranger, psistartr and phistartr are multiplied by pi and saved as numerical values



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

	**Reconstruct the intervals that define the given volume by matching the volumes using the sliders.** 

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

<p> <b>Reconstruct the intervals that define the given volume by matching the volumes using the sliders. </b> </p> 

<p> Write the interval in the form \(r\in\)<code>[r1,r2]</code> and  \(\phi\in\)<code>[phi1,phi2]</code>, e.g. <code>[1/2,2]</code> and <code>[1/2*pi,2*pi]</code>.</p>

[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']] 

	var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false}); 
	var view = board.create('view3d',
		        [[-6, -1.5], [8, 8],
		        [[-5, 5], [-5, 5], [-5, 5]]],
		        {});
			// Transform components of the vector function
							
			var TF1 = (u,v,w) => u * Math.cos(v) * Math.sin(w) ;
		    var TF2 = (u,v,w) => u * Math.sin(v) * Math.sin(w) ;
		    var TF3 = (u,v,w) => u * Math.cos(w) ;

		    // define Variables init=[xlower, xinit, xupper]

		    var u1init = [0,1,4];
		    var u2init = [0,2,4];
		    var v1init = [0, 0, 6.28];
		    var v2init = [0, 2, 6.28];
		    var w1init = [0, 0, 3.14];
		    var w2init = [0, 2, 3.14];

			// Generate box, !!!! slider adjusted to the init of the board above//
		    // Create Slider for control object for student
            var u1s = board.create('slider', [[-7, -4.5], [3, -4.5], u1init], { name: 'r_1' });
            var u2s = board.create('slider', [[-7, -5.5], [3, -5.5], u2init], { name: 'r_2' });
            var v1s = board.create('slider', [[-7, -6.5], [3, -6.5], v1init], { name: '\phi_1' });
            var v2s = board.create('slider', [[-7, -7.5], [3, -7.5], v2init], { name: '\phi_2' });
            var w1s = board.create('slider', [[-7, -8.5], [3, -8.5], w1init], { name: '\psi_1' });
            var w2s = board.create('slider', [[-7, -9.5], [3, -9.5], w2init], { name: '\psi_2' });
            
			

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
		        ], { strokeWidth: 1, strokeOpacity: 0.6,
					mesh3d: { visible: true } });

		    var c2 = view.create('parametricsurface3d', [
		        (u, v) => TF1(u,v,w2),
		        (u, v) => TF2(u,v,w2),
		        (u, v) => TF3(u,v,w2),
		        () => [u1, u2],
		        () => [v1, v2]
		        ], { strokeWidth: 1, strokeOpacity: 0.6,
					mesh3d: { visible: false } });

		    var c3 = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v1,w),
		        (u, w) => TF2(u,v1,w),
		        (u, w) => TF3(u,v1,w),
		        () => [u1, u2],
		        () => [w1, w2]
		        ], { strokeWidth: 1, strokeOpacity: 0.6,
					mesh3d: { visible: false } });
		                    
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
			
			
		    // Create transformed box - student

		    var c1s = view.create('parametricsurface3d', [
		        (u, v) => TF1(u,v,w1s.Value()),
		        (u, v) => TF2(u,v,w1s.Value()),
		        (u, v) => TF3(u,v,w1s.Value()),
		        () => [u1s.Value(), u2s.Value()],
		        () => [v1s.Value(), v2s.Value()]
		        ], { strokeColor:'red', 
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: true } });

		    var c2s = view.create('parametricsurface3d', [
		        (u, v) => TF1(u,v,w2s.Value()),
		        (u, v) => TF2(u,v,w2s.Value()),
		        (u, v) => TF3(u,v,w2s.Value()),
		        () => [u1s.Value(), u2s.Value()],
		        () => [v1s.Value(), v2s.Value()]
		        ], { strokeColor:'red', 
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		    var c3s = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v1s.Value(),w),
		        (u, w) => TF2(u,v1s.Value(),w),
		        (u, w) => TF3(u,v1s.Value(),w),
		        () => [u1s.Value(), u2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], { strokeColor:'red', 
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c4s = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v2s.Value(),w),
		        (u, w) => TF2(u,v2s.Value(),w),
		        (u, w) => TF3(u,v2s.Value(),w),
		        () => [u1s.Value(), u2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], { strokeColor:'red', 
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c5s = view.create('parametricsurface3d', [
		        (v, w) => TF1(u1s.Value(),v,w),
		        (v, w) => TF2(u1s.Value(),v,w),
		        (v, w) => TF3(u1s.Value(),v,w),
		        () => [v1s.Value(), v2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], {strokeColor:'red', 
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c6s = view.create('parametricsurface3d', [
		        (v, w) => TF1(u2s.Value(),v,w),
		        (v, w) => TF2(u2s.Value(),v,w),
		        (v, w) => TF3(u2s.Value(),v,w),
		        () => [v1s.Value(), v2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], { strokeColor:'red', 
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
			
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
|Model answer | `[radius1,radius2]` defined in **Question variables** |
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

| ![prt1](https://user-images.githubusercontent.com/120648145/209998779-1117f249-7b2f-49d2-bbd9-e0e42368d7eb.PNG) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `r1`|
|TAns | `radius1`| 
|Node 1 true feedback | `<p>Nice, you found the correct value for \(r_1\)! Good job! </p>`|
|Node 1 false feedback |`<p>The value you gave for \(r_1\) is not correct. Try matching the volumes using the sliders and read the smaller radius from the coordinate system. This is the lower bound of the interval of possible radiuses. Make sure, you're giving the values in the format specified in the task explanation.</p>`|


| ![Node 1](https://user-images.githubusercontent.com/120648145/209998776-cfa51f7e-9a9a-4695-bc7d-376f25c109e7.PNG) |
|:--:|
| *Values of **node 1*** |

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `r2`|
|TAns | `radius2`| 
|Node 2 true feedback | `<p>Nice, you found the correct value for \(r_2\)! Good job!</p>`|
|Node 2 false feedback |`<p>The value you gave for \(r_2\) is not correct. Try matching the volumes using the sliders and read the smaller radius from the coordinate system. This is the upper bound of the interval of possible radiuses. Make sure, you're giving the values in the format specified in the task explanation.</p>`|

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `phi1`|
|TAns | `phistartr`| 
|Node 3 true feedback | `<p>Nice, you found the correct value for \(\phi_1\)! Good job!<p>`|
|Node 3 false feedback |`<p>The value you gave for \(\phi_1\) is not correct. Try matching the volumes using the sliders and read the smaller angle from the coordinate system taking into account its orientation. This is the lower bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

### Node 4
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `phi2`|
|TAns | `phistartr+phiranger`| 
|Node 4 true feedback | `<p>Nice, you found the correct value for \(\phi_2\)! Good job!<p>`|
|Node 4 false feedback |`<p>The value you gave for \(\phi_2\) is not correct. Try matching the volumes using the sliders and read the larger angle from the coordinate system taking into account its orientation. This is the upper bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

### Node 5
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `psi1`|
|TAns | `psistartr`| 
|Node 5 true feedback | `<p>Nice, you found the correct value for \(\psi_1\)! Good job!<p>`|
|Node 5 false feedback |`<p>The value you gave for \(\psi_1\) is not correct. Try matching the volumes using the sliders and read the smaller angle from the coordinate system taking into account its orientation. This is the lower bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

### Node 6
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `psi2`|
|TAns | `psistartr+psiranger`| 
|Node 6 true feedback | `<p>Nice, you found the correct value for \(\psi_2\)! Good job!<p>`|
|Node 6 false feedback |`<p>The value you gave for \(\psi_2\) is not correct. Try matching the volumes using the sliders and read the larger angle from the coordinate system taking into account its orientation. This is the upper bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. </p>`|

## Todo:
* [x] **JSXGraph applet does not work currently**
* [x] Explain orientation of angles
* [x] Give maximal intervalls
* [x] Check in code whether maximal intervalls are correct
* [x] Check whether model solutions are correct
* [x] Replace theta with correct angle
* [ ] Print JSXGraph applet bigger
* [ ] make square appear as such
* [x] Simplify and improve PRT
* [ ] Update Images and description
* [ ] Further improve PRT
* [ ] Remove extra PRTs
