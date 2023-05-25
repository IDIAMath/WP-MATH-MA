---
title: Rotation about two axis solo
usemathjax: true
theme: minima
---
## Aim of task
+	Student knows how a multidimensional curve is produced from varying a single parameter. (Handling mathematical symbols and formalism)
+	Student knows how rotational matrices change vectors (Handling mathematical symbols and formalism)
+ Student knows that the outcome of rotations is dependent on the order of operations 
+ Student can predict how a curve will change graphically once a rotational matrix is applied (Representing mathematical entities, Making use of aids and tools)
+ Student can reconstruct the axis of rotation and the order of operations from a rotated curve (Representing mathematical entities)

| ![First impression](https://private-user-images.githubusercontent.com/120648145/240869581-0a26ba30-dcb4-4fd8-b567-4dff6c1be322.PNG?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDA3NTk0LCJuYmYiOjE2ODUwMDcyOTQsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDg2OTU4MS0wYTI2YmEzMC1kY2I0LTRmZDgtYjU2Ny00ZGZmNmMxYmUzMjIuUE5HP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMDkzNDU0WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZTQ5YTJlNTlhZWQwY2EwMzE1MTVkMjUxNTc4OWMzNmJjOGFlNTcxZTA2ODI2Y2VlZWM0MjczMTE0MzVhYzFlOSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.OKe8PJfl-nuz9v-y8T-ZSecjzo4wRHTcpDSLuxVMRlQ) |
|:--:|
| *First impression of the question* |

## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
```math
t \mapsto \begin{pmatrix} 
r \cdot \cos(t) \\
r\cdot \sin(t) \\
0
\end{pmatrix}.
```
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about two different coordinate axis. The student is provided the concrete angles of rotation for rotations about each of the coordinate axis.
They need to find out, what axis the curve was rotated about and in which order the rotations where executed.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with angles of rotation for each of the coordinate axis. They are asked to select the correct order of operations from a multiple choice selection.

| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240869574-97273dcf-f5cb-42aa-8291-eacb9fca59b4.PNG?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDA3NTk0LCJuYmYiOjE2ODUwMDcyOTQsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDg2OTU3NC05NzI3M2RjZi1mNWNiLTQyYWEtODI5MS1lYWNiOWZjYTU5YjQuUE5HP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMDkzNDU0WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YzRlYjk1M2RhNjcxOTVhMDZkMDAyZDJmZjFhMWI3ZGQ5MTYyZDlkNDZhOTEyNjg0MzAzZmY5NDY5OTNhYjU0MSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.zbnTO-hO2t2chk-InvjWJE6uC8WttoBAGfk_VJ6qKKw) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for angles of rotation. In order to do this, they simply need to modify the entries in the lists specified e.g. change `alpahr : rand([1,2,3,4,5,6])/4*%pi;` to `phaser : rand([1/4,1/3,1/2,2/3])*%pi;`. 

Additionally, they can change the roational matrices to the ones they desire. In order to do this, they need to change the entries of `L1`, `L2` and `L3`. The first entry is the first row of the matrix.
Also, they can change the curve that is rotated. To do this, they need to change the entries of `Lv`. Here the fisrt entry is the first component, e.g. the $x$-coordinate.
They will need to change the question text as well to match the new curve and/or rotational matrices.

For an explanation of the processing of the values read **Question variables** and **Question text**.


