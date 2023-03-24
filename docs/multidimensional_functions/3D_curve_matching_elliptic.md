---
title: Parametric Curve Matching elliptic
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows how a multidimensional curve is produced from varying a single parameter. (Handling mathematical symbols and formalism)
+	Student can find other parameters of the curve using a 3D visualization. (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools  )

| ![First impression](https://user-images.githubusercontent.com/120648145/213679634-c35d8096-4c3f-4fbe-b2be-8cb6d441ea87.png) |
|:--:|
| *First impression of the question* |

## Question description


A 3D curve is plotted. It is a closed curve whose constant parameters are randomly selected upon starting the task. Its equation is
```math 
t \mapsto \begin{pmatrix} x_0+ a \cdot \cos(t) \cdot \cos(\alpha) - b \cdot \sin(t) \cdot \sin(\alpha) \\ y_0+ a \cdot \cos(t) \cdot \sin(\alpha) + b \cdot \sin(t) \cdot \cos(\alpha) \\h \cdot \cos(t)\end{pmatrix}.
```
A second curve given by the same equation is plotted that can be varied using sliders.
That way, by matching the two curves, the parameters can be interactively obtained.
The task is to find the correct values for $r$, $a$, $\phi$ and $n$ in real numbers or integer numbers.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

It is the task to reconstruct the parameters of the 3D curve. In order to do this they have to find out the radius, amplitude, phase shift and number of oscillations by matching a second curve to the given one using sliders. If they overlap exactly, the parameter values can be read from the sliders. The values have to be given in an exact algebraic manner.

| ![Click draw button](https://user-images.githubusercontent.com/120648145/213679631-30d42545-5805-4ed7-8ec7-5ab5812c95ef.png) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for parameters. In order to do this, they simply need to modify the entries in the lists specified e.g. change `alphar : rand([1/6, 1/4, 1/3, 1/2, 2/3, 3/4, 5/6 ,1]);` to `alphar : rand([1/6, 1/4, 1/3, 1/2]);`. 

Another example - in the case of the semiaxis - is the following: change `ar: 1+rand(6)/2` to `ar: 1+ rand(8)/2` in order to select numbers from 1 to 4.5 in steps of 1/2.

For an explanation of the processing of the values read **Question variables** and **Question text**.


| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/213679633-b475a068-2a0f-4882-9bd0-001c98901157.png) |
|:--:|
| *The above image shows which values the teacher may wish to change* |


## Question code

### Question Variables
+	`ar`, `br` ,`xr`, `yr` and `ampr` are randomly selected integer numbers created using `rand()`, they are divided by 2 and 4 respectively to allow for non-integer steps
+ `alphar`is randomly selected from a list of possible values using `rand()`
+ The value of `alphar` is multiplied by pi and saved to `alpha` as a numerical value. This is done in between `numer:true` and `numer:false`.
+ The value of `alphar` is multiplied by pi to use it for plotting in **Question text**.



#### Question variable code
```jacascript
/*randomize parameters*/

xr:  1+rand(6)/2;
yr:  1+rand(6)/2;
ar: 1+rand(6)/2;
br: 1+rand(6)/2;
ampr: 1/4+rand(10)/4; 
alphar : rand([1/6, 1/4, 1/3, 1/2, 2/3, 3/4, 5/6 ,1]);


/* prepare numerical values for JSXGraph */
numer:true
alpha: alphar*%pi;
numer:false

/*symbolic data for checking*/
alphar: alphar*%pi
```

### Question Text
Reconstruct the blue 3D curve dependent on a parameter $t$.

In order to do so, you need to find the correct offsets $x_0$ and $y_0$, semi-axis  $a$ and $b$, angle of rotation $\alpha$ and amplitude $h$.

The curve is the trace of the function 
```math
t \mapsto \begin{pmatrix} x_0+ a \cdot \cos(t) \cdot \cos(\alpha) - b \cdot \sin(t) \cdot \sin(\alpha) \\ y_0+ a \cdot \cos(t) \cdot \sin(\alpha) + b \cdot \sin(t) \cdot \cos(\alpha) \\h \cdot \cos(t)\end{pmatrix}.
```

Use the sliders in the JSXGraph applet or type in your reply right below it.
	


+ Task explanation using LaTex
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans1]]`, `[[input:ans2]]`, `[[input:ans3]]`, `[[input:ans4]]`, `[[input:ans5]]` and `[[input:ans6]]` at the end of JSXGraph code to allow input of  answers of the student for r, a and phi and n respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` , `[[validation:ans3]]`, `[[validation:ans4]]`, `[[validation:ans5]]`and `[[validation:ans6]]`  are used for checking of answer

