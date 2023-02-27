---
title: Parametric Curve Matching circular
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows how a multidimensional curve is produced from varying a single parameter. (Handling mathematical symbols and formalism)
+	Student can find other parameters of the curve using a 3D visualization. (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://user-images.githubusercontent.com/120648145/213417666-1451a89a-2008-4e9f-84df-dc3dbe322f82.png) |
|:--:|
| *First impression of the question* |

## Question description

A 3D curve is plotted. It is a closed curve whose constant parameters are randomly selected upon starting the task. Its equation is
```math
t \mapsto \begin{pmatrix} r \cdot \cos(t) \\ r \cdot \sin(t) \\ a \cdot \cos(n \cdot t - \phi) \end{pmatrix}. 
```
A second curve given by the same equation is plotted that can be varied using sliders.
That way, by matching the two curves, the parameters can be interactively obtained.
The task is to find the correct values for $r$, $a$, $\phi$ and $n$ in real numbers or integer numbers.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

It is the task to reconstruct the parameters of the 3D curve. In order to do this they have to find out the radius, amplitude, phase shift and number of oscillations by matching a second curve to the given one using sliders. If they overlap exactly, the parameter values can be read from the sliders. The values have to be given in an exact algebraic manner.

| ![Click draw button](https://user-images.githubusercontent.com/120648145/213417659-8066e704-98db-44fb-876a-db9d76c60c68.png) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for parameters. In order to do this, they simply need to modify the entries in the lists specified e.g. change `phaser : rand([1/6, 1/4, 1/3, 1/2, 2/3, 3/4, 5/6 ,1]);` to `phaser : rand([1/6, 1/4, 1/3, 1/2]);`. 

Another example - in the case of the radius - is the following: change `radiusr:rand(6)/2` to `radiusr: rand(8)/2` in order to select numbers from 0 to 4 in steps of 1/2.

For an explanation of the processing of the values read **Question variables** and **Question text**.


| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/213417662-9af7a3b2-9482-4509-811c-4e1379039363.png) |
|:--:|
| *The above image shows which values the teacher may wish to change* |


## Question code

### Question Variables
+	`radiusr` and `ampr` are randomly selected integer numbers created using `rand()`, they are divided by 2 and 4 respectively to allow for non-integer steps
+ `phaser`is randomly selected from a list of possible values using `rand()`
+ `numr`is a randomly selected integer number created using `rand()`
+ The value of `phaser` is multiplied by pi and saved to `phase` as a numerical value. This is done in between `numer:true` and `numer:false`.
+ The value of `phaser` is multiplied by pi to use it for plotting in **Question text**.



#### Question variable code
```jacascript
/*randomize radius, amplitude, phase shift, number of oscillations*/

radiusr: 1+rand(6)/2;
ampr: 1/4+rand(10)/4; 
phaser : rand([1/6, 1/4, 1/3, 1/2, 2/3, 3/4, 5/6 ,1]);
numr: rand(5)+1;

/* prepare numerical values for JSXGraph */
numer:true
phase:phaser*%pi;
numer:false

/*symbolic data for checking*/
phaser: phaser*%pi
```

### Question Text
Reconstruct the blue 3D curve dependent on a parameter $t$.

In order to do so, you need to find the correct radius $r$, amplitude $a$, phase shift $\phi$ and number of oscillations $n$.

The curve is the trace of the function 
```math
t \mapsto \begin{pmatrix} r \cdot \cos(t) \\ r \cdot \sin(t) \\ a \cdot \cos(n \cdot t - \phi) \end{pmatrix}.
```

Use the sliders in the JSXGraph applet to your advantage and type in your reply right below it.
	
Note: Give your reply in the form of fractions e.g. $r$= `1/2`, $\phi$= `7*pi/4`. 

+ Task explanation using LaTex
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans1]]`, `[[input:ans2]]`, `[[input:ans3]]` and `[[input:ans4]]` at the end of JSXGraph code to allow input of  answers of the student for r, a and phi and n respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` , `[[validation:ans3]]` and `[[validation:ans4]]`  are used for checking of answer

#### Question text code


