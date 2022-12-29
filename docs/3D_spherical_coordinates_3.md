---
title: Example Spherical Coordinates (3)
usemathjax: true
theme: minima
---
## Aim of task
+	Student can take a volume with spherical geometry and reconstruct the limits of its radius and angles (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
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

| ![values the teacher can change](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *The above image shows which values the teacher may wish to change* |

### Questions and answers examples

[insert examples]

## Question code

### Question Variables
+ 	Transformation is defined in 3D with variables `Tx`, `Ty`, `Tz` dependend on u,v,w
+ phiranger and phistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	psiranger and psistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	radius1 and radius2 are randomly selected in steps of 1/2 and radius2 is always bigger than radius1  
+	psiranger, phiranger, psistartr and phistartr are multiplied by pi and saved as numerical values
+ angle orientation is given in text
+ Preparation of correct answers for PRT
+ values for sliders are specified



#### Question variable code
```jacascript
/* define transformation */
Tx:u*cos(v)*sin(w)
Ty:u*sin(v)*sin(w)
Tz:u*sin(w)
/* define interval [r1,r2] */
radius1:rand(6)/2;
radius2:radius1+(rand(6)+1)/2;

/* define angle in the xy-Plane */
/* the factor %pi is handled seperatly, here the rational numbers are processed only*/
phiranger:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);
phistartr:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);
/* check, that phiranger+phistartr<=1 */
if phiranger+phistartr>=1 then phistartr:rand([1/6,1/4,1/3]) ;

/* define angle wrt. z-axes */
psiranger:rand([1/6,1/4,1/3,1/2]);
psistartr:rand([1/6,1/4,1/3,1/2]);

/* define the interval [u1val, u2val], [v1val, v2val], [w1val, w2val]  for JSXGraph*/

/* generate numerical values for JSXGraph drawings */
/* Multiply with PI */
/* numerical data for plotting */
numer:true
u1val:radius1;
u2val:radius2;
v1val:phistartr*%pi;
v2val:v1val+phiranger*%pi;
w1val:psistartr*%pi;
w2val:w1val+psiranger*%pi;
numer:false



/* set teacher answers for default PRTs */
/* the answer will be checked against rational numbers or rational*%pi, symbolic data for checking */
u1tan:radius1;
u2tan:radius2;
v1tan:phistartr*%pi;
v2tan:v1tan+phiranger*%pi;
w1tan:psistartr*%pi;
w2tan:w1tan+psiranger*%pi;


/* definit init values for sliders, students reference volume */
u1init:[0,1,4]
u2init:[0,2,4];
v1init:[0, 0, 6.28];
v2init:[0, 2, 6.28];
w1init:[0, 0, 3.14];
w2init:[0, 2, 3.14];
```

### Question Text
+	“Given the transformation $T:\mathbb{R}^3\to\mathbb{R}^3$ by
$T(u,v,w):=\begin{pmatrix}{@Tx@}\\{@Ty@}\\{@Tz@}\end{pmatrix}$.
Determine the limits of the $u$, $v$ and $w$ to describe the volume show as $T([u1,u2]\times[v1,v2]\times[w1,w2])$. 
Write the interval in the form $u\in$[u1,u2],$v\in$[v1,v2] and $w\in$[w1,w2]., e.g. [1/2,2] or [1/2* pi, 2*pi].
”
+ Task explanation using LaTex
+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the 3D volume given by the coordinates phi, psi and r
+	`[[input:ans1]]`, `[[input:ans2]]`, `[[input:ans3]]` at the end of JSXGraph code to allow input of  answers of the student for r, phi and psi respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` , `[[validation:ans3]]`  checking of answer

#### Question text code


```javascript
<p>Given the transformation \(T:\mathbb{R}^3\to\mathbb{R}^3\) by<br>
\(T(u,v,w):=\begin{pmatrix}{@Tx@}\\{@Ty@}\\{@Tz@}\end{pmatrix}\).</p>
<p>Determine the limits of the \(u\), \(v\) and \(w\) to describe the volume show as 
\(T([u1,u2]\times[v1,v2]\times[w1,w2])\). </p>
<p> Write the interval in the form \(u\in\)<code>[u1,u2]</code>,\(v\in\)<code>[v1,v2]</code> and  \(w\in\)<code>[w1,w2].</code>, e.g. <code>[1/2,2]</code> or <code>[1/2*pi,2*pi]</code>.</p>


[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

                        var view = board.create('view3d',
		                            [[-6, -1.5], [8, 9.5],
		                            [[-5, 5], [-5, 5], [-5, 5]]],
		                            {});

		                       // Transform components of the vector function

		                       /*var TF1 = (u,v,w) =&gt; u*Math.cos(v) * Math.sin(w) ;
		                       var TF2 = (u,v,w) =&gt; u * Math.sin(v)*Math.sin(w);
		                       var TF3 = (u,v,w) =&gt; u*Math.cos(w);*/
		                       var TF1 = board.jc.snippet('{#Tx#}', true, 'u,v,w');
		                       var TF2 = board.jc.snippet('{#Ty#}', true, 'u,v,w');
		                       var TF3 = board.jc.snippet('{#Tz#}', true, 'u,v,w');


		                     // define Variables init=[xlower, xinit, xupper]

		                     var u1init = {#u1init#};
		                     var u2init = {#u2init#};
		                     var v1init = {#v1init#};
		                     var v2init = {#v2init#};
		                     var w1init = {#w1init#};
		                     var w2init = {#w2init#};

		// Generate box, !!!! slider adjusted to the init of the board above//
		                        // Create Slider for control object for student
                       var u1s = board.create('slider', [[-7, -4], [5, -4], u1init], { name: 'u_1' });
                       var u2s = board.create('slider', [[-7, -5], [5, -5], u2init], { name: 'u_2' });
                       var v1s = board.create('slider', [[-7, -6], [5, -6], v1init], { name: 'v_1' });
                       var v2s = board.create('slider', [[-7, -7], [5, -7], v2init], { name: 'v_2' });
                       var w1s = board.create('slider', [[-7, -8], [5, -8], w1init], { name: 'w_1' });
                       var w2s = board.create('slider', [[-7, -9], [5, -9], w2init], { name: 'w_2' });

		                       var u1 = {#u1val#};
		                       var u2 = {#u2val#};
		                       var v1 = {#v1val#};
		                       var v2 = {#v2val#};
		                       var w1 = {#w1val#};
		                       var w2 = {#w2val#};

		                       // Create transformed box
		                        var c1 = view.create('parametricsurface3d', [
		                            (u, v) =&gt; TF1(u,v,w1),
		                            (u, v) =&gt; TF2(u,v,w1),
		                            (u, v) =&gt; TF3(u,v,w1),
		                            () =&gt; [u1, u2],
		                            () =&gt; [v1, v2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: true } });

		                        var c2 = view.create('parametricsurface3d', [
		                            (u, v) =&gt; TF1(u,v,w2),
		                            (u, v) =&gt; TF2(u,v,w2),
		                            (u, v) =&gt; TF3(u,v,w2),
		                            () =&gt; [u1, u2],
		                            () =&gt; [v1, v2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		                        var c3 = view.create('parametricsurface3d', [
		                            (u, w) =&gt; TF1(u,v1,w),
		                            (u, w) =&gt; TF2(u,v1,w),
		                            (u, w) =&gt; TF3(u,v1,w),
		                            () =&gt; [u1, u2],
		                            () =&gt; [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c4 = view.create('parametricsurface3d', [
		                            (u, w) =&gt; TF1(u,v2,w),
		                            (u, w) =&gt; TF2(u,v2,w),
		                            (u, w) =&gt; TF3(u,v2,w),
		                            () =&gt; [u1, u2],
		                            () =&gt; [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c5 = view.create('parametricsurface3d', [
		                            (v, w) =&gt; TF1(u1,v,w),
		                            (v, w) =&gt; TF2(u1,v,w),
		                            (v, w) =&gt; TF3(u1,v,w),
		                            () =&gt; [v1, v2],
		                            () =&gt; [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c6 = view.create('parametricsurface3d', [
		                            (v, w) =&gt; TF1(u2,v,w),
		                            (v, w) =&gt; TF2(u2,v,w),
		                            (v, w) =&gt; TF3(u2,v,w),
		                            () =&gt; [v1, v2],
		                            () =&gt; [w1, w2]
		                        ], { strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		                       // Create transformed box - student

		                        var c1s = view.create('parametricsurface3d', [
		                            (u, v) =&gt; TF1(u,v,w1s.Value()),
		                            (u, v) =&gt; TF2(u,v,w1s.Value()),
		                            (u, v) =&gt; TF3(u,v,w1s.Value()),
		                            () =&gt; [u1s.Value(), u2s.Value()],
		                            () =&gt; [v1s.Value(), v2s.Value()]
		                        ], { strokeColor:'red', 
                                             strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: true } });

		                        var c2s = view.create('parametricsurface3d', [
		                            (u, v) =&gt; TF1(u,v,w2s.Value()),
		                            (u, v) =&gt; TF2(u,v,w2s.Value()),
		                            (u, v) =&gt; TF3(u,v,w2s.Value()),
		                            () =&gt; [u1s.Value(), u2s.Value()],
		                            () =&gt; [v1s.Value(), v2s.Value()]
		                        ], { strokeColor:'red', 
                                             strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		                        var c3s = view.create('parametricsurface3d', [
		                            (u, w) =&gt; TF1(u,v1s.Value(),w),
		                            (u, w) =&gt; TF2(u,v1s.Value(),w),
		                            (u, w) =&gt; TF3(u,v1s.Value(),w),
		                            () =&gt; [u1s.Value(), u2s.Value()],
		                            () =&gt; [w1s.Value(), w2s.Value()]
		                        ], { strokeColor:'red', 
                                             strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c4s = view.create('parametricsurface3d', [
		                            (u, w) =&gt; TF1(u,v2s.Value(),w),
		                            (u, w) =&gt; TF2(u,v2s.Value(),w),
		                            (u, w) =&gt; TF3(u,v2s.Value(),w),
		                            () =&gt; [u1s.Value(), u2s.Value()],
		                            () =&gt; [w1s.Value(), w2s.Value()]
		                        ], { strokeColor:'red', 
                                             strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c5s = view.create('parametricsurface3d', [
		                            (v, w) =&gt; TF1(u1s.Value(),v,w),
		                            (v, w) =&gt; TF2(u1s.Value(),v,w),
		                            (v, w) =&gt; TF3(u1s.Value(),v,w),
		                            () =&gt; [v1s.Value(), v2s.Value()],
		                            () =&gt; [w1s.Value(), w2s.Value()]
		                        ], {strokeColor:'red', 
                                             strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        var c6s = view.create('parametricsurface3d', [
		                            (v, w) =&gt; TF1(u2s.Value(),v,w),
		                            (v, w) =&gt; TF2(u2s.Value(),v,w),
		                            (v, w) =&gt; TF3(u2s.Value(),v,w),
		                            () =&gt; [v1s.Value(), v2s.Value()],
		                            () =&gt; [w1s.Value(), w2s.Value()]
		                        ], { strokeColor:'red', 
                                             strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

board.update();
[[/jsxgraph]]
<p>\(u\in\) [[input:ans1]] [[validation:ans1]]</p>
<p>\(v \in\) [[input:ans2]] [[validation:ans2]]</p>
<p>\(w\in\)  [[input:ans3]] [[validation:ans3]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[u1tan,u2tan]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 2
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[v1tan,v2tan]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `[w1tan,w2tan]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|

## Potential response tree
### prt1

Feedback variables: `u1san:ans1[1]`


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | u1san|
|TAns | u1tan| 
|Node 1 true feedback | \\(r_1\\) is correct.|
|Node 1 false feedback | \\(r_1\\) is not correct.|

### prt2

Feedback variables: `u2san:ans1[2]`


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | u2san|
|TAns | u2tan| 
|Node 1 true feedback | \\(r_2\\) is correct.|
|Node 1 false feedback | \\(r_2\\) is not correct. {@r2@}, {@radius2@}|

### prt3

Feedback variables: `v1san:ans2[1]`


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | v1san|
|TAns | v1tan| 
|Node 1 true feedback | \\(\phi_1\\) is correct. {@phi1@}, {@phistartr@}|
|Node 1 false feedback | \\(\phi_1\\) is not correct.|

### prt4

Feedback variables: `v2san:ans2[2]`


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | v2san|
|TAns | v2tan| 
|Node 1 true feedback | \\(\phi_2\\) is correct. |
|Node 1 false feedback | \\(\phi_2\\) is not correct.|

### prt5

Feedback variables: `w1san:ans3[1]`


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | w1san|
|TAns | w1tan| 
|Node 1 true feedback | \\(\psi_1\\) is correct.|
|Node 1 false feedback | \\(\psi_1\\) is not correct.|

### prt6

Feedback variables: `psi2:ans3[2]`


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns |w2san|
|TAns | w2tan| 
|Node 1 true feedback | \\(\psi_2\\) is correct.|
|Node 1 false feedback | \\(\psi_2\\) is not correct.|

## Todo:
* [ ] **JSXGraph applet is not working currently**
* [ ] enable other coordinate systems: spherical coordinates are defined explicitly in JSXGraph code again --> not possible to switch to e.g. cylindrical coordinates
* [ ] ensure consistency in u,v,w and r, phi, psi notation
* [ ] Explain orientation of angles
* [ ] Give maximal intervalls
* [ ] Check in code whether maximal intervalls are correct
* [ ] Check whether model solutions are correct
* [ ] Replace theta with correct angle
* [ ] Print JSXGraph applet bigger
* [ ] make square appear as such
* [ ] Simplify and improve PRT