#### Question text code


```javascript
<p>Reconstruct the blue 3D curve dependent on a parameter \(t\).</p>
<p>In order to do so, you need to find the correct offsets \(x_0\) and \(y_0\), semi-axis  \(a\) and \(b\), angle of rotation \(\alpha\) and amplitude \(h\).</p>
<p> The curve is the trace of the function \[ t \mapsto \begin{pmatrix} 
x_0+ a \cdot \cos(t) \cdot \cos(\alpha) - b \cdot \sin(t) \cdot \sin(\alpha) \\
y_0+ a \cdot \cos(t) \cdot \sin(\alpha) + b \cdot \sin(t) \cdot \cos(\alpha) \\
h \cdot \cos(t)
\end{pmatrix}.\] </p>
<p>Use the sliders in the JSXGraph applet or type in your reply right below it.</p>

[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref' input-ref-ans2='ans2Ref' input-ref-ans3='ans3Ref' input-ref-ans4='ans4Ref' input-ref-ans5='ans5Ref' input-ref-ans6='ans6Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

                             var view = board.create('view3d',
		                            [[-6, -3], [8, 8],
		                            [[-5, 5], [-5, 5], [-5, 5]]],
		                            {});

			//curve from STACK values
			var xrad = {#ar#};
			var yrad = {#br#};
			var ang = {#alpha#};
			var xoff = {#xr#};
			var yoff = {#yr#};
                        var amp = {#ampr#};
			var c_base = view.create('curve3d', [
				(t) => xoff + xrad* Math.cos(t)* Math.cos(ang) - yrad* Math.sin(t)* Math.sin(ang),
				(t) => yoff + xrad* Math.cos(t)* Math.sin(ang) + yrad* Math.sin(t)* Math.cos(ang),
				(t) => amp* Math.cos(t),
				[-Math.PI,Math.PI ]], {strokeWidth: 1, strokeColor: "blue"});
			
		
				
			//slider-based curve 
			
			var a = board.create('slider', [[-7,-7], [-3,-7], [0,1,10]], {name: "a",snapwidth:0.1, highline: {strokeColor: 'red'}, baseline: {strokeColor: 'red'}});
			var b = board.create('slider', [[-1,-7], [3,-7], [0,3,10]], {name: "b",snapwidth:0.1, highline: {strokeColor: 'red'}, baseline: {strokeColor: 'red'}});
			var y = board.create('slider', [[-1,-6],[3,-6],[-3,2,7]], {name: 'y0',snapwidth:0.1, highline: {strokeColor: 'red'}, baseline: {strokeColor: 'red'}});
			var xsl = board.create('slider', [[-7,-6],[-3,-6],[-3,2,7]], {name: 'x0',snapwidth:0.1, highline: {strokeColor: 'red'}, baseline: {strokeColor: 'red'}});
			var angle = board.create('slider', [[-7,-8], [3,-8], [0,1, Math.PI]], {name:"alpha", snapwidth:0.05, highline: {strokeColor: 'red'}, baseline: {strokeColor: 'red'}});
			var h = board.create("slider", [[-7,-9], [3,-9], [0,2,5]], {name: "h", snapwidth:0.05, highline: {strokeColor: 'red'}, baseline: {strokeColor: 'red'}});
			stack_jxg.bind_slider(ans1Ref,xsl);
			stack_jxg.bind_slider(ans2Ref,y);
			stack_jxg.bind_slider(ans3Ref,a);
			stack_jxg.bind_slider(ans4Ref,b);
			stack_jxg.bind_slider(ans5Ref,angle);
			stack_jxg.bind_slider(ans6Ref,h);

			var c = view.create('curve3d', [
				(t) => xsl.Value() + a.Value()* Math.cos(t)* Math.cos(angle.Value()) - b.Value()* Math.sin(t)* Math.sin(angle.Value()),
				(t) => y.Value() + a.Value()* Math.cos(t)* Math.sin(angle.Value()) + b.Value()* Math.sin(t)* Math.cos(angle.Value()),
				(t) => h.Value()*Math.cos(t),
				[-Math.PI, Math.PI]], {strokeWidth: 1, strokeColor: "red"}); 
board.update();
[[/ jsxgraph]]
<p>\(x_0=\) [[input:ans1]] [[validation:ans1]]</p>
<p>\(y_0=\) [[input:ans2]] [[validation:ans2]]</p>
<p>\(a=\) [[input:ans3]] [[validation:ans3]]</p>
<p>\(b=\) [[input:ans4]] [[validation:ans4]]</p>
<p>\(\alpha=\) [[input:ans5]] [[validation:ans5]]</p>
<p>\(h=\) [[input:ans6]] [[validation:ans6]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `xr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 2
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `yr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `ar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 4
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `br` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 5
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `alphar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 6
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `ampr` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
## Potential response tree
### prt1

Feedback variables:
```
xans: ans1
yans: ans2
aans: ans3
bans: ans4
alphaans: ans5
ampans: ans6
```

| ![prt1](https://user-images.githubusercontent.com/120648145/213679636-4e177792-32eb-47ca-8676-590ea2662fd9.png) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `xans`|
|TAns | `xr`| 
|Node 1 true feedback | `<p> Nice! You found the correct offset \(x_0\). Good job!</p>`|
|Node 1 false feedback |`<p>The offset \(x_0\) is not yet correct. Check, whether the curves' centres are aligned, when you slide "x0" to this value.</p>`|