```javascript
<p>Reconstruct the blue 3D curve dependent on a parameter \(t\).</p>
<p>In order to do so, you need to find the correct radius \(r\), amplitude \(a\), phase shift \(\phi\) and number of oscillations \(n\).</p>
<p> The curve is the trace of the function \( t \mapsto \begin{pmatrix} r \cdot \cos(t) \\ r \cdot \sin(t) \\ a \cdot \cos(n \cdot t - \phi) \end{pmatrix} \). </p>
<p>Use the sliders in the JSXGraph applet to your advantage and type in your reply right below it.</p>
<p>Note: Give your reply in the form of fractions e.g. \(r\)= <code>1/2</code>, \(\phi\)= <code>7*pi/4</code>.</p>

[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

                        var view = board.create('view3d',
		                            [[-6, -3], [8, 8],
		                            [[-5, 5], [-5, 5], [-5, 5]]],
		                            {});
			
			//curve from STACK values
			var r = {#radiusr#};
			var a = {#ampr#};
			var p = {#phase#};
			var n = {#numr#};
			var c_base = view.create('curve3d', [
				(t) => r* Math.cos(t),
				(t) => r* Math.sin(t),
				(t) => a* Math.cos(n *t-p),
				[-Math.PI, Math.PI]], {strokeWidth: 1, strokeColor: "blue"});

			//slider-based curve 

			var rslide = board.create('slider', [[-7,-6], [3,-6], [0,5,10]], {name: "r"});
			var aslide = board.create('slider', [[-7,-7],[3,-7],[0,2,4]], {name: 'a'});
			var nslide = board.create('slider', [[-7,-9],[3,-9],[0,2,7]], {name: 'n', snapWidth:1});
			var sslide = board.create('slider', [[-7,-8],[3,-8],[0,2,Math.PI]], {name: 'phase shift'});
			var c = view.create('curve3d', [
				(t) => rslide.Value()* Math.cos(t),
				(t) => rslide.Value()* Math.sin(t),
				(t) => aslide.Value()*Math.cos(nslide.Value()*t- sslide.Value()),
				[-Math.PI, Math.PI]], {strokeWidth: 1, strokeColor: "red"});



[[/ jsxgraph]]
<p>\(r=\) [[input:ans1]] [[validation:ans1]]</p>
<p>\(a=\) [[input:ans2]] [[validation:ans2]]</p>
<p>\(\phi=\) [[input:ans3]] [[validation:ans3]]</p>
<p>\(n=\) [[input:ans4]] [[validation:ans4]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `radiusr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 2
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `ampr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `phaser` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 4
|property | setting| 
|:---|:---|
|Input type | Algebraic input|
|Model answer | `numr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
## Potential response tree
### prt1

Feedback variables:
```
radiusans: ans1
ampans: ans2
phaseans: ans3
numans: ans4
```

| ![prt1](https://user-images.githubusercontent.com/120648145/213417669-8735a0da-5074-4b7c-9870-8b287ab42be6.png) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `radiusans`|
|TAns | `radiusr`| 
|Node 1 true feedback | `<p> Nice! You found the correct radius \(r\). Good job!</p>`|
|Node 1 false feedback |`<p>The radius \(r\) is not yet correct. Check, whether the curves align, when you slide "r" to this value.</p>`|


| ![Node 1](https://user-images.githubusercontent.com/120648145/213417672-46371a41-85ae-428f-bd38-1865306c451b.png) |
|:--:|
| *Values of **node 1*** |

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `ampans`|
|TAns | `ampr`| 
|Node 2 true feedback | `<p>Nice! You found the correct amplitude a. Good job!</p>`|
|Node 2 false feedback |`<p>The amplitude a is not yet correct. Check, whether the curves align, when you slide "a" to this value.</p>`|

| ![Node 2](https://user-images.githubusercontent.com/120648145/213417645-2510084e-fcca-42a0-92cc-213e60dc6553.png) |
|:--:|
| *Values of **node 2*** |

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `phaseans`|
|TAns | `phaser`| 
|Node 3 true feedback | `<p>Nice! You found the correct phase shift \(\phi\). Good job!</p>`|
|Node 3 false feedback |`<p>The phase shift \(\phi\) is not yet correct. Check, whether the curves align, when you slide "phase shift" to this value.</p>`|

| ![Node 3](https://user-images.githubusercontent.com/120648145/213417653-ed158b79-5e19-4862-b9c8-e1270d617724.png) |
|:--:|
| *Values of **node 3*** |

### Node 4 
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `numans`|
|TAns | `numr`| 
|Node 4 true feedback | `<p>Nice! You found the correct number of oscillations \(n\). Good job!</p>`|
|Node 4 false feedback |`<p>The number of oscillations \(n\) is not yet correct. Check, whether the curves align, when you slide "n" to this value. Note, that you can count the maxima of the curve and try again.</p>`|

| ![Node 4](https://user-images.githubusercontent.com/120648145/213418525-b0eab465-30e9-4f61-b8a2-100190665751.png) |
|:--:|
| *Values of **node 4*** |





## Todo:
* [ ] check grading
* [ ] check why randomization does not work
