---
title: Example Function of two variables (stationary point)
usemathjax: true
theme: minima
---
## Aim of task
+ Student knows how to calculate partial derivatives and tangent planes  (Handling mathematical symbols and formalism)
+	Student knows the concept of stationary points in 2D and can calculate them  (Handling mathematical symbols and formalism)
+	Student understands, how stationary points and tangent planes are connected graphically  (Representing mathematical entities)
+ Using a visualization of planes tangent to a 2D function graph student can decide whether or not a point is stationary (Making use of aids and tools)

| ![First impression](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *First impression of the question* |

## Question description

A 2D function is plotted and its Taylor approximation of first order is given at a moveable point $x_0= (x_1,x_2)$. 
Since the Taylor approximation is given as 
$$f_1 (t) = f(x_0) + \nabla f(x_0) \cdot (x-x_0) $$
it describes the tangent plane to a given point $x_0$.

The task is to move $x_0$ where it is stationary with the help of the tangent plane. It is stationary where the slope in both $x_1$ and $x_2$ direction are zero.

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
+	3 lists of integer numbers for variables a1, a2, a3 to randomly select from
+	Selected number can be divided or multiplied with a number to    scale e.g.: `a1:rand([-10,-8,-6,-4,-2,2,4,6,8,10])/5;`
+	function F using ` a1`, `a2`, `a3` dependent on variables `x`, `y` as follows: 

    `F: a1 * cos(%pi*a2*x)*cos(a3*y);`  
    Note that this function’s parameters `a1`, `a2` and `a3` are randomized upon executing the code as mentioned above
+	derivatives of Function F using Maxima syntax e.g.: `Fdx: diff(F,x)` to calculate the components of the Hessian Matrix
+	numerical reference solution e.g.: `FdyRefSol:0
`

#### Question variable code
```jacascript
/* generate function */
a1:rand([-10,-8,-6,-4,-2,2,4,6,8,10])/5;
a2:rand([1,2,4,6,8,10])/5;
a3:rand([4,5,6,8,10])/5;

/* define the function */
F:a1 * cos(%pi*a2 * x )* cos( a3 * y);
Fdx:diff(F,x);
Fdy:diff(F,y);

/* generate reference solution*/
FdyRefSol:0;
FdxRefSol:1/a2;
```

### Question Text
+	“Find a stationary point on the surface”
+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the randomized function and displaying the	tangent plane for a point of freely adjustable x,y-coordinates
+	`[[input:ans1]]` at the end of JSXGraph code to allow input of an answer of the student
+	`[[validation:ans1]]` checking of answer

#### Question text code


```javascript
<p>Find a stationary point on the surface.</p>


[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : true});

	    var box = [-2, 2];
		    var view = board.create('view3d',
		        [
		            [-6, -3], [8, 8],
		            [box, box, box]
		        ],
		        {
		            xPlaneRear: {visible: false},
		            xPlaneRearYAxis: {visible: false},
		            xPlaneRearZAxis: {visible: false},
		            yPlaneRear: {visible: false},
		            yPlaneRearXAxis: {visible: false},
		            yPlaneRearZAxis: {visible: false},
		        });

                               var txtraw = '{#F#}';
                               txtraw=txtraw.replace(/%pi/g, "PI");
                               //txtraw=txtraw.replace(/pi/g, "PI");
                               var F =  board.jc.snippet(txtraw, true, 'x,y');
                               txtraw = '{#Fdx#}';
                               txtraw=txtraw.replace(/%/g, "");
                               txtraw=txtraw.replace(/pi/g, "PI");
                               var Fdx =  board.jc.snippet(txtraw, true, 'x,y');
                               var txtraw = '{#Fdy#}';
                               txtraw=txtraw.replace(/%/g, "");
                               txtraw=txtraw.replace(/pi/g, "PI");
                               var Fdy =  board.jc.snippet(txtraw, true, 'x,y');
    var c = view.create('functiongraph3d', [
        F,
        box,
        box,
    ], { strokeWidth: 0.5, stepU: 70, stepsV: 70 });

  // 3D points:
    // Point on xy plane
    var Axy = view.create('point3d', [1, 1, -2], { withLabel: false });

    // Project Axy to the surface
    var A = view.create('point3d', [
        () => [Axy.X(), Axy.Y(), F(Axy.X(), Axy.Y())]
        ], { withLabel: false });
    view.create('line3d', [Axy, A], { dash: 1 });
    // Partial derivatives of F in point A
    // should be provided form STACK
    var dFx = () => Fdx(A.X(),A.Y()),
        dFy = () => Fdy(A.X(),A.Y());
    var dFx_vecnorm = () => Math.sqrt(1+Fdx(A.X(),A.Y())**2),
        dFy_vecnorm = () => Math.sqrt(1+Fdy(A.X(),A.Y())**2);

    // var dFx1 = () => 1.0/Math.sqrt(1+Fdx(A.X(),A.Y())**2),
     var dFx1 = () => 1.0/dFx_vecnorm(),
        dFx2 = () => Fdx(A.X(),A.Y())/Math.sqrt(1+Fdx(A.X(),A.Y())**2);
    var dFy1 = () => 1.0/Math.sqrt(1+Fdy(A.X(),A.Y())**2),
        dFy2 = () => Fdy(A.X(),A.Y())/Math.sqrt(1+Fdy(A.X(),A.Y())**2);

    var dFx_vec = [dFx1, 0, dFx2],
        dFy_vec = [0, dFy1, dFy2];

    // Tangent plane
    var plane1 = view.create('plane3d', [
        A,
        dFx_vec, dFy_vec,
        [-0.5,0.5], [-0.5,0.5]
    ], {
        fillOpacity: 0.8, fillColor: 'red'
    });
    var a = view.create('line3d', [A, dFx_vec, [0, 1]]);
    var b = view.create('line3d', [A, dFy_vec, [0, 1]]);

board.update(); 

var p1 =board.create('point', [function () {return A.X();} ,function () {return A.Y();}],{visible:false}); 
stack_jxg.bind_point(ans1Ref,p1);

board.update(); 

[[/jsxgraph]]
<p>[[input:ans1]] </p><p>[[validation:ans1]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Numerical |
|Model answer | `[FdxRefSol, FdyRefSol]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
--- 
## Potential response tree
### prt1

Feedback variables:
```
FdxSAns:ev(Fdx,numer,x=ans1[1],y=ans1[2]);
FdySAns:ev(Fdy,numer,x=ans1[1],y=ans1[2]);
```
 Creates variables `FdxSAns`, `FdySAns`. Their values are determined by the function `ev()` evaluating the derivatives `Fdx`, `Fdy` specified in **Question variables** numerically at the location specified by `ans1`.


| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | FdxSAns|
|TAns | 0| 
|Node 1 true feedback | In \\(x\\)-direction the slope is close to zero.|
|Node 1 false feedback | In \\(x\\)-direction the slope is not close to zero enough.|
### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | FdySAns|
|TAns | 0| 
|Node 2 true feedback | In \\(y\\)-direction the slope is close to zero.|
|Node 2 false feedback | In \\(y\\)-direction the slope is not close to zero enough.|

## Todo:
* [ ] Elaborate more on task for students
* [ ] Display definition of stationary point in solution
* [ ] JSXGraph-Applet does not work in solution