| ![Node 1](https://user-images.githubusercontent.com/120648145/213679611-61f88456-34bd-4cea-a60e-b7582a5b6bd7.png) |
|:--:|
| *Values of **node 1*** |

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `yans`|
|TAns | `yr`| 
|Node 2 true feedback | `<p> Nice! You found the correct offset \(y_0\). Good job!</p>`|
|Node 2 false feedback |`<p>The offset \(y_0\) is not yet correct. Check, whether the curves' centres are aligned, when you slide "y0" to this value.</p>`|

| ![Node 2](https://user-images.githubusercontent.com/120648145/213679618-09d2226a-d3ae-4b24-bc59-566872be36d3.png) |
|:--:|
| *Values of **node 2*** |

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `aans`|
|TAns | `ar`| 
|Node 3 true feedback | `<p> Nice! You found the correct semi-axis length  \(a\). Good job!</p>`|
|Node 3 false feedback |`<p>The semi-axis length  \(a\) is not yet correct. Check, whether the curves have the same shape from above, when you slide "a" to this value.</p>`|

| ![Node 3](https://user-images.githubusercontent.com/120648145/213679623-fa1d75d9-647e-4e85-9635-59744217ef3e.png) |
|:--:|
| *Values of **node 3*** |

### Node 4 
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `bans`|
|TAns | `br`| 
|Node 4 true feedback | `<p> Nice! You found the correct semi-axis length  \(b\). Good job!</p>`|
|Node 4 false feedback |`<p>The semi-axis length  \(b\) is not yet correct. Check, whether the curves have the same shape from above, when you slide "b" to this value.</p>`|

| ![Node 4](https://user-images.githubusercontent.com/120648145/213679626-94525833-4578-4b69-ac35-1d5f090abefd.png) |
|:--:|
| *Values of **node 4*** |

### Node 5 
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `alphaans`|
|TAns | `alphar`| 
|Node 5 true feedback | `<p> Nice! You found the correct angle \(\alpha\). Good job!</p>`|
|Node 5 false feedback |`<p>The angle \(\alpha\) is not yet correct. Check, whether the curves are oriented the same way, when you slide "alpha" to this value.</p>`|

| ![Node 5](https://user-images.githubusercontent.com/120648145/213679627-77266e47-e2a1-4f0f-918c-15c72e858ede.png) |
|:--:|
| *Values of **node 5*** |

### Node 6 
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `ampans`|
|TAns | `ampr`| 
|Node 6 true feedback | `<p> Nice! You found the correct amplitude \(h\). Good job!</p>`|
|Node 6 false feedback |`<p>The amplitude \(h\) is not yet correct. Check, whether the curves have the same height in \(z\)-direction, when you slide "h" to this value.</p>`|

| ![Node 6](https://user-images.githubusercontent.com/120648145/213679629-32540240-5e26-4e4c-a185-5f57dea69adf.png) |
|:--:|
| *Values of **node 6*** |



## Todo:
* [ ] check grading
* [x] fix randomizing
* [ ] change PRT 
* [ ] update Aims of Task