| ![values the teacher can change](https://private-user-images.githubusercontent.com/120648145/240869580-d2ae3505-3e17-40f1-9b0b-6c69686ef4b3.PNG?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDA3NTk0LCJuYmYiOjE2ODUwMDcyOTQsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDg2OTU4MC1kMmFlMzUwNS0zZTE3LTQwZjEtOWIwYi02YzY5Njg2ZWY0YjMuUE5HP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMDkzNDU0WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YzgzZjk0YThmY2YxY2VjZjJmMmY5MTA0ZDRmODhjNjE2MjJkYWE1OGRjOTFmZmNjMzQ5NzA5ZmVjNzhhMTE3MiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.cUjpjdL-D8stKVWTHLzMiIU8dkxaOCfoHddnoqEk_u8) |
|:--:|
| *The above image shows which values the teacher may wish to change* |


## Question code

### Question Variables
+ the possible answers are saved to a list along with the information whether the answer is correct to allow for the radiobuttons (multiple choice) format
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

#### Question text code


```javascript
<p>The blue curve below \(c(t) = \begin{pmatrix} r\cdot \cos(t) \\ r\cdot \sin(t) \\ 0 \end{pmatrix}\) has been rotated about two of the coordinate axis. The result of the rotation is the orange curve. Find the correct order of operations.</p><p> The rotational angles about the \(x\)-, \(y\)-, and \(z\)-axis are \(\alpha = {@alphar@}, \beta = {@betar@}\) and \(\gamma = {@gammar@}\), respectively. Note: \(x-y\) means rotation about the \(x\)-axis first and \(y\)-axis second. </p>
[[jsxgraph width="500px" height="500px"]]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-8, 8, 8, -10], axis:false, shownavigation: false, keepaspectratio:true});
var box = [-3,3]
var view = board.create('view3d',
	[[-6, -3], [8, 8],
	[box, box, box]],
	{
		/*planes*/
		xPlaneRear: {visible:false},
		yPlaneRear: {visible:false}	
	});
var xlabel=view.create('point3d',[0.9*box[1],0,(0.6*box[0]+0.4*box[1])], {size:0,name:"x"});
var ylabel=view.create('point3d',[0,0.9*box[1],(0.6*box[0]+0.4*box[1])], {size:0,name:"y"});
var zlabel=view.create('point3d',[
        0.7*(0.6*box[0]+0.4*box[1]),
        0.7*(0.6*box[0]+0.4*box[1]),
        0.9*box[1]], 
        {size:0,name:"z"});    
       

/* define curve */

var c_base = view.create('curve3d', [
	(t) =>2* Math.cos(t),
	(t) =>2*  Math.sin(t),
	(t)=> 0,
	[0, Math.PI]], {strokeWidth: 2, strokeColor: '#1f84bc'});    
var xcoordraw =  '{#res[1]#}';
var ycoordraw =  '{#res[2]#}';
var zcoordraw =  '{#res[3]#}';	
			
var xcurve = board.jc.snippet(xcoordraw, true, 't');
var ycurve = board.jc.snippet(ycoordraw, true, 't');
var zcurve = board.jc.snippet(zcoordraw, true, 't'); 

var c_result = view.create('curve3d', [
(t) => xcurve(t),
(t) => ycurve(t),
(t) => zcurve(t),
[0, Math.PI]], {strokeWidth:2, strokeColor: '#EE442F'}); 



[[/jsxgraph]]

<p>[[input:ans1]] [[validation:ans1]]</p>
```
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

+ `checker` specifies what to look for in the list `ta`, namely the student's answer `ans1`
+ in the list, the position of `ans1` is saved as the variable `location`
+ from that, the corresponding matrices `M1s` and `M2s`can be found to depict the student's answer
+ the curve is calculated and exported like the reference solution and can later be displayed using JSXGraph

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

| ![prt1](https://private-user-images.githubusercontent.com/120648145/240872018-e215f1d1-4e35-4de8-a593-0b9d1b3591f5.PNG?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDA3OTU4LCJuYmYiOjE2ODUwMDc2NTgsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDg3MjAxOC1lMjE1ZjFkMS00ZTM1LTRkZTgtYTU5My0wYjlkMWIzNTkxZjUuUE5HP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMDk0MDU4WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MzA5ZDhlNjhiMWIxMWEwZTdiMjM5ODk3NDY4YTlmZWIxZDk1OWEzOWUyYzQ3OThmM2U2YWU5ODkwZmY1NWE0MiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.hdPhKbjiDESi7aMw-IWtfAD6UrZ278CTAQbIgoFkBUY) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | String|
|SAns | `ans1`|
|TAns | `tans[1]`| 
|Node 1 true feedback | `<p> Well done! You got the order of operations right! Will you dare to try again for a different set of angles?</p>`|

#### Node 1 false feedback:

Here, the student's answer is evaluated as a rotated curve and plotted for them to compare it to the correct answer.

Code:

```JavaScript
<p> Unfortunately, this is not the correct order of operations. <br>  In the following applet, you can see, how your answer would have looked like with the angles provided. The blue and orange curves are the way they were presented before. Your solution is displayed in purple. </p>
<p> Note: sometimes there are other correct solutions. If there is only a purple curve, it overlaps with the orange and your answer is correct, as well.</p>
[[jsxgraph width="500px" height="500px"]]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-8, 8, 8, -10], axis:false, shownavigation: false, keepaspectratio:true});
var box = [-3,3]
var view = board.create('view3d',
	[[-6, -3], [8, 8],
	[box, box, box]],
	{
		/*planes*/
		xPlaneRear: {visible:false},
		yPlaneRear: {visible:false}	
	});
var xlabel=view.create('point3d',[0.9*box[1],0,(0.6*box[0]+0.4*box[1])], {size:0,name:"x"});
var ylabel=view.create('point3d',[0,0.9*box[1],(0.6*box[0]+0.4*box[1])], {size:0,name:"y"});
var zlabel=view.create('point3d',[
        0.7*(0.6*box[0]+0.4*box[1]),
        0.7*(0.6*box[0]+0.4*box[1]),
        0.9*box[1]], 
        {size:0,name:"z"});    
       

/* define curve */

var c_base = view.create('curve3d', [
	(t) =>2* Math.cos(t),
	(t) =>2*  Math.sin(t),
	(t)=> 0,
	[0, Math.PI]], {strokeWidth: 2, strokeColor: '#1f84bc'});    



/*curve in original applet*/

var xcoordraw =  '{#res[1]#}';
var ycoordraw =  '{#res[2]#}';
var zcoordraw =  '{#res[3]#}';	
			
var xcurve = board.jc.snippet(xcoordraw, true, 't');
var ycurve = board.jc.snippet(ycoordraw, true, 't');
var zcurve = board.jc.snippet(zcoordraw, true, 't'); 

var c_result = view.create('curve3d', [
(t) => xcurve(t),
(t) => ycurve(t),
(t) => zcurve(t),
[0, Math.PI]], {strokeWidth:2, strokeColor: '#EE442F'}); 

/* curve based on student answer */

var sxcoordraw =  '{#studentres[1]#}';
var sycoordraw =  '{#studentres[2]#}';
var szcoordraw =  '{#studentres[3]#}';	
			
var sxcurve = board.jc.snippet(sxcoordraw, true, 't');
var sycurve = board.jc.snippet(sycoordraw, true, 't');
var szcurve = board.jc.snippet(szcoordraw, true, 't'); 

var c_student = view.create('curve3d', [
(t) => sxcurve(t),
(t) => sycurve(t),
(t) => szcurve(t),
[0, Math.PI]], {strokeWidth:2, strokeColor: '#601A4A'}); 

[[/jsxgraph]]
``` 
| ![node 1](https://private-user-images.githubusercontent.com/120648145/240872024-1ef20f99-2e43-452b-8ffb-0048e073791d.PNG?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDA3OTU4LCJuYmYiOjE2ODUwMDc2NTgsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDg3MjAyNC0xZWYyMGY5OS0yZTQzLTQ1MmItOGZmYi0wMDQ4ZTA3Mzc5MWQuUE5HP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMDk0MDU4WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NWNjMWY3ZWQ5NDE0Y2UyOGVkYjFlMmI1MjgxMWJhYTRjZDU4MzVmNGFkMzFmMzU4OTEzZTViYzFiMzdmODc4NyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.v-v2DA86GCxOI_VGy8z1KPqplrC3M1Rca6nYZUpV2X4) |
|:--:|
| *Values of **node 1*** |

| ![Feedback](https://private-user-images.githubusercontent.com/120648145/240872026-d464c6c0-ae5e-4662-a08b-bd91927ba05f.PNG?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg1MDA3OTU4LCJuYmYiOjE2ODUwMDc2NTgsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDg3MjAyNi1kNDY0YzZjMC1hZTVlLTQ2NjItYTA4Yi1iZDkxOTI3YmEwNWYuUE5HP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjVUMDk0MDU4WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MmFmZjZhYWMyNWQzNGM5OThjNjZjOGU2ZDRkYzQ3YjdhYTY2NTdmN2QxZGJhZjFkYzBmZDFjNDE5MTMxMGQ2MCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.yw3iXV7pXZ2p31JMzCVxP-EPpH95zZs1-aiinsmvxjI) |
|:--:|
| *Feedback upon incorrect answer * |





## Todo:
* [x] Update figures
