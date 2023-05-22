---
title: Rotation about two axis adaptive
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows how a multidimensional curve is produced from varying a single parameter. (Handling mathematical symbols and formalism)
+	Student knows how rotational matrices change vectors (Handling mathematical symbols and formalism)
+ Student knows that the outcome of rotations is dependent on the order of operations 
+ Student can predict how a curve will change graphically once a rotational matrix is applied (Representing mathematical entities, Making use of aids and tools)
+ Student can reconstruct the axis of rotation and the order of operations from a rotated curve (Representing mathematical entities)

# Exercise layout
This is an adaptive tutorial task. That means, a relatively hard task is presented. When the task is answered incorrectly, a series of other tasks is activated. These tasks cover the fundamentals necessary to solve the initial problem. The next figure depicts the scheme.
The tasks are documented seperately, but no in complete detail in this document. Some of the tasks are availabe as stand-alone exercises.


| ![First impression](https://user-images.githubusercontent.com/120648145/233791552-098c7f94-1c3a-43e2-8644-623bcb9ab5f6.jpg) |
|:--:|
| *First impression of the question* |


## Question Variables

The tasks are programmed in the same Question Text. However, they are each wrapped in a `<div>`-environment. That way, they can be accessed individually. For better legibility, in this documentation the individual tasks are presented as if they were seperate Question Texts sharing the same Question Variables.

The Question Variables set up a number of things:
+ the multiplication of matrices by converting lists to matrices, multpilying them and turning them to lists again for export
+ the randomization of the order of rotation for the initial task
+ the randomization of the angles $\alpha, \beta, \gamma$ provided 
+ the conversion of the randomized angles into mumerical values for plotting
+ the matrix mutliplication for the reference curve in the initial task
+ the matrix multiplication for the reference curve in task1
+ the matrix multiplication for the reference curve in task2a
+ the matrix multiplication for the reference curve in task2b
+ the randomization of the order of rotation for task3
+ the randomization of new angle `ap_betar` to use in task3
+ the matrix multiplication for the reference curve in task3

```


/* implement the creation of matrices from lists */

listtomat(L):=block(
 [i, M], 
 M:matrix(), 
 for i:1 thru length(L) do M:addrow(M,L[i]),
 return(M)
);
mattolist(M):=makelist(M[i],i,1,length(M));

/* specify the lists to be turnt into matrices */
r: 2;
L1: [[1,0,0],[0,cos(a),-sin(a)],[0, sin(a), cos(a)]];
L2: [[cos(b),0,sin(b)],[0,1,0],[-sin(b), 0, cos(b)]];
L3: [[cos(c),-sin(c),0],[sin(c),cos(c),0],[0, 0, 1]];
Lv: [[r*cos(t),0,0],[r*sin(t),0,0],[0,0,0]];

/* create matrices */

M1: listtomat(L1);
M2: listtomat(L2);
M3:listtomat(L3);
v: listtomat(Lv);

matlist: [M1,M2,M3];

/* randomize the order of operations for initial task */
indexr: 1+rand(6)
ta: [[string(x-y),false],[string(y-x),false],[string(x-z),false],[string(z-x),false],[string(y-z),false],[string(z-y), false]];
ta[indexr][2]:true;
tans: ta[indexr];

/* select matrices for multiplication for initial task */

indexlist:[[1,2],[2,1],[1,3],[3,1],[2,3],[3,2]];
indices: indexlist[indexr];

M1r: matlist[indices[1]];
M2r: matlist[indices[2]];

alphar: rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;
betar:  rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;
gammar: rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;
deltar: rand([1/6,1/4,1/3,2/3,3/4,5/4,4/3])*%pi;

/* numerical values */
numer: true
alpha: alphar;
beta: betar;
gamma: gammar;
delta: deltar;
numer: false

/* calculate matrix product and evalutate angles for initial task */
matres: ev(M2r.M1r.v, a:alphar, b:betar, c: gammar);

/* turn matrix to list for export*/
res: [mattolist(matres)[1][1],mattolist(matres)[2][1],mattolist(matres)[3][1]];




/* Rotation about one axis */
or_matres: ev(M1.v, a:deltar);
or_res: [mattolist(or_matres)[1][1],mattolist(or_matres)[2][1],mattolist(or_matres)[3][1]];



/* Rotation about two axis matching */
trm_matres: ev(M3.M2.v, b:betar, c: gammar);
trm_res: [mattolist(trm_matres)[1][1],mattolist(trm_matres)[2][1],mattolist(trm_matres)[3][1]];

/* Rotation about two axis observing */
tro_matres: ev(M1.M3.v, a:alphar, c:gammar);
tro_res: [mattolist(tro_matres)[1][1],mattolist(tro_matres)[2][1],mattolist(tro_matres)[3][1]];

/* Rotation about two known axis in unknown order - "ap" is short for "axis pair"*/
ap_betar: rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;
while ap_betar = alphar do ap_betar: rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;
ap_in: rand([1,2]);
ap_matlist:[[M2,M3],[M3,M2]];
ap_M1r: ap_matlist[ap_in][1];
ap_M2r: ap_matlist[ap_in][2];

ap_ta: [[string(y-z),false],[string(z-y), false]];
ap_ta[ap_in][2]:true;
ap_tans: ap_ta[ap_in];
ap_matres: ev(ap_M2r.ap_M1r.v, b: alphar, c: ap_betar);
ap_res: [mattolist(ap_matres)[1][1],mattolist(ap_matres)[2][1],mattolist(ap_matres)[3][1]];

```


# Initial task (Rotating a curve about two unknown axis)

| ![First impression](https://user-images.githubusercontent.com/120648145/233791552-098c7f94-1c3a-43e2-8644-623bcb9ab5f6.jpg) |
|:--:|
| *First impression of the question* |

## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
$$  t \mapsto \begin{pmatrix} 
r \cdot \cos(t) \\
r\cdot \sin(t) \\
0
\end{pmatrix}. $$
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about two different coordinate axis. The student is provided the concrete angles of rotation for rotations about each of the coordinate axis.
They need to find out, what axis the curve was rotated about and in which order the rotations where executed.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with angles of rotation for each of the coordinate axis. They are asked to select the correct order of operations from a multiple choice selection.

| ![Click draw button](https://user-images.githubusercontent.com/120648145/233791555-f9ccb417-cea3-45a4-8551-3b38b9d9748d.jpg) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for angles of rotation. In order to do this, they simply need to modify the entries in the lists specified e.g. change `alpahr : rand([1,2,3,4,5,6])/4*%pi;` to `phaser : rand([1/4,1/3,1/2,2/3])*%pi;`. 

For an explanation of the processing of the values read **Question variables** and **Question text**.


| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/233791551-bfa998c4-8045-4be9-9146-e62fdedc7aa2.jpg) |
|:--:|
| *The above image shows which values the teacher may wish to change* |


## Question code

### Question Variables
+	the possible answers are saved to a list along with the information whether the answer is correct to allow for the radiobuttons (multiple choice) format
+ one possibility is randomly selected and assigned the bool `true` - this is the correct answer
+ `alphar`, `betar`, `gammar` are randomly selected rational multiples of $\pi$ created using `rand()`, division and multiplication
+ the rotational matrices for rotations about the $x$,$y$ and $z$-axis are given as lists of 3 lists with 3 elements each, resulting in the 9 elements of a matrix
+ the lists of lists are converted to matrices using the function "listtomat" in order to perform matrix multiplications
+ the parametrized curve is saved into a vector to be eligible for matrix multiplication
+ the matrices `M1r` and `M2r` are selected as the rotational matrices using the same index as the true answer 
+ the results are evaluated for the angles and saved to the variable `matres`
+ the matrix is converted to a list `res` in order to export the results to JSXGraph




#### Question variable code
```jacascript
/* randomize the order of operations */
indexr: 1+rand(6)
ta: [[string(x-y),false],[string(y-x),false],[string(x-z),false],[string(z-x),false],[string(y-z),false],[string(z-y), false]];
ta[indexr][2]:true
tans: ta[indexr]

/* implement the creation of matrices from lists */

listtomat(L):=block(
 [i, M], 
 M:matrix(), 
 for i:1 thru length(L) do M:addrow(M,L[i]),
 return(M)
);
mattolist(M):=makelist(M[i],i,1,length(M));

/* specify the lists to be turnt into matrices */
r: 2;
L1: [[1,0,0],[0,cos(a),-sin(a)],[0, sin(a), cos(a)]];
L2: [[cos(b),0,sin(b)],[0,1,0],[-sin(b), 0, cos(b)]];
L3: [[cos(c),-sin(c),0],[sin(c),cos(c),0],[0, 0, 1]];
Lv: [[r*cos(t),0,0],[r*sin(t),0,0],[0,0,0]];

/* create matrices */

M1: listtomat(L1);
M2: listtomat(L2);
M3:listtomat(L3);
v: listtomat(Lv);

matlist: [M1,M2,M3];

/* select matrices for multiplication */

indexlist:[[1,2],[2,1],[1,3],[3,1],[2,3],[3,2]];
indices: indexlist[indexr];

M1r: matlist[indices[1]];
M2r: matlist[indices[2]];

alphar: rand([1,2,3,5,6])/4*%pi;
betar:  rand([1,2,3,5,6])/4*%pi;
gammar: rand([1,2,3,5,6])/4*%pi;

/* calculate matrix product and evalutate angles */
matres: ev(M2r.M1r.v, a:alphar, b:betar, c: gammar);

/* turn matrix to list for export*/
res: [mattolist(matres)[1][1],mattolist(matres)[2][1],mattolist(matres)[3][1]];


```

### Question Text
+ Task explanation using LaTex, importing the random values from **Question variables**
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans1]]` at the end of JSXGraph code to allow input of  answers of the student for r, a and phi and n respectively
+	`[[validation:ans1]]`is used for checking of answer


## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Radiobuttons|
|Model answer | `ta` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---

## Potential response tree
### prt1

In the following, the feedback variables are given. Here, the student answer is processed to be able to show them, how their incorrect answer would look like. That way, they can compare their result to the correct solution and reflect on their train of thought leading up to the error.

Feedback variables:
```
checker: ans1;
for i:1 thru length(ta) step 1 do(if member(checker, [ta[i][1]]) then location:i);
location;


studentindices: indexlist[location];

M1s: matlist[studentindices[1]];
M2s: matlist[studentindices[2]];

/* calculate matrix product and evalutate angles */
studentmatres: ev(M2s.M1s.v, a:alphar, b:betar, c: gammar);

/* turn matrix to list for export*/
studentres: [mattolist(studentmatres)[1][1],mattolist(studentmatres)[2][1],mattolist(studentmatres)[3][1]];

```

| ![prt1](https://user-images.githubusercontent.com/120648145/233791553-f9011fed-26f3-4f88-836a-f208c8649343.jpg) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `ans1`|
|TAns | `tans[1]`| 
|Node 1 true feedback | `<p> Nice, you found the correct order of operations! </p>`|

#### Node 1 false feedback:

Here, the student's answer is evaluated as a rotated curve and plotted for them to compare it to the correct answer.



| ![Feedback](https://user-images.githubusercontent.com/120648145/233791702-da37c675-28a1-4a9e-9750-58060f9186f3.jpg) |
|:--:|
| *Feedback upon incorrect answer * |





## Todo:
* [x] Update figures

