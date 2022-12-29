---
title: Example Spherical Coordinates
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows the transformation from cartesian to spherical coordinates  (Handling mathematical symbols and formalism)
+	Student can take a volume with spherical geometry and reconstruct the limits of its radius and angles (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://user-images.githubusercontent.com/120648145/209998696-1ee2b6d4-1da2-4064-87b3-23af814004fe.PNG) |
|:--:|
| *First impression of the question* |

## Question description

A 3D volume is plotted. It is a randomly generated section of a ball in spherical coordinates.

The task is to find the correct intervalls for $r$, $\phi$ and $\psi$ in real numbers that construct the generated volume in sperical coordinates.


### Student perspective

[describe what the student will see]




### Teacher perspective
[describe what the teacher needs to do and can do]

| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/209998687-f82d15ab-b25f-4e98-89b0-1044f6d9bd83.PNG) |
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
phiranger:rand([1/6,1/4,1/3,1/2,2/3]);
/* check, that phiranger+phistartr<=1 */
if phiranger>=1/2 then phistartr:rand([1/6,1/4,1/3]) else phistartr:rand([1/6,1/4,1/3,1/2,2/3]);
psiranger:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);
psistartr:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);

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
+	“Determine the limits of the $r$, $\phi$ and $\theta$ in the spherical coordinates. Write the interval in the form $r\in$[r1,r2] and $\phi\in$[phi1,phi2]., e.g. [1/2,2] and [1/2* pi,2*pi]”
+ Task explanation using LaTex
+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the 3D volume given by the coordinates phi, psi and r
+	`[[input:ans1]]`, `[[input:ans2]]`, `[[input:ans3]]` at the end of JSXGraph code to allow input of  answers of the student for r, phi and psi respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` , `[[validation:ans3]]`  checking of answer

#### Question text code


```javascript
<p>Determine the limits of the \(r\), \(\phi\) and \(\theta\) in the spherical coordinates?</p>
<p> Write the interval in the form \(r\in\)<code>[r1,r2]</code> and  \(\phi\in\)<code>[phi1,phi2].</code>, e.g. <code>[1/2,2]</code> and <code>[1/2*pi,2*pi]</code></p>

[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

                        var view = board.create('view3d',
		                            [[-6, -3], [8, 8],
		                            [[-5, 5], [-5, 5], [-5, 5]]],
		                            {});

		                       // Transform components of the vector function

		                       var TF1 = (u,v,w) => u*Math.cos(v) * Math.sin(w) ;
		                       var TF2 = (u,v,w) => u * Math.sin(v)*Math.sin(w);
		                       var TF3 = (u,v,w) => u*Math.cos(w);

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
|Model answer | `[phistart,phistart+phirange]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[psistart,psistart+psirange]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|

## Potential response tree
### prt1

| ![prt1](https://user-images.githubusercontent.com/120648145/209998699-350a22b1-ed52-4698-b321-bfe65a5b2e80.PNG) |
|:--:|
| *Visualization of **prt1*** |

Feedback variables:

`distSqrd: (ans1-centre).(ans1-centre);` 
`radiusSqrd: radius^2;`



### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | Num-GT|
|SAns | radisuSqrd|
|TAns | distSqrd| 
|Node 1 true feedback | fine|
|Node 1 false feedback |not fine|


## Todo:
* [ ] Explain orientation of angles
* [ ] Give maximal intervalls
* [ ] Check in code whether maximal intervalls are correct
* [ ] Check whether model solutions are correct
* [ ] Replace theta with correct angle
* [ ] Print JSXGraph applet bigger
* [ ] Improve PRT
