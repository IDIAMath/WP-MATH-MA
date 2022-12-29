---
title: Example Vectorfield (curl)
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows how to calculate partial derivatives, vector products and curls of 3D vector fields  (Handling mathematical symbols and formalism)
+	Student understands, how a vector field and its curl are connected graphically (Representing mathematical entities)
+ 	Using a visualization of vector field and its curl the student can graphically check whether his calculations are correct (Making use of aids and tools)

| ![First impression](https://user-images.githubusercontent.com/120648145/209999022-cebb6337-8522-40a4-bcc6-429757301ddc.PNG) |
|:--:|
| *First impression of the question* |

## Question description

A 3D vector field is plotted. 
3 different options for its curl are presented and the student needs to pick what they believe to be correct.

### Student perspective

[describe what the student will see]

| ![Click draw button](https://cdn.pixabay.com/photo/2013/07/12/17/47/test-pattern-152459_960_720.png) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
[describe what the teacher needs to do and can do]

| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/209999017-c79b6da8-0685-4cdc-b808-9efee6b2ea99.PNG) |
|:--:|
| *The above image shows which values the teacher may wish to change* |

### Questions and answers examples

[insert examples]

## Question code

### Question Variables
+	Vlist is a list of 3D vector fields dependent on x,y,z and constants given in format [f_x,f_y,f_z]  to randomly select from
+	Select one of the vector fields by randomizing the index Vindex of the list and evaluating Vlist via Vselected: Vlist[Vindex]
+	Define Variables Vx, Vy, Vz as the vector field components in order to plot it in Question text
+	Save the curls of all of the vector fields with attribute false to a list in order to access it in Question text
+	Set attribute of curl of selected vector field to true in order to be able to check answer


#### Question variable code
```jacascript
/* define the list of vector fields */
Vlist:[[z,x,y],[y,-x,0],[x,y,z]];

/* select one of the vector fields */
lv:length(Vlist);
Vindex:rand(lv)+1;
Vselected:Vlist[Vindex];

/* compute the curl of all vector fields in the list */
Vcurlop(Vinp):=[diff(Vinp[3],y)-diff(Vinp[2],z),diff(Vinp[1],z)-diff(Vinp[3],x),diff(Vinp[2],x)-diff(Vinp[1],y)];
for iv:1 step 1 thru lv do   
    (Vlistcurl[iv]:Vcurlop(Vlist[iv])); 

/* define Vx, Vy, Vz for rendering the vector field*/
Vx:Vselected[1];
Vy:Vselected[2];
Vz:Vselected[3];


/* build option list for selection */
iv:0;
/* ta out of for loop does not work, create the list manualy */
ta:[[Vlistcurl[1],if Vindex=1 then true else false]];
for iv:2 step 1 thru lv do ta:append(ta,[[Vlistcurl[iv],if Vindex=iv then true else false]]);
/* ta:[[Vlistcurl[1],false],[Vlistcurl[2],false],[Vlistcurl[3],false]];*/

/* set the selected vector field to 'true' */
ta[Vindex][2]:true;

tans:Vlistcurl[Vindex];
```

### Question Text
+	Given is a vector field  $V:\mathbb{R}^3\to\mathbb{R}^3$ by $V(x,y,z):=\begin{pmatrix}{@Vx@}\\{@Vy@}\\{@Vz@}\end{pmatrix}$ as shown in the diagram. Select the vector fields $\hat V$, so that $\hat V = \nabla \times V$ is valid.

+	JSXGraph applet using the functions and variables defined in **Question variables** plotting the 3D vector field and its curl in a projected plane, the angle of projection can be changed such that the vector fields can be viewed from multiple directions
+	`[[input:ans1]]` at the end of JSXGraph code to allow input of an answer of the student
+	`[[validation:ans1]]` checking of answer

#### Question text code


```javascript
<p>Given is a vector field  \(V:\mathbb{R}^3\to\mathbb{R}^3\) by \(V(x,y,z):=\begin{pmatrix}{@Vx@}\\{@Vy@}\\{@Vz@}\end{pmatrix}\) as shown in the diagram.</p>

<p>Select the vector fields \(\hat V\), so that \(\hat V = \nabla \times V\) is valid.</p>

[[jsxgraph width="500px" height="500px" input-ref-ans1='ans1Ref']]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [0, 10, 10,0], axis:false, shownavigation : false});
var box = [-3,3]
var view = board.create('view3d',
            [[2,2.5], [6, 6],
            [box, box, box]],
            {});
// Transform components of the vector function
var TF1 = board.jc.snippet('{#Vx#}', true, 'x,y,z');
var TF2 = board.jc.snippet('{#Vy#}', true, 'x,y,z');
var TF3 = board.jc.snippet('{#Vz#}', true, 'x,y,z');

var vector=[];
var scaleVec = 0.5;

/* Funktionen zum Plotten der Vektorfelder */
function clearVectorField(){
    board.removeObject(vector);
    vector=[];
}

function vectorField(){
    clearVectorField();
    board.suspendUpdate();
    var i,j,k,vx,vy;
    var pout=[];
    for(k=-2; k<2; k+=1){
        for(i=-2; i<2; i+=1){
            for(j=-2;j<2; j+=1){
                                //var norm = Math.max((i*i+ j*j ),0.001);
                               var norm =1;
                 vector.push(view.create('line3d',[[i, j,k ],
                                [TF1(i,j,k),TF2(i,j,k),TF3(i,j,k)],[0,scaleVec]],
                                {point: { withLabel: false},
                                point1: {visible: true, size: 1, color: 'red',strokeColor: 'red', withLabel: false},
                                point2: {visible: false, withLabel: false},
                                lastArrow:true, fixed: true, strokeColor:'red', highlight:false})
                            );

            }
        }
    }
board.unsuspendUpdate();
}
/* end helper functions */
vectorField();

board.update();
[[/jsxgraph]]
Select \(\hat V\).
<p>[[input:ans1]] [[validation:ans1]]</p>
```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type |Radio|
|Model answer | `ta` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, compact|
--- 
## Potential response tree
### prt1
| ![prt1](https://user-images.githubusercontent.com/120648145/209999029-fa4b3865-d361-47b8-a088-f86c5ffc5ded.PNG) |
|:--:|
| *Visualization of **prt1*** |

Feedback variables:

None needed, since `ans1` is selected by ticking a button.


| ![Node 1](https://user-images.githubusercontent.com/120648145/209999025-682c7f4b-23a9-4919-9782-f88854279609.PNG) |
|:--:|
| *Values of **node 1*** |
### Node 1
 |property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | ans1|
|TAns | tans| 
|Node 1 true feedback | Correct vector field selected.|
|Node 1 false feedback | Selected vector field does not fit. Please compute \\(\nabla \times V\\) for the given field. \\(\nabla \times V(x,y,z):=\begin{pmatrix}{@Vx@}\\\{@Vy@}\\\{@Vz@}\end{pmatrix}\\)|


## Todo:
* [ ] More options for vector fields
* [ ] Display definition of curl in solution
* [ ] **fix JSXGraph-Applet, does not work currently**

