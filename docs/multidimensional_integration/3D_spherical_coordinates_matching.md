---
title: Spherical Coordinates Matching
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows the transformation from cartesian to spherical coordinates  (Handling mathematical symbols and formalism)
+	Student can take a volume with spherical geometry and reconstruct the limits of its radius and angles (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://private-user-images.githubusercontent.com/120648145/240959221-79653916-5814-4343-9ccd-e359c45f1a77.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MjQwLCJuYmYiOjE2ODUwMjc5NDAsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTIyMS03OTY1MzkxNi01ODE0LTQzNDMtOWNjZC1lMzU5YzQ1ZjFhNzcucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTAwWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZmUzMDI3NGVjMTJmNjNiODNjNDIyYzQzODA5Mjc2MGRkNzg1MmZmYTM1NjJlMjBkOTM3M2Q5NmMzNDI2NGFjMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.dPI7SWiFAvkLqADF_SngkWW_ariuvK_e9kgTly70aoI) |
|:--:|
| *First impression of the question* |

## Question description

A 3D volume is plotted. It is a randomly generated section of a ball in spherical coordinates.
An additional 3D section of a ball is plotted that can be varied using sliders.
That way, by matching the two volumes, the intervalls of radius and angles can be interactively obtained.
The task is to find the correct intervalls for $r$, $\phi$ and $\psi$ in real numbers that construct the generated volume in sperical coordinates.


### Student perspective

The student sees a cartesian coordinate system and a volume with spherical geometry.

It is the task to reconstruct the intervals of a 3D integration in spherical coordinates that results in the volume given. In order to do this they have to find out the radius and angles by matching a second volume to the given one using sliders. If they overlap exactly, the interval bounds can be read from the sliders. The values have to be given in an exact algebraic manner.

| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240959207-fd37658b-a50a-4639-985d-dc299731c5c9.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MjQwLCJuYmYiOjE2ODUwMjc5NDAsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTIwNy1mZDM3NjU4Yi1hNTBhLTQ2MzktOTg1ZC1kYzI5OTczMWM1YzkucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTAwWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZWNmMDRlODU5NDhhNzA5NTJjY2VhNWNiZjg4NjE0MWRmNmM2MTk0NTM0NDQxMDk2ZjM2Y2Y3MzM4MjVhMGZmZSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.c-_sZ56WYgHpen1GKccWU1G6Zc9GCc_Wmu2bJlTzUSY) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for interval bounds. In order to do this, they simply need to modify the entries in the lists specified e.g. change `psiranger:rand([1/6,1/4,1/3,1/2,2/3])` to `psiranger:rand([1/8,1/7,1/3])`. However, if they change this, they have to make sure $\psi$, composed by `phistartr+phiranger` is not larger than 1, since it will be multiplied by $\pi$.

Another example - in the case of the radius - is the following: change `radius1:rand(6)/2` to `radius1: rand(8)/2` in order to select numbers from 0 to 4 in steps of 1/2.

For an explanation of the processing of the values read **Question variables** and **Question text**.

**It is important to make sure that $\psi \le \pi$ and $\phi \le 2 \pi$, when changing values!** 

