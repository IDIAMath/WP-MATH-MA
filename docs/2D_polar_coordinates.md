---
title: Example Polar Coordinates
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows the transformation from cartesian to polar coordinates  (Handling mathematical symbols and formalism)
+	Student can think of an area that is transformed to the given area in polar coordinates and check graphically (represent mathematical entities, posing and solving mathematical problems, making use of aids and tools )

| ![First impression](https://user-images.githubusercontent.com/120648145/209998497-b80aeef2-fcc8-41cb-a717-89c361abd805.PNG) |
|:--:|
| *First impression of the question* |

## Question description

A 2D figure is plotted. It is a randomly generated section of a sphere in polar coordinates.

The task is to find the correct intervalls for $r$ and $\phi$ in real numbers that construct the generated figure in polar coordinates.


### Student perspective

[describe what the student will see]

| ![Click draw button](https://user-images.githubusercontent.com/120648145/209998506-2108d80f-d943-4fc1-b863-3698215d32a0.PNG) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
[describe what the teacher needs to do and can do]

| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/209998491-d053aeba-cb1a-408a-98b2-a08263bf6196.PNG) |
|:--:|
| *The above image shows which values the teacher may wish to change* |

### Questions and answers examples

[insert examples]

## Question code

### Question Variables
+	`ranger` and `startr` take random values of a list containing possible values for phi (needs to be multiplied by pi later)
+	`radius1` and `radius2` are randomly selected in steps of 1/2 and `radius2` is always bigger than `radius1`  
+	`p1x`, `p1y`, `p2x`, `p2y`, `p3x`, `p3y`, `p4x`, `p4y` are defined as numerical value using polar coordinate transformation and `radius1`, `radius2`, `startr` and `ranger`
+ the variables `p1x`,…,`p4y` form a rectangle that is constructed in the code of **Question text** which is the correct solution of the task



#### Question variable code
```jacascript
ranger:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);
startr:rand([1/6,1/4,1/3,1/2,2/3,3/4,5/6,1]);
/*radius*/
radius1: rand(6)/2;
radius2: radius1+(rand(6)+1)/2;
/* preper JSXGraph values */
numer:true;
p1x:radius1*cos(startr*%pi);
p1y:radius1*sin(startr*%pi);
p2x:radius2*cos(startr*%pi);
p2y:radius2*sin(startr*%pi);
p3x:radius2*cos((startr+ranger)*%pi)
p3y:radius2*sin((startr+ranger)*%pi)
p4x:radius1*cos((startr+ranger)*%pi)
p4y:radius1*sin((startr+ranger)*%pi)

numer:false;
```

### Question Text
+	Give the limits for a 2d integration for the area shown in the diagram in polar coordinates $(r,\phi)$. 
Write the interval in the form $r\in$[r1,r2] and $\phi\in$[phi1,phi2]., e.g. [1/2,2] and [1/2* pi,2*pi]”

+ Task explanation using LaTex
+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the randomized points in polar coordinates
+	`[[input:ans1]]` , `[[input:ans2]]` at the end of JSXGraph code to allow input of an answer of the student for both the radius intervalls and the angle intervall respectively
+	`[[validation:ans1]]`,  `[[validation:ans2]]` checking of answer

#### Question text code


```javascript
<p>Give the limits for a 2d integration for the area shown in the diagram in polar coordinates \((r,\phi)\). </p>
<p> Write the interval in the form \(r\in\)<code>[r1,r2]</code> and  \(\phi\in\)<code>[phi1,phi2].</code>, e.g. <code>[1/2,2]</code> and <code>[1/2*pi,2*pi]</code></p>

[[ jsxgraph width="250px" height="250px"]] [[/ jsxgraph ]]
[[ jsxgraph width="250px" height="250px"]] [[/ jsxgraph ]]

[[jsxgraph width='0px' height='0px' input-ref-ans1='ans1Ref']]

//handling divids
var divid3 = divid;
console.log(divid3);
var parts = divid.split('-');
console.log(parts);

parts[2] = parts[2] -1;
var divid2 = parts.join('-');
console.log(divid2);

parts[2] = parts[2] -1;
var divid1 = parts.join('-');
console.log(divid1);

//content
var board = JXG.JSXGraph.initBoard(divid1,{boundingbox : [-5, 5, 5,-5], axis:true, shownavigation : false});

var center =board.create("point",[0,0],{name : "",visible:false,fixed:true});
var p1 = board.create("point",[{#p1x#},{#p1y#}],{name : "P1",visible:false,fixed:true,});
var p2 = board.create("point",[{#p2x#},{#p2y#}],{name : "P2",visible:false,fixed:true});
var p3 = board.create("point",[{#p3x#},{#p3y#}],{name : "P3",visible:false,fixed:true});
var p4 = board.create("point",[{#p4x#},{#p4y#}],{name : "P4",visible:false,fixed:true});
var c1 = board.create("arc",[center,p1,p4],{frozen:true});
var c2 = board.create("line",[p4,p3],{frozen:true, straightFirst:false, straightLast:false});
var c3 = board.create("arc",[center,p2,p3],{frozen:true});
var c4 = board.create("line",[p2,p1],{frozen:true, straightFirst:false, straightLast:false});
//stack_jxg.bind_point(ans1Ref,p1);


var board2 = JXG.JSXGraph.initBoard(divid2,{boundingbox : [-1, 5, 5,-0.5], axis:true, 
  defaultAxes: {
    	y: {
      	ticks: {
        	scale: Math.PI,
          scaleSymbol: '\u03c0',
          ticksDistance: 0.5,
          beautifulScientificTickLabels:true,
          insertTicks: false
        }}}, 
      shownavigation : false});
  board2.addChild(board);
  board.suspendUpdate();
  board2.suspendUpdate();

// var center2 =board2.create("point",[0,0],{name : "",visible:false,fixed:true});
var p12 = board2.create("point",[0.5,1.57],{name : "P1",visible:true});
var p32 = board2.create("point",[2.5,3.14],{name : "P2",visible:true});

var p22 = board2.create("point",[function () {return p32.X()},function () {return p12.Y()}],{name : "P3",visible:false});
var p42 = board2.create("point",[function () {return p12.X()},function () {return p32.Y()}],{name : "P4",visible:false});
var polyg1 = board2.create("polygon",[p12,p22,p32,p42],{name : ""});

//stack_jxg.bind_point(ans1Ref,p1);

var p1p = board.create("point",[function () {return p12.X()*Math.cos(p12.Y());},
                            function () {return p12.X()*Math.sin(p12.Y());}],
                            {name : "P1",visible:false});
var p2p = board.create("point",[function () {return p32.X()*Math.cos(p12.Y());},
                            function () {return p32.X()*Math.sin(p12.Y());}],
                            {name : "P2",visible:false});
var p3p = board.create("point",[function () {return p32.X()*Math.cos(p32.Y());},
                            function () {return p32.X()*Math.sin(p32.Y());}],
                            {name : "P3",visible:false});
var p4p = board.create("point",[function () {return p12.X()*Math.cos(p32.Y());},
                            function () {return p12.X()*Math.sin(p32.Y());}],
                            {name : "P4",visible:false});
var c1p = board.create("arc",[center,p1p,p4p],{frozen:true,strokeColor:'red'});
var c2p = board.create("line",[p4p,p3p],{frozen:true,strokeColor:'red', straightFirst:false, straightLast:false});
var c3p = board.create("arc",[center,p2p,p3p],{frozen:true,strokeColor:'red'});
var c4p = board.create("line",[p2p,p1p],{frozen:true,strokeColor:'red', straightFirst:false, straightLast:false});

board.unsuspendUpdate();
board2.unsuspendUpdate();

[[/ jsxgraph]]

<p>\(r\in\) [[input:ans1]] [[validation:ans1]]</p>
<p>\(\phi\in\) [[input:ans2]] [[validation:ans2]]</p>
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
|Model answer | `[startr*%pi, (startr+ranger)*%pi]` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---

## Potential response tree
### prt1

| ![prt1](https://user-images.githubusercontent.com/120648145/209998503-d17d43ca-be5f-4e6e-820d-01946ba26950.PNG) |
|:--:|
| *Display of **prt1*** |

Feedback variables:
```
r1:ans1[1]
r2:ans1[2]
phi1:ans2[1]/%pi
phi2:ans2[2]/%pi

int1low:ans1[1]
```

| ![Node 1](https://user-images.githubusercontent.com/120648145/209998500-913eb222-72fc-4ffd-9451-d1519cfa673c.PNG) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | Algequiv|
|SAns | r1|
|TAns | radius1| 
|Node 1 true feedback |Nice, you found the correct value for \(r_1\)! Good job! |
|Node 1 false feedback |The value you gave for \(r_1\) is not correct. Try matching the points perfectly and read the smaller radius. This is the lower bound of the interval of possible radiuses. Make sure, you're giving the values in the format specified in the task explanation.|

### Node 2
 |property | setting| 
|:---|:---|
|Answer Test | Algequiv|
|SAns | r2|
|TAns | radius2| 
|Node 2 true feedback |Nice, you found the correct value for \(r_2\)! Good job!|
|Node 2 false feedback |The value you gave for \(r_2\) is not correct. Try matching the points perfectly and read the bigger radius. This is the upper bound of the interval of possible radiuses. Make sure, you're giving the values in the format specified in the task explanation.|

### Node 3
 |property | setting| 
|:---|:---|
|Answer Test | Algequiv|
|SAns | phi1|
|TAns | startr| 
|Node 3 true feedback |Nice, you found the correct value for \(\phi_1\)! Good job!|
|Node 3 false feedback |The value you gave for \(\phi_1\) is not correct. Try matching the points perfectly and read the smaller angle. This is the lower bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation|

### Node 4
 |property | setting| 
|:---|:---|
|Answer Test | Algequiv|
|SAns | phi1|
|TAns | startr| 
|Node 4 true feedback |Nice, you found the correct value for \(\phi_2\)! Good job! Now that you know how to transform points from cartesian to polar coordinates graphically, you can have a look at the quantitative transformation from one system in the other. If you know this, it will be way easier to parametrize functions or solve problems with rotational symmetry. You can then use, what you used in this exercise to find suiting integration bounds and perform calculations you could not easily do with cartesian coordinates.|
|Node 4 false feedback |The value you gave for \(\phi_2\) is not correct. Try matching the points perfectly and read the bigger angle. This is the upper bound of the interval of possible angles. Make sure, you're giving the values in the format specified in the task explanation. If you try again and know how to transform points from cartesian to polar coordinates graphically, you can have a look at the quantitative transformation from one system in the other. If you know this, it will be way easier to parametrize functions or solve problems with rotational symmetry. You can then use, what you used in this exercise to find suiting integration bounds and perform calculations you could not easily do with  cartesian coordinates.|

## Todo:
* [ ] make sure variable names and code are consistent with other tasks

