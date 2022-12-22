---
title: Example function of two variables (Hessian)
usemathjax: true
theme: minima
---
## Aim of task
+ Student knows how to calculate partial derivatives and Hessian matrix (Handling mathematical symbols and formalism)
+	Student understands how the Hessian matrix is used in Taylor approximation to locally approximate functions (Communicating in, with, and about mathematics)
+	Student understands, how local approximation and value of Hessian matrix are connected graphically (Representing mathematical entities)
+	Using a visualization of Taylor-approximation student can derive qualitative statements about Hessian matrix at a given point (Making use of aids and tools)

| ![First impression](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *First impression of the question* |

## Question description

A 2D function is plotted and its Taylor approximation of second order is given at a moveable point $(x,y)$. 
Since the Taylor approximation is given as 
$$f_2 (t) = f(x_0) + \nabla f(x_0) \cdot (x-x_0) + \frac{1}{2} (x-x_0)^\text{T} H_f(x-x_0)$$
the character of the Taylor approximation gives information about the hessian of the function.

**NOT YET IMPLEMENTED:** Some desired properties of the hessian matrix will be given. The student then chooses a point $(x,y)$ where $f$ fulfills the conditions.

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
+	Selected number can be divided or multiplied with a number to    scale e.g.: a1:rand([-10,-8,-6,-4,-2,2,4,6,8,10])/5;
+	function F using ` a1, a2, a3` dependent on variables `x, y` as follows: 

    `F: a1 * cos(%pi*a2*x)*cos(a3*y);`  
    Note that this function’s parameters `a1, a2` and `a3` are randomized upon executing the code as mentioned above
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
Fdxx:diff(Fdx,x);
Fdxy:diff(Fdy,x);
Fdyy:diff(Fdy,y);

/* generate reference solution*/
FdyRefSol:0;
FdxRefSol:1/a2;
```

### Question Text
+	“Find a point with certain properties of the Hessian at this point”
+	JSXGraph applet using the functions and variables defined in Question variables plotting the randomized function and displaying the Taylor-Approximation in a point of freely adjustable x,y-coordinates
+	`[[input:ans1]]` at the end of JSXGraph code to allow input of an answer of the student
+	`[[validation:ans1]]` checking of answer




```javascript
<p>Find a point with certain properties of the Hessian at this point.</p>
<p><strong>No PRT implemented yet!</strong></p>


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

   // entries of quadratic form given from outside
   var a1g = 0;
   var a2g = 0.5;
   var a3g = 0;

   var a1 = board.create('slider', [[-7, -6], [5, -6], [-2, 1, 2]], { name: 'a_{11}' });
   var a2 = board.create('slider', [[-7, -7], [5, -7], [-2, 1, 2]], { name: 'a_{12}' });
   var a3 = board.create('slider', [[-7, -8], [5, -8], [-2, 1, 2]], { name: 'a_{13}' });

   // Function Fgiven to be plotted
   var F = (x, y) => a1.Value() * Math.cos(Math.PI*a2.Value() * x )* Math.cos( a3.Value() * y);
   var Fdx = (x, y) => -Math.PI*a2.Value() *a1.Value() * Math.sin(Math.PI*a2.Value() * x )* Math.cos( a3.Value() * y);
   var Fdy = (x, y) => -a3.Value() *a1.Value() * Math.cos(Math.PI*a2.Value() * x )* Math.sin( a3.Value() * y);
   var Fdxx = (x, y) => -Math.pow((Math.PI*a2.Value()),2)*a1.Value()  * Math.cos(Math.PI*a2.Value() * x )* Math.cos( a3.Value() * y);
   var Fdxy = (x, y) => Math.PI*a2.Value()*a3.Value() *a1.Value() * Math.sin(Math.PI*a2.Value() * x )* Math.sin( a3.Value() * y);
   var Fdyy = (x, y) => -a3.Value() *a3.Value() *a1.Value() * Math.cos(Math.PI*a2.Value() * x )* Math.cos( a3.Value() * y);
   // 3D surface

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
   view.create('line3d', [Axy, A], { dash: 1 })


   var TF = (x,y) => F(A.X(),A.Y())+Fdx(A.X(),A.Y())*(x-A.X())
                                         +Fdy(A.X(),A.Y())*(y-A.Y())
                                         +Fdxx(A.X(),A.Y())*(x-A.X())*(x-A.X())
                                         +Fdyy(A.X(),A.Y())*(y-A.Y())*(y-A.Y())
                                         +2*Fdxy(A.X(),A.Y())*(y-A.Y())*(x-A.X());
   var c2 = view.create('functiongraph3d', [
       TF,
       () => [A.X()-0.5,A.X()+0.5],
       () => [A.Y()-0.5,A.Y()+0.5,],
   ], { strokeWidth: 0.25, stepU: 50, stepsV: 50, strokeColor:'red' });



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
   /*
   var plane1 = view.create('plane3d', [
       A,
       dFx_vec, dFy_vec,
       [-0.5,0.5], [-0.5,0.5]
   ], {
       fillOpacity: 0.8, fillColor: 'red'
   });
   */
   var a = view.create('line3d', [A, dFx_vec, [0, 1]]);
   var b = view.create('line3d', [A, dFy_vec, [0, 1]]);

var p1 =board.create('point', [function () {return A.X();} ,function () {return A.Y();}],{visible:false}); 
stack_jxg.bind_point(ans1Ref,p1);

board.update(); 

[[/jsxgraph]]
<p>[[input:ans1]] </p><p>[[validation:ans1]]</p>
```
## Answers
### Answer ans 1
---
|type | numerical |
|reference solution | [FdxRefSol, FdyRefSol] defined in Question variables |
--- 
## Feedback variables
We retrieve the student answer and store it in variables. 
```rust
[insert feedback variables]
```
## Partial response tree
| ![Node 1](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *Values of **node 1*** |
### Node 1