| ![values the teacher can change](https://private-user-images.githubusercontent.com/120648145/240959218-774d4f98-a379-4270-91de-e7b1dff39114.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MjQwLCJuYmYiOjE2ODUwMjc5NDAsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTIxOC03NzRkNGY5OC1hMzc5LTQyNzAtOTFkZS1lN2IxZGZmMzkxMTQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTAwWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NWIwOGQ5MDUxNGY4ZjU1M2FmZTM2ZWJiYTFjOWRmMGQ0NWRmMTVmMzcwZmI1ZjM3NzNlN2Y4OWExZGYyMjhmYiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.Rpb61PJaR2bhq1sDyM2a5knZWIZmzDNOUgCmaHoukeM) |
|:--:|
| *The above image shows which values the teacher may wish to change* |


## Question code

### Question Variables
+	phiranger and phistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	psiranger and psistartr take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	radius1 and radius2 are randomly selected in steps of 1/2 and radius2 is always bigger than radius1  
+	psiranger, phiranger, psistartr and phistartr are multiplied by pi and saved as numerical values. This is done in between `numer:true` and `numer:false`.



#### Question variable code
```
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

	Reconstruct the intervals that define the given volume."

+ Task explanation using LaTex
+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the 3D volume given by the coordinates phi, psi and r
+	`[[input:ans1]]`, `[[input:ans2]]`, `[[input:ans3]]`,`[[input:ans4]]`, `[[input:ans5]]`, `[[input:ans6]]` at the end of JSXGraph code to allow input of  answers of the student for r, phi and psi respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` , `[[validation:ans3]]`,`[[validation:ans4]]`,  `[[validation:ans5]]` , `[[validation:ans6]]`  checking of answer

#### Question text code


```javascript
<p>Given is a 3D volume with spherical geometry. It is defined by the intervals for each of the spherical coordinates \(r\), \(\phi\) and \(\psi\). Here \(r\) is the radial coordinate and \(\phi\) is the azimuthal angle starting at the \(x\)-axis oriented counterclockwise with \(\phi\in [0, 2 \pi]\). Lastly, \(\psi\) is the polar angle measured from the \(z\)-axis with \(\psi\in [0, \pi]\). </p>

<p> Reconstruct the intervals that define the given volume.  </p> 

[[jsxgraph width="500px" height="500px"  input-ref-ans1='ans1Ref' input-ref-ans2='ans2Ref' input-ref-ans3='ans3Ref' input-ref-ans4='ans4Ref' input-ref-ans5='ans5Ref' input-ref-ans6='ans6Ref']]
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
		    var u2init = [0,2,6];
		    var v1init = [0, 0, 6.28];
		    var v2init = [0, 2, 6.28];
		    var w1init = [0, 0, 3.14];
		    var w2init = [0, 2, 3.14];

			// Generate box, !!!! slider adjusted to the init of the board above//
		    // Create Slider for control object for student
            var u1s = board.create('slider', [[-7, -4.5], [3, -4.5], u1init], { name: 'r_1',snapwidth:0.1, highline: {strokeColor: '#EE442F'}, baseline: {strokeColor: '#EE442F'}});
            var u2s = board.create('slider', [[-7, -5.5], [3, -5.5], u2init], { name: 'r_2',snapwidth:0.1, highline: {strokeColor: '#EE442F'}, baseline: {strokeColor: '#EE442F'}});
            var v1s = board.create('slider', [[-7, -6.5], [3, -6.5], v1init], { name: '\phi_1',snapwidth:0.05, highline: {strokeColor: '#EE442F'}, baseline: {strokeColor: '#EE442F'}});
            var v2s = board.create('slider', [[-7, -7.5], [3, -7.5], v2init], { name: '\phi_2',snapwidth:0.05, highline: {strokeColor: '#EE442F'}, baseline: {strokeColor: '#EE442F'}});
            var w1s = board.create('slider', [[-7, -8.5], [3, -8.5], w1init], { name: '\psi_1',snapwidth:0.05, highline: {strokeColor: '#EE442F'}, baseline: {strokeColor: '#EE442F'}});
            var w2s = board.create('slider', [[-7, -9.5], [3, -9.5], w2init], { name: '\psi_2',snapwidth:0.05, highline: {strokeColor: '#EE442F'}, baseline: {strokeColor: '#EE442F'}});

		    

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
		        ], { strokeColor: "#1f84bc",strokeWidth: 1, strokeOpacity: 0.6,
					mesh3d: { visible: true }});

		    var c2 = view.create('parametricsurface3d', [
		        (u, v) => TF1(u,v,w2),
		        (u, v) => TF2(u,v,w2),
		        (u, v) => TF3(u,v,w2),
		        () => [u1, u2],
		        () => [v1, v2]
		        ], { strokeColor: "#1f84bc",strokeWidth: 1, strokeOpacity: 0.6,
					mesh3d: { visible: false } });

		    var c3 = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v1,w),
		        (u, w) => TF2(u,v1,w),
		        (u, w) => TF3(u,v1,w),
		        () => [u1, u2],
		        () => [w1, w2]
		        ], { strokeColor: "#1f84bc",strokeWidth: 1, strokeOpacity: 0.6,
					mesh3d: { visible: false } });
		                    
			var c4 = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v2,w),
		        (u, w) => TF2(u,v2,w),
		        (u, w) => TF3(u,v2,w),
		        () => [u1, u2],
		        () => [w1, w2]
		        ], { strokeColor: "#1f84bc",strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c5 = view.create('parametricsurface3d', [
		        (v, w) => TF1(u1,v,w),
		        (v, w) => TF2(u1,v,w),
		        (v, w) => TF3(u1,v,w),
		        () => [v1, v2],
		        () => [w1, w2]
		        ], { strokeColor: "#1f84bc",strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                
			var c6 = view.create('parametricsurface3d', [
		        (v, w) => TF1(u2,v,w),
		        (v, w) => TF2(u2,v,w),
		        (v, w) => TF3(u2,v,w),
		        () => [v1, v2],
		        () => [w1, w2]
		        ], { strokeColor: "#1f84bc",strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
			
			
		    // Create transformed box - student

		    var c1s = view.create('parametricsurface3d', [
		        (u, v) => TF1(u,v,w1s.Value()),
		        (u, v) => TF2(u,v,w1s.Value()),
		        (u, v) => TF3(u,v,w1s.Value()),
		        () => [u1s.Value(), u2s.Value()],
		        () => [v1s.Value(), v2s.Value()]
		        ], {strokeColor: "#EE442F",
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: true } });

		    var c2s = view.create('parametricsurface3d', [
		        (u, v) => TF1(u,v,w2s.Value()),
		        (u, v) => TF2(u,v,w2s.Value()),
		        (u, v) => TF3(u,v,w2s.Value()),
		        () => [u1s.Value(), u2s.Value()],
		        () => [v1s.Value(), v2s.Value()]
		        ], {strokeColor: "#EE442F",
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		    var c3s = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v1s.Value(),w),
		        (u, w) => TF2(u,v1s.Value(),w),
		        (u, w) => TF3(u,v1s.Value(),w),
		        () => [u1s.Value(), u2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], { strokeColor: "#EE442F",
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c4s = view.create('parametricsurface3d', [
		        (u, w) => TF1(u,v2s.Value(),w),
		        (u, w) => TF2(u,v2s.Value(),w),
		        (u, w) => TF3(u,v2s.Value(),w),
		        () => [u1s.Value(), u2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], { strokeColor: "#EE442F",
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c5s = view.create('parametricsurface3d', [
		        (v, w) => TF1(u1s.Value(),v,w),
		        (v, w) => TF2(u1s.Value(),v,w),
		        (v, w) => TF3(u1s.Value(),v,w),
		        () => [v1s.Value(), v2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], {strokeColor: "#EE442F",
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });
		                        
			var c6s = view.create('parametricsurface3d', [
		        (v, w) => TF1(u2s.Value(),v,w),
		        (v, w) => TF2(u2s.Value(),v,w),
		        (v, w) => TF3(u2s.Value(),v,w),
		        () => [v1s.Value(), v2s.Value()],
		        () => [w1s.Value(), w2s.Value()]
		        ], { strokeColor: "#EE442F",
                    strokeWidth: 1, strokeOpacity: 0.6, mesh3d: { visible: false } });

		        stack_jxg.bind_slider(ans1Ref,u1s);
			stack_jxg.bind_slider(ans2Ref,u2s);
			stack_jxg.bind_slider(ans3Ref,v1s);
			stack_jxg.bind_slider(ans4Ref,v2s);
			stack_jxg.bind_slider(ans5Ref,w1s);
			stack_jxg.bind_slider(ans6Ref,w2s);	

/* axis labels*/
                       var xlabel=view.create('point3d',[0.9*box[1],0,(0.6*box[0]+0.4*box[1])], {size:0,name:"x"});
                       var ylabel=view.create('point3d',[0,0.9*box[1],(0.6*box[0]+0.4*box[1])], {size:0,name:"y"});
                       var zlabel=view.create('point3d',[
                           0.7*(0.6*box[0]+0.4*box[1]),
                           0.7*(0.6*box[0]+0.4*box[1]),
                           0.9*box[1]], 
                           {size:0,name:"z"});
			board.update(); 
[[/jsxgraph]]
<p>\(r_1=\) [[input:ans1]] [[validation:ans1]]</p>
<p>\(r_2=\) [[input:ans2]] [[validation:ans2]]</p>
<p>\(\phi_1 =\) [[input:ans3]] [[validation:ans3]]</p>
<p>\(\phi_2 =\) [[input:ans4]] [[validation:ans4]]</p>
<p>\(\psi_1=\)  [[input:ans5]] [[validation:ans5]]</p>
<p>\(\psi_2=\)  [[input:ans6]] [[validation:ans6]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `radius1` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 2
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `radius2` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `phistartr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
### Answer ans 4
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `phistartr+phiranger` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 5
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `psistartr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 6
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `psistartr+psiranger` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|

## Potential response tree
### prt1

Feedback variables:
```
r1:ans1
r2:ans2

```

| ![prt1](https://private-user-images.githubusercontent.com/120648145/240959464-966f4706-8809-4824-8494-ab8175aeada4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4Mjk3LCJuYmYiOjE2ODUwMjc5OTcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTQ2NC05NjZmNDcwNi04ODA5LTQ4MjQtODQ5NC1hYjgxNzVhZWFkYTQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTU3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9Y2VhZGM0YjY3OTdhZDZkOTFhNjNlMTEwNWQ3NTlmNzhiYzRiNWEzNjM4NTgxMTdlYzM3MjBmZjIyNTRjMjdlZSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.8oPOeoVPk0-qZZk9uUqNrySMZennSNs9ig0uFCfGh1w) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `r1`|
|TAns | `radius1`| 
|Node 1 true feedback | `<p>Nice, you found the correct value for \(r_1\)! Good job!</p>`|
|Node 1 false feedback |`<p>The value you gave for \(r_1\) is not correct.  </p>`|


| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240959467-41247bb2-e583-4d6d-b147-836b9a97ef00.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4Mjk3LCJuYmYiOjE2ODUwMjc5OTcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTQ2Ny00MTI0N2JiMi1lNTgzLTRkNmQtYjE0Ny04MzZiOWE5N2VmMDAucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTU3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9Y2MzZmU1Y2UwM2MyZGRiNzgzNDhhOTRiNDQwZjgzYWM2MGVlN2RlNTIwZTIwNjExNDJkNjZmYTBmODRiYzU2ZSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.EQKiw4Pxp_MlqvuQdjIAA3IMUP9PPNTDRVeoRaNRauk) |
|:--:|
| *Values of **node 1*** |

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `r2`|
|TAns | `radius2`| 
|Node 2 true feedback | `<p>Nice, you found the correct value for \(r_2\)! Good job!</p> <p> Perfect! You got both radiuses right! </p>`|
|Node 2 false feedback |`<p>The value you gave for \(r_2\) is not correct. Try matching the points perfectly and read the larger radius. </p>`|

| ![Node 2](https://private-user-images.githubusercontent.com/120648145/240959458-79501a9d-8fb8-470f-b93a-d5e62d09c798.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4Mjk3LCJuYmYiOjE2ODUwMjc5OTcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTQ1OC03OTUwMWE5ZC04ZmI4LTQ3MGYtYjkzYS1kNWU2MmQwOWM3OTgucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTU3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NTMzMDc4NjZlMTJlZGJlYWY2ZDc5ZDAxMTA0NjIyZjE0ZGUyM2UxN2UwNDk5NmY3Yzk3ODEyZDYyYWExNGYyYSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.CxrqEQc8r3BTowletX4u5oVWps6V09geMITzn-HVNUQ) |
|:--:|
| *Values of **node 2*** |


### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `r2`|
|TAns | `radius2`| 
|Node 3 true feedback | `<p>Nice, you found the correct value for \(r_2\)! Good job!</p> <p>Check whether you did anything different here than for \(r_1\) and try again. </p>`|
|Node 3 false feedback |`<p>The value you gave for \(r_2\) is also not correct. Try matching the points perfectly and read the radiuses. The smaller radius is the lower bound of the interval. The larger radius is the upper bound of the interval. </p>`|

| ![Node 3](https://private-user-images.githubusercontent.com/120648145/240959462-036c8eff-740a-49fb-b39e-f41a0767ba42.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4Mjk3LCJuYmYiOjE2ODUwMjc5OTcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTQ2Mi0wMzZjOGVmZi03NDBhLTQ5ZmItYjM5ZS1mNDFhMDc2N2JhNDIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUxOTU3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YTY0YTFlYTg2MjUwOTdhYjJlMTcwYzk2NDk1ZGI1YmM4MDU2Mjg1NGIzMzM0NGY4MmYwZjhkNzcxMWExMDAyMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.tg7QperEwTpCwq5waltUIzl-qDhkfs9azImvX_xUrY0) |
|:--:|
| *Values of **node 3*** |


### prt2

Feedback variables:
```
phi1:ans3;
phi2:ans4;

```

| ![prt2](https://private-user-images.githubusercontent.com/120648145/240959822-cf48db59-8395-4cc1-99bf-c71dd46d6429.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MzYzLCJuYmYiOjE2ODUwMjgwNjMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTgyMi1jZjQ4ZGI1OS04Mzk1LTRjYzEtOTliZi1jNzFkZDQ2ZDY0MjkucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMTAzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MDk4NzFjY2YwNzU5NDQwMGZjMjdkOGVkMzRlMDhlZmYwN2JiNjA4NWY1ZjMzMjE5YjVhZjJkYjFjYTJjMTgxMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.rSRkI3hX0oUat91jlG50Qh7AEyvZvF670u3xFMfZidA) |
|:--:|
| *Visualization of **prt2*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `phi1`|
|TAns | `phistartr`| 
|Node 1 true feedback | `<p>Nice, you found the correct value for \(\phi_1\)! Good job!<p>`|
|Node 1 false feedback |`<p>The value you gave for \(\phi_1\) is not correct.  </p>`|

| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240959831-e21b87a0-d937-4158-94de-31732f771054.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MzYzLCJuYmYiOjE2ODUwMjgwNjMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTgzMS1lMjFiODdhMC1kOTM3LTQxNTgtOTRkZS0zMTczMmY3NzEwNTQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMTAzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9M2JkYzZkYWUzNWM3YThiN2Q3MzY3YmY3OTk5ZjBiN2FlMDdkODA2YzdmNTI5MDcxM2EwN2MyN2MzY2E3MTgyMSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.rex4bN8a8POIGxppeJ3RpK8cT7c3oiJWWTU-H2WW5FM) |
|:--:|
| *Values of **node 1*** |


### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `phi2`|
|TAns | `phistartr + phiranger`| 
|Node 2 true feedback | `<p>Nice, you found the correct value for \(\phi_2\)! Good job!</p> <p> Perfect! You got both values of \(\phi\) right! </p>`|
|Node 2 false feedback |`<p>The value you gave for \(\phi_2\) is not correct. Try matching the points perfectly and read the bigger angle.</p>`|

| ![Node 2](https://private-user-images.githubusercontent.com/120648145/240959810-b4fe9426-f1b4-4648-acf9-9f88958a604a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MzYzLCJuYmYiOjE2ODUwMjgwNjMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTgxMC1iNGZlOTQyNi1mMWI0LTQ2NDgtYWNmOS05Zjg4OTU4YTYwNGEucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMTAzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YjEwM2FjZWI5N2I4NDdhYTMxMGI1MDA0YjljMzY5YzUxMTU4NDI2MGQ0ZjVmZDZkMTU0Zjk3YTczYThlN2MyMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.ZoEQTM5tr6WbF29lfJluuAGwupn3dkfoynne1hgWXZ8) |
|:--:|
| *Values of **node 2*** |

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `phi2`|
|TAns | `phistartr + phiranger`| 
|Node 3 true feedback | `<p>Nice, you found the correct value for \(\phi_2\)! Good job!</p> <p>Check whether you did anything different here than for \(\phi_1\) and try again. </p>`|
|Node 3 false feedback |`<p>The value you gave for \(\phi_2\) is also not correct. Try matching the points perfectly and read the angles. The smaller angle is the lower bound of the interval. The larger angle is the upper bound of the interval.</p>`|

| ![Node 3](https://private-user-images.githubusercontent.com/120648145/240959816-b571d51f-fef9-498e-a155-270292a910f8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4MzYzLCJuYmYiOjE2ODUwMjgwNjMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk1OTgxNi1iNTcxZDUxZi1mZWY5LTQ5OGUtYTE1NS0yNzAyOTJhOTEwZjgucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMTAzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MDQ1OTdhZmRmNDEwODk1NGRjYmY0OTJiZTg5ZTBiODk3ZWIxMDRmOTVjODVkN2ZhZjVmNjllMmEzZTYwOWQ0MyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.Y_wYWjo6btNRxg3__WNYe-Nvv55Qmx0K6N57Zh9Soxs) |
|:--:|
| *Values of **node 3*** |

### prt3

Feedback variables:
```
psi1:ans5;
psi2:ans6;

```

| ![prt3](https://private-user-images.githubusercontent.com/120648145/240960377-ab3a7c38-2655-479a-ae73-d91839a45a53.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4NDc1LCJuYmYiOjE2ODUwMjgxNzUsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk2MDM3Ny1hYjNhN2MzOC0yNjU1LTQ3OWEtYWU3My1kOTE4MzlhNDVhNTMucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMjU1WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZGQ2YTcwY2E2NTU2N2E0YmEyNGExMTQwMmM0OGQ3OWVlOGNkZjdmM2ZlMmI4YmQwNmE5MjYwZmFiMzU4MDkxNCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.MVdSz6-PcApZe7NlXbWUKZb8MBXVnZ7RHBiJZ_pZGPE) |
|:--:|
| *Visualization of **prt3*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `psi1`|
|TAns | `psistartr`| 
|Node 1 true feedback | `<p>Nice, you found the correct value for \(\psi_1\)! Good job!<p>`|
|Node 1 false feedback |`<p>The value you gave for \(\psi_1\) is not correct.  </p>`|

| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240960369-60d14ff4-0d0e-4e96-9b06-afcb8817bf26.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4NDc1LCJuYmYiOjE2ODUwMjgxNzUsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk2MDM2OS02MGQxNGZmNC0wZDBlLTRlOTYtOWIwNi1hZmNiODgxN2JmMjYucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMjU1WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NmVjOTMxYWU2MTllOWY0YmQwYWI2MTUzYzg5OWQzNTZmZDA3ZGEzN2IwMTFhN2UyNWFjYTU2YzhiNWJkZDU0OSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.eUdhgiaDvpBAJ3HVEHe6TpOtZLdKsBnfDsdaHiXBLhc) |
|:--:|
| *Values of **node 1*** |

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `psi2`|
|TAns | `psistartr + psiranger`| 
|Node 2 true feedback | `<p>Nice, you found the correct value for \(\psi_2\)! Good job!</p> <p> Perfect! You got both values of \(\psi\) right! </p>`|
|Node 2 false feedback |`<p>The value you gave for \(\psi_2\) is not correct. Try matching the points perfectly and read the bigger angle. </p>`|

| ![Node 2](https://private-user-images.githubusercontent.com/120648145/240960374-0d861c5d-6e7d-453d-b45d-b3acf3812c7c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4NDc1LCJuYmYiOjE2ODUwMjgxNzUsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk2MDM3NC0wZDg2MWM1ZC02ZTdkLTQ1M2QtYjQ1ZC1iM2FjZjM4MTJjN2MucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMjU1WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MzYzNTgwYjdmNjZmODFiZDM3YTYxYjgwZDk2Nzk4NTc1OGYyZjlmZDZlODk0M2M5Y2ExN2QxZTgxYTJkYzMzOCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.YqbIBvFqQQUy38gqe-3PrilGb0QRn2pQMR20nPjB608) |
|:--:|
| *Values of **node 2*** |

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `psi2`|
|TAns | `psistartr + psiranger`| 
|Node 3 true feedback | `<p>Nice, you found the correct value for \(\psi_2\)! Good job!</p> <p>Check whether you did anything different here than for \(\psi_1\) and try again. </p>`|
|Node 3 false feedback |`<p>The value you gave for \(\psi_2\) is also not correct. Try matching the points perfectly and read the angles. The smaller angle is the lower bound of the interval. The larger angle is the upper bound of the interval.</p>`|

| ![Node 3](https://private-user-images.githubusercontent.com/120648145/240960376-8147f233-ccfe-47a3-9bcf-8cf5fd14ca9e.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDI4NDc1LCJuYmYiOjE2ODUwMjgxNzUsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDk2MDM3Ni04MTQ3ZjIzMy1jY2ZlLTQ3YTMtOWJjZi04Y2Y1ZmQxNGNhOWUucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMTUyMjU1WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NDE0MWFiMWNhZDI2NDVkMDZhZDJmMzcxZDI2ZmU4NzczMTAyY2FmNGQzNWUyMjI5ZWRkZjRkMTI5NTY4NDQyYSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.0PYPPu4hjK6f6r4MWW3NVn6erS7wlXbXjkFuf-xSz5E) |
|:--:|
| *Values of **node 3*** |

## Todo:

* [ ] Print JSXGraph applet bigger
* [x] make square appear as such
* [ ] Update Images
