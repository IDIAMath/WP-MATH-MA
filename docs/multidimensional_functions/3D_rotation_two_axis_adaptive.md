---
title: Rotating a curve about two axis adaptive
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


| ![Overview](https://private-user-images.githubusercontent.com/120648145/239914246-c663f94c-b5d8-443a-9185-79fcca29cce1.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0NzYwMzYxLCJuYmYiOjE2ODQ3NjAwNjEsInBhdGgiOiIvMTIwNjQ4MTQ1LzIzOTkxNDI0Ni1jNjYzZjk0Yy1iNWQ4LTQ0M2EtOTE4NS03OWZjY2EyOWNjZTEucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMiUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjJUMTI1NDIxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9OWI1ZmU3NjI0ZTYzZTgxM2Q5NTg3MGZjYTQ1M2I2OTE2ZDYxZTg0NDBmMjIwMmNhYmU1OGY0MzYwY2Q3YTA1ZCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.2YcKPQ4eR8JXBa-eWohAOESpRJfKeoxl6g4QxQY_3Es) |
|:--:|
| *Overview of the task.* |


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

| ![First impression](https://private-user-images.githubusercontent.com/120648145/240385755-309e330d-9a0f-494b-bde6-b123f6ea7a1a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY2ODk5LCJuYmYiOjE2ODQ4NjY1OTksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NTc1NS0zMDllMzMwZC05YTBmLTQ5NGItYmRlNi1iMTIzZjZlYTdhMWEucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgyOTU5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZTkzNWQxYmViMzAzYmM2MTE3YjUxNjA1ZTlhMTNmOTgxMDZlOTFlYTczMjhkZGZmNjMzYTVmMmYzNmE0MDVhMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.WOYyuz5Z14uDjj9Kw8gq2eL7VGj2P8-UENpiQpL1bv4) |
|:--:|
| *First impression of the question* |


## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
```math
t \mapsto \begin{pmatrix} 
r \cdot \cos (t) \\
r \cdot \sin (t) \\
0
\end{pmatrix}.
```
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about two different coordinate axis. The student is provided the concrete angles of rotation for rotations about each of the coordinate axis.
They need to find out, what axis the curve was rotated about and in which order the rotations where executed.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with angles of rotation for each of the coordinate axis. They are asked to select the correct order of operations from a multiple choice selection.

| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240385755-309e330d-9a0f-494b-bde6-b123f6ea7a1a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY2ODk5LCJuYmYiOjE2ODQ4NjY1OTksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NTc1NS0zMDllMzMwZC05YTBmLTQ5NGItYmRlNi1iMTIzZjZlYTdhMWEucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgyOTU5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZTkzNWQxYmViMzAzYmM2MTE3YjUxNjA1ZTlhMTNmOTgxMDZlOTFlYTczMjhkZGZmNjMzYTVmMmYzNmE0MDVhMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.WOYyuz5Z14uDjj9Kw8gq2eL7VGj2P8-UENpiQpL1bv4) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for angles of rotation. In order to do this, they simply need to modify the entries in the lists specified e.g. change `alpahr : rand([1,2,3,4,5,6])/4*%pi;` to `phaser : rand([1/4,1/3,1/2,2/3])*%pi;`. 

For an explanation of the processing of the values read **Question variables** and **Question text**.


### Question variables used

+ the possible answers are saved to list `ta` along with the information whether the answer is correct to allow for the radiobuttons (multiple choice) format
+ one possibility is randomly selected and assigned the bool `true` - this is the correct answer
+ `alphar`, `betar`, `gammar` are randomly selected rational multiples of $\pi$ created using `rand()`, division and multiplication
+ the rotational matrices for rotations about the $x$,$y$ and $z$-axis are given as lists of 3 lists with 3 elements each, resulting in the 9 elements of a matrix
+ the lists of lists are converted to matrices using the function "listtomat" in order to perform matrix multiplications
+ the parametrized curve is saved into a vector to be eligible for matrix multiplication
+ the matrices `M1r` and `M2r` are selected as the rotational matrices using the same index as the true answer 
+ the results are evaluated for the angles and saved to the variable `matres`
+ the matrix is converted to a list `res` in order to export the results to JSXGraph



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

| ![prt1](https://private-user-images.githubusercontent.com/120648145/240385712-18d69ca0-2c9d-4b0c-9724-beb75c128f01.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY2ODk5LCJuYmYiOjE2ODQ4NjY1OTksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NTcxMi0xOGQ2OWNhMC0yYzlkLTRiMGMtOTcyNC1iZWI3NWMxMjhmMDEucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgyOTU5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MzAyZWQ5MDdmNTkwMWQ0MDI0ZWIyM2Q2ODE5ZWEyNjM5MWUwMzM1MTJjZjYxY2ExMGI0YzliYjNjZTc2ZWJkMCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.RnbhVvf5cJVlPFONm1KBFO5B16v7x47Su4vRM0AqyYk) |
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
```
<p> Unfortunately, this is not the correct order of operations. <br>  In the following applet, you can see, how your answer would have looked like with the angles provided. The blue and orange curves are the way they were presented before. Your solution is displayed in purple. </p>
<p> Note: sometimes there are other correct solutions. If there is only a purple curve, it overlaps with the orange and your answer is correct, as well.</p>
```
| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240385715-0c45a0b4-0f9e-4665-bbf8-013dc7cc7e30.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY2ODk5LCJuYmYiOjE2ODQ4NjY1OTksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NTcxNS0wYzQ1YTBiNC0wZjllLTQ2NjUtYmJmOC0wMTNkYzdjYzdlMzAucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgyOTU5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9OWM4NTc4YzA4NTdjNDM5ZGMwZWUwYWFiMTYzMWI0MDQ3Y2E1MDhhOTI3ZDE0Y2UzNjNiNThlMTk4ZGE5YTBlNSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.fqkwOqF37QTZXhbu9WBsLB4EEeF7R9cG-44olHaFZmQ) |
|:--:|
| *Values of **Node 1*** |


| ![Feedback](https://private-user-images.githubusercontent.com/120648145/240385779-63fb49bb-f794-44ff-943c-f053250fc860.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY2ODk5LCJuYmYiOjE2ODQ4NjY1OTksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NTc3OS02M2ZiNDliYi1mNzk0LTQ0ZmYtOTQzYy1mMDUzMjUwZmM4NjAucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgyOTU5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9N2UwM2ZhYTIwOGEwZDI2ZTJhZDEwY2E2NDViMDBkMzJhODcyNGVlMTRmMWZjYWE5NzE1NDRmMjZkNzlmODZlMCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.J7WM58FLSAAPKJxJE02uYzxUhO98OczqiyA4eYnzyKE) |
|:--:|
| *Feedback upon incorrect answer * |

# Input 1: Rotational matrices and 3D rotations

In case of answering the first task incorrectly, the student is presented the following sequence of tasks. The first step is an introductory text explaining rotations in 3D and rotational matrices. The text is as follows:
<hr>

Let's repeat, what exactly rotating a curve means. First of all, a curve is represented by a vector as a function of its parameter. As with any vector, it can be multiplied with a matrix to rotate. 

This matrix is called the rotational matrix. In a 3D vector-space with euklidian base, one can easily define 3 rotations $R_x ,R_y, R_z$ about the axis

```math
   
   R_x =\begin{pmatrix}
        1 &0 &0\\
        0& \cos(\alpha) & -\sin(\alpha)\\
        0& \sin(\alpha) &\cos(\alpha) 
    \end{pmatrix},
    \quad
    R_y =\begin{pmatrix}
        \cos(\alpha) &0 &\sin(\alpha)\\
        0&1  & 0\\
         -\sin(\alpha) &0&\cos(\alpha) 
    \end{pmatrix} ,
    \quad
    R_z =\begin{pmatrix}
        \cos(\alpha) & -\sin(\alpha) &0\\
         \sin(\alpha) &\cos(\alpha) &0\\
        0 &0&1
    \end{pmatrix} .
```
A rotation of angle $\alpha$ is performed by multiplying the vector $v$ with the desired rotational matrix in the form $v_\text{rotated} = R_i \cdot v$.
Go on to the next task to look at an easy rotation.
<hr>

# Task 1: Rotation about one axis


| ![First impression](https://private-user-images.githubusercontent.com/120648145/240387362-a5afb547-6e0b-40c1-9a85-31281248bf93.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3MzAxLCJuYmYiOjE2ODQ4NjcwMDEsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NzM2Mi1hNWFmYjU0Ny02ZTBiLTQwYzEtOWE4NS0zMTI4MTI0OGJmOTMucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzNjQxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZWIxMDY4ZTFmM2RhZWNhZmM0MTg0ZTAzMTE0OWVhMGI1MDYzODc0NWFmNjRkMTA1MjE5NDJiNzE1MDY5MzlhMiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.nQ63UuL1ItQHikbqoaz7Lexy8HvupO-tFCg8VflBJ5s) |
|:--:|
| *First impression of the question* |


## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
```math
t \mapsto \begin{pmatrix} 
r \cdot \cos (t) \\
r \cdot \sin (t) \\
0
\end{pmatrix}.
```
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about a coordinate axis. The student is provided with the resulting rotated curve.
They need to find out, what angle of rotation is.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with two curves that can be changed into one another by rotation about a coordinate axis. They are asked to find the correct rotational angle with the help of a slider.
| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240387340-4fe6cadf-83ca-4dcf-9769-3210111b4e59.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3MzAxLCJuYmYiOjE2ODQ4NjcwMDEsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NzM0MC00ZmU2Y2FkZi04M2NhLTRkY2YtOTc2OS0zMjEwMTExYjRlNTkucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzNjQxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9Y2U3ODJkMGQ0Y2VkNDdhYTMxMWYwMGE2MTY2MzUzMjYxMTU3Yjk1NmZlMjIxMWE3YTM3YTNiZDhkMWY0OGI0MiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.PsGJC7KqGZ-mBpj3msxBHNKG-feRibNU_eb8q03cE8s) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for the angle of rotation. In order to do this, they simply need to modify the entries in the list specified e.g. change `deltar : rand([1/6,1/4,1/3,2/3,3/4,5/4,4/3])*%pi;` to `deltar: rand([3/4,5/4,4/3])*%pi;`. 

For an explanation of the processing of the values read **Question variables** and **Question text**.


### Question variables used

+ `deltar` is a randomly selected rational multiple of $\pi$ created using `rand()`, division and multiplication
+ the matrix `M1` is used for the matrix product
+ the results are evaluated for the angle and saved to the variable `or_matres`
+ the matrix is converted to a list `or_res` in order to export the results to JSXGraph



### Question Text
+ Task explanation using LaTex, importing the random values from **Question variables**
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans2]]` at the end of JSXGraph code to allow input of  answers of the student for r, a and phi and n respectively
+	`[[validation:ans2]]`is used for checking of answer


## Answers
### Answer ans 2
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `deltar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---

## Potential response tree
### prt2

Feedback variables:
```
ans2;
```

| ![prt2](https://private-user-images.githubusercontent.com/120648145/240387861-7cf10434-a589-4e2e-afe4-229e290bf7e2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3NDEzLCJuYmYiOjE2ODQ4NjcxMTMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4Nzg2MS03Y2YxMDQzNC1hNTg5LTRlMmUtYWZlNC0yMjllMjkwYmY3ZTIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzODMzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YjBmMmVhNzA0M2NhNjczODIxMmU1ZWVmYWUwMDU4YTU5NzlkNWU2NmE3YTEyYjU2OWRkM2I0YzU2ZjQ5MTk1ZSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.oQ3vnqqCNv91xl3Xo8KN8alSvx08xx20zQBVZ3X0MtI) |
|:--:|
| *Visualization of **prt2*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `ans2`|
|TAns | `deltar`| 
#### Node 1 true feedback 
```
 <p> Nice! You found the correct angle. Good job! </p>
 <p> Let's have a look at the mathematics of multiple rotations. Click the button to go on.</p>
 <p>
        <button type="button" onclick="hide('task1');show('input2');">Continue</button>
 </p>
 ```

#### Node 1 false feedback 
```
<p> You did not find the correct angle. The correct angle is {@deltar@}. Have a look, whether the curves really overlapped perfectly. </p>
 <p> Let's have a look at the mathematics of multiple rotations. Click the button to go on.</p>
 <p>
        <button type="button" onclick="hide('task1');show('input2');">Continue</button>
    </p> 
```
| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240387862-efea22a3-f1c6-4865-b239-a38ab54c03d2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3NDEzLCJuYmYiOjE2ODQ4NjcxMTMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4Nzg2Mi1lZmVhMjJhMy1mMWM2LTQ4NjUtYjIzOS1hMzhhYjU0YzAzZDIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzODMzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MDAyODg3YmU5MTI2NGE4MTI5YmQzZGVkNGVjYWU4YjMzM2RkNzlmM2VkMjNlNDg0Mzg0YmU4MWViMDJlYjIxOSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.w999V4-OvrBVUXW9rnEcRHKNEo_Pj4RdUPrMNJ5pgVs) |
|:--:|
| *Values of **Node 1*** |
# Input 2: Rotations about multiple axis

Before rotations about two axis are object of the intermittent tasks, another text is presented. The text is as follows:
<hr>

 <p>If a rotation is performed about multiple, say 2 axis, the corresponding rotational axis are multiplied. To execute the first rotation, the matrix is multiplied to the vecotr from the left. All consecutive rotational matrices are multiplied from the left, as well. This way, if you have rotations 1,2 and 3, the resulting rotational matrix is $R_\text{res} = R_3\cdot R_2\cdot R_1$.
<br> However, since matrix multiplication is not commutative, the order of execution matters.
    <br>
    For example, for a rotation about the \(x\)-axis with an angle of $\alpha=60^\circ$ and a rotation about the $y$-axis with an angle of $\beta=45^\circ$, we get the following results

```math
 
 R_x(60^\circ) \cdot R_y(45^\circ) =
 \begin{pmatrix}
 \cos{\left(\beta \right)} & 0 & \sin{\left(\beta \right)}\\
 \sin{\left(\alpha \right)} \sin{\left(\beta \right)} & \cos{\left(\alpha \right)} & - \sin{\left(\alpha \right)} \cos{\left(\beta \right)}\\
 -\sin{\left(\beta \right)} \cos{\left(\alpha \right)} & \sin{\left(\alpha \right)} & \cos{\left(\alpha \right)} \cos{\left(\beta \right)}
 \end{pmatrix}= 
 \begin{pmatrix}
 \frac{\sqrt{2}}{2} & 0 & \frac{\sqrt{2}}{2}\\
 \frac{\sqrt{6}}{4} & \frac{1}{2} & - \frac{\sqrt{6}}{4}\\
 -\frac{\sqrt{2}}{4} & \frac{\sqrt{3}}{2} & \frac{\sqrt{2}}{4}
 \end{pmatrix}
```
    
and with the switched order of operation
    
```math
 R_y(45^\circ) \cdot R_x(60^\circ) =
 \begin{pmatrix}
 \cos{\left(\beta \right)} & \sin{\left(\alpha \right)} \sin{\left(\beta \right)} & \sin{\left(\beta \right)} \cos{\left(\alpha \right)}\\
 0 & \cos{\left(\alpha \right)} & -\sin{\left(\alpha \right)}\\
 -\sin{\left(\beta \right)} & \sin{\left(\alpha \right)} \cos{\left(\beta \right)} & \cos{\left(\alpha \right)} \cos{\left(\beta \right)}
 \end{pmatrix}= 
 \begin{pmatrix}
 \frac{\sqrt{2}}{2} & \frac{\sqrt{6}}{4} & \frac{\sqrt{2}}{4}\\
 0 & \frac{1}{2} & - \frac{\sqrt{3}}{2}\\
 -\frac{\sqrt{2}}{2} & \frac{\sqrt{6}}{4} & \frac{\sqrt{2}}{4}
 \end{pmatrix}
```
    
Therefore, the resulting vector will be different.
In the next task, you can get familiar with a rotation about two axis.

<hr>

# Task 2a: Rotation about two known axis with unknown angles

| ![First impression](https://private-user-images.githubusercontent.com/120648145/240387345-7bc063ec-a252-4077-98e4-c01770d84cd2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3MzAxLCJuYmYiOjE2ODQ4NjcwMDEsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NzM0NS03YmMwNjNlYy1hMjUyLTQwNzctOThlNC1jMDE3NzBkODRjZDIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzNjQxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NTk5N2Q4ZTI4NTM2MDM0ZTQ4MjVhZjZiMjQxOWJmNWY2ZjNjNjcwZGUyZjYyOTdiODMyZGQzODNjY2YwNjAzYyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.67RWmYEH78jN_gayEs5itO_gY7matSvMqjUVyT_mids) |
|:--:|
| *First impression of the question* |


## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
```math
t \mapsto \begin{pmatrix} 
r \cdot \cos (t) \\
r \cdot \sin (t) \\
0
\end{pmatrix}.
```
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about two coordinate axis. The student is provided with the coordinate axis and the order of operation.
They need to find out, what the angles of rotation are.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with two curves that can be changed into one another by rotation about two coordinate axis. They are asked to find the correct rotational angles with the help of two sliders.
| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240387348-c01829d5-057e-4cdf-a164-0bd1d5cfadb1.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3MzAxLCJuYmYiOjE2ODQ4NjcwMDEsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4NzM0OC1jMDE4MjlkNS0wNTdlLTRjZGYtYTE2NC0wYmQxZDVjZmFkYjEucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzNjQxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ODhjMjY5MTBiOGIzYWMzMDI1MGNjN2Y4ZDBiNjc4OTVhZmQ2MDg0MGRjYTM4MmQxZTU0ZWRiYWE4OWFiZDM3NCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.w6vFQWH8VlUinhXbqCadRODhUh4T3ZcI4DHGO8JpP4M) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for the angle of rotation. They can add a new variable for the angle in the same manner the other angles are randomized. Otherwise, they can change the list of possible values for the variables `betar` and `gammar` used in this task.  In order to do this, they simply need to modify the entries in the list specified e.g. change `betar : rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;` to `betar: rand([3/4,5/4,4/3])*%pi;`. 

For an explanation of the processing of the values read **Question variables** and **Question text**.


### Question variables used

+ `betar` and `gammar` are the same variables used in the initial task
+ the matrix `M2` and `M3` are used for the matrix product
+ the results are evaluated for the angle and saved to the variable `trm_matres`
+ the matrix is converted to a list `trm_res` in order to export the results to JSXGraph



### Question Text
+ Task explanation using LaTex, importing the random values from **Question variables**
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans3]]`, `[[input:ans4]]` at the end of JSXGraph code to allow input of  angles. This is done automatically by binding the slider.
+	`[[validation:ans3]]`, `[[validation:ans4]]` is used for checking of answer


## Answers
### Answer ans 3
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `betar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 4
|property | setting| 
|:---|:---|
|Input type | Numerical|
|Model answer | `gammar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
## Potential response tree

### prt3

Feedback variables:
```
ans3;
ans4;
```

| ![prt3](https://private-user-images.githubusercontent.com/120648145/240387864-507df4c5-de1a-4305-b10d-61e8b75b1c57.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3NDEzLCJuYmYiOjE2ODQ4NjcxMTMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4Nzg2NC01MDdkZjRjNS1kZTFhLTQzMDUtYjEwZC02MWU4Yjc1YjFjNTcucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzODMzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MmJhMGY0MDgwNTViMjk5ZjEzMjFlNGJiZmI2MDQ1ZWJkYzBhZjY4Mjc2MGI4MmIwNWE4YWY4NjE0NjFiZmY1YSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.lqde5eWIWrX_U4n-VRscCJ_OYUBGmZG9GYprQ9piiA8) |
|:--:|
| *Visualization of **prt3*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `ans3`|
|TAns | `beta`| 
|Node 1 true feedback |  <p> Nice! You found the correct angle \(\alpha\). Good job! </p>|
|Node 1 false feedback | <p> The value you gave for angle \(\alpha\) is not yet correct. The correct value is {@betar@}. </p>|


| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240387868-44d218a8-565f-42ed-9f8a-fa01b69384c4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3NDEzLCJuYmYiOjE2ODQ4NjcxMTMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4Nzg2OC00NGQyMThhOC01NjVmLTQyZWQtOWY4YS1mYTAxYjY5Mzg0YzQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzODMzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9OGVjMWFkNmIzN2ZhYjEzMTUwNjU0N2ZjYWIxY2M0MGZlYWY2ZjI3MzIwMWI4YmE4MDNhNDU3MzY5ZjIzYWY0ZCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.WNLHULQQpw1E8iRBmzF_niHZoDOeyn_84jVlFB83AHc) |
|:--:|
| *Node 1* |



### Node 2
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `ans4`|
|TAns | `gamma`| 

#### Node 2 true feedback 
```<p> Nice! You also found the correct angle \(\beta\). Good job! </p> <p> Perfect! You got both angles right! </p>
<br>
<p> In the next task, you can use your experience from this task, to find out the angles without sliders.
    
    <p>
        <button type="button" onclick="hide('task2a');show('task2b');">Continue</button>
    </p> </p>
```   
  
#### Node 2 false feedback 
```<p> The value you gave for angle \(\beta\) is not yet correct. The correct value is {@gammar@}.  Make sure the curves overlap perfectly.</p>
<br>

<p> In the next task, you can use your experience from this task, to find out the angles without sliders.
    
    <p>
        <button type="button" onclick="hide('task2a');show('task2b');">Continue</button>
    </p>not correct.<br></p>
```

| ![Node 2](https://private-user-images.githubusercontent.com/120648145/240387870-76a813b2-8524-4b10-b276-c6b8f8f09f1d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3NDEzLCJuYmYiOjE2ODQ4NjcxMTMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4Nzg3MC03NmE4MTNiMi04NTI0LTRiMTAtYjI3Ni1jNmI4ZjhmMDlmMWQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzODMzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NDI1ZWIwNjIzYWM1MTBmN2UyZDI2OGFhZjdiZjlmM2FjNTgxMzQ3OTcyZTZkMDdmMDRhNzQyYWI4NTNkYzYzNyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.MgbzfeAU4yXWiiEPLxwLBkk95JkY4GFyN1pLH8sZhj4) |
|:--:|
| *Node 2* |
### Node 3
|property | setting| 
|:---|:---|
|Answer Test | NumAbsolute|
|SAns | `ans4`|
|TAns | `gamma`| 

#### Node 3 true feedback 
```<p> Nice! You found the correct angle \(\beta\). Good job! Check, whether you did anything differently for \(\alpha\). </p>
<br>
 <p> In the next task, you can use your experience from this task, to find out the angles without sliders.
    
    <p>
        <button type="button" onclick="hide('task2a');show('task2b');">Continue</button>
    </p>correct.<br></p>
```   
  
#### Node 3 false feedback 
```<p> The value you gave for angle \(\beta\) is also not yet correct. The correct value is {@gammar@}. Make sure the curves overlap perfectly using the sliders. This might take a bit of patience.</p>
<br>
<p> In the next task, you can use your experience from this task, to find out the angles without sliders.
    
    <p>
        <button type="button" onclick="hide('task2a');show('task2b');">Continue</button>
    </p>
```
| ![Node 3](https://private-user-images.githubusercontent.com/120648145/240387873-425b5449-4f06-450e-b970-c7bc11d59218.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3NDEzLCJuYmYiOjE2ODQ4NjcxMTMsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4Nzg3My00MjViNTQ0OS00ZjA2LTQ1MGUtYjk3MC1jN2JjMTFkNTkyMTgucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTgzODMzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YTdiZGYyZjYxNmNkYTYxNjc3ZmQwMDY0ODA5Yjc1NjMwYzY0ZmJlZTdlMmU1ZTQ3YWM3NGMxN2NhZDdmY2FlMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.CgDBchPpzhCiLwvg_ObZTNg4vv72HCHuvCmEJ28ndN8) |
|:--:|
| *Node 3* |

# Task 2b: Rotation about two known axis with unknown angles

| ![First impression](https://private-user-images.githubusercontent.com/120648145/240389050-1397cd94-442c-4f3e-88cf-2a9dfd3565bb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3Nzg3LCJuYmYiOjE2ODQ4Njc0ODcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTA1MC0xMzk3Y2Q5NC00NDJjLTRmM2UtODhjZi0yYTlkZmQzNTY1YmIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NDQ3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MzFmYzIxYTMwYjFjZGY4ZDg1OWNkOWJiMTdiYjQ2YmRhMWU2YzlhODg0ZjA1ZWUxODBkNDkzMjE5ZWY1YTI1NyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.qT7x6oQ-sMDhetLZuAwhY9h8-Bed1wM1Xfygpn0XwQI) |
|:--:|
| *First impression of the question* |


## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
```math
t \mapsto \begin{pmatrix} 
r \cdot \cos (t) \\
r \cdot \sin (t) \\
0
\end{pmatrix}.
```
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about two coordinate axis. The student is provided with the coordinate axis and the order of operation.
They need to find out, what the angles of rotation are.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with two curves that can be changed into one another by rotation about two coordinate axis. They are asked to find the correct rotational angles. They give their answer in an algebraic manner.
| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240389151-af8e9346-8b49-4680-b15d-f706dac71df0.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3Nzg3LCJuYmYiOjE2ODQ4Njc0ODcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTE1MS1hZjhlOTM0Ni04YjQ5LTQ2ODAtYjE1ZC1mNzA2ZGFjNzFkZjAucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NDQ3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MDFmYTUzZDc3MWY4YTk2NWYxMDZjMmE0MDMxZGMxODUxNzRmZGE4N2U4ZTdkNTU2MTk4YzcwMDUwZDAzYTU4YiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.nyA5SKOb4vPjXyFrTXu4bUriXNXT1c4CO3LhgOGAOxM) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for the angle of rotation. They can add a new variable for the angle in the same manner the other angles are randomized. Otherwise, they can change the list of possible values for the variables `alphar` and `gammar` used in this task.  In order to do this, they simply need to modify the entries in the list specified e.g. change `alphar : rand([1/6,1/4,1/3,1/2,2/3,3/4])*%pi;` to `alphar: rand([3/4,5/4,4/3])*%pi;`. 

For an explanation of the processing of the values read **Question variables** and **Question text**.


### Question variables used

+ `alphar` and `gammar` are the same variables used in the initial task
+ the matrix `M1` and `M3` are used for the matrix product
+ the results are evaluated for the angle and saved to the variable `tro_matres`
+ the matrix is converted to a list `tro_res` in order to export the results to JSXGraph



### Question Text
+ Task explanation using LaTex, importing the random values from **Question variables**
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans5]]`, `[[input:ans6]]` at the end of JSXGraph code to allow input of  angles
+	`[[validation:ans5]]`, `[[validation:ans6]]` is used for checking of answer


## Answers
### Answer ans 5
|property | setting| 
|:---|:---|
|Input type | Algebraic Input|
|Model answer | `alphar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
### Answer ans 6
|property | setting| 
|:---|:---|
|Input type | Algebraic Input|
|Model answer | `gammar` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---
## Potential response tree

### prt4

Feedback variables:
```
ans5;
ans6;
```

| ![prt4](https://private-user-images.githubusercontent.com/120648145/240389593-899863be-3203-4361-8733-914f5dd66f15.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3ODg5LCJuYmYiOjE2ODQ4Njc1ODksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTU5My04OTk4NjNiZS0zMjAzLTQzNjEtODczMy05MTRmNWRkNjZmMTUucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NjI5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9Y2JlMzUxZjZiYWUyNTcyYWNlNDMwZWM2NWFhOTJjZTg2NDNjYjBjMWM4Njk2ZDNjMzIwOGE3OWJkYjdjMjJlYyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.jn_F8Y4oYvJ7IVE-SQgLgKx5YvcM01N10h86pYM3XIc) |
|:--:|
| *Visualization of **prt4*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `ans5`|
|TAns | `gammar`| 
|Node 1 true feedback |  `<p> Nice! You found the correct angle \(\alpha\). Good job! </p>`|
|Node 1 false feedback | `<p> The value you gave for angle \(\alpha\) is not yet correct. The correct value is {@gammar@}. </p>`|


| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240389596-1fac0ac0-81c2-4721-9a2e-fd3a0b3dc6d2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3ODg5LCJuYmYiOjE2ODQ4Njc1ODksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTU5Ni0xZmFjMGFjMC04MWMyLTQ3MjEtOWEyZS1mZDNhMGIzZGM2ZDIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NjI5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZDllMzk2MzkwMWE4YjJiNjczZjBiZTk0YjU2Yjc3OWM5MTA5MjFlNGRmMTI5NzAwOTkwYTljN2QzOWVlYzRhOCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.QDYzso4I4_MtMkSGE46gwIK-ZkvKI9_GIPQIJ8RCZPM) |
|:--:|
| *Node 1* |



### Node 2
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `ans6`|
|TAns | `alphar`| 

#### Node 2 true feedback 
```<p> Nice! You also found the correct angle \(\beta\). Good job! </p> <p> Perfect! You got both angles right! </p>
<br>

<p> Now that you have a feel for the angles, let's look at the dependance of the result on the order of operations.
    <p>
        <button type="button" onclick="hide('task2b');show('task3');">Continue</button>
    </p>
```   
  
#### Node 2 false feedback 
```<p> The value you gave for angle \(\beta\) is not yet correct. The correct value is {@alphar@}.</p>
<br> In the following applet, you can see, how your answer would have looked. The blue and orange curves are the way they were presented before. Your solution is displayed in purple. </p>
```
+ JSXGraph Applet

| ![Node 2](https://private-user-images.githubusercontent.com/120648145/240389597-1eb312e8-a853-4b4f-8736-c3892009eb77.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3ODg5LCJuYmYiOjE2ODQ4Njc1ODksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTU5Ny0xZWIzMTJlOC1hODUzLTRiNGYtODczNi1jMzg5MjAwOWViNzcucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NjI5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NGNhM2M0Y2I4ZTNiMDY5NDNiN2MwNzFlMTQxNzEyYjA5NTU4ZTczYzQ5ODgxMjlhYTE1ZmU1OGY1ZDE1N2ZkOSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.vNqoTEyoVdCSdbrrpwHGllF2rYULWBzIg5-aU6ITtIw) |
|:--:|
| *Node 2* |

### Node 3
|property | setting| 
|:---|:---|
|Answer Test | AlgEquiv|
|SAns | `ans6`|
|TAns | `alphar`| 

#### Node 3 true feedback 
```<<p> Nice! You found the correct angle \(\beta\). Good job! Check, whether you did anything differently for \(\alpha\). </p>
<br> In the following applet, you can see, how your answer would have looked. The blue and orange curves are the way they were presented before. Your solution is displayed in purple. </p>
```   
+ JSXGraph Applet
  
#### Node 3 false feedback 
```<p> The value you gave for angle \(\beta\) is also not yet correct. The correct value is {@alphar@}. </p>
<br> In the following applet, you can see, how your answer would have looked. The blue and orange curves are the way they were presented before. Your solution is displayed in purple. </p>
```
| ![Node 3]https://private-user-images.githubusercontent.com/120648145/240389599-d13e8740-bcf3-4a80-a72f-26677c15d704.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3ODg5LCJuYmYiOjE2ODQ4Njc1ODksInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTU5OS1kMTNlODc0MC1iY2YzLTRhODAtYTcyZi0yNjY3N2MxNWQ3MDQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NjI5WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YjE2ZWI2OTFhZjNmZjA3YmZlZDAwYzgwNTMzMWFjZGE5NWI5NTA0ZTlmY2UwYmY0ZjIzMDFjM2JlMzI0MzljOSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.HjuQ3TmrEz8yR5FxdhsxIC5u18JXj-0g2AXr5fHatN0) |
|:--:|
| *Node 3* |


Here, the student's answer is evaluated as a rotated curve and plotted for them to compare it to the correct answer.

| ![Feedback](https://private-user-images.githubusercontent.com/120648145/240389242-121cd75b-8dc9-4718-a5c6-7d285d39fea3.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY3Nzg3LCJuYmYiOjE2ODQ4Njc0ODcsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM4OTI0Mi0xMjFjZDc1Yi04ZGM5LTQ3MTgtYTVjNi03ZDI4NWQzOWZlYTMucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg0NDQ3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NmFhNGNjZDMyZmRjMzYzZjdmNWVhOWQ4YjFlYmY0MDdkNGQwZjk4MDY0NmMzYTI1MDYzYWEzZjJiNWJlNTQ1MiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.VvY-6XpyPekO3k3bBryAdCmw9mUmW1SH5PBSVT5IdTg) |
|:--:|
| *Feedback upon incorrect answer * |


# Task 3: Rotation of a curve about two known axis in unknown order


| ![First impression](https://private-user-images.githubusercontent.com/120648145/240390451-45356907-cd71-4d20-9ccc-e962cecd4cc0.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY4MTQyLCJuYmYiOjE2ODQ4Njc4NDIsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM5MDQ1MS00NTM1NjkwNy1jZDcxLTRkMjAtOWNjYy1lOTYyY2VjZDRjYzAucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg1MDQyWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NzMyNmQ3NmNkZWMwZGJhOWJiYTczZDZjMTI3ZDNjMTQ3NDdkYzNiOGJjYmI3YWEyNjMxY2I5NmZiZGViODIzNyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.QuL4Puc8-DA8gS_qYIKNrIcsgQgW_ArmcIptw9xjiTg) |
|:--:|
| *First impression of the question* |


## Question description

A 3D curve is plotted. It is a half circle so its orientation changes visibly after rotational matrices are applied. The curve can be parametrized as
```math
t \mapsto \begin{pmatrix} 
r \cdot \cos (t) \\
r \cdot \sin (t) \\
0
\end{pmatrix}.
```
A second curve of the same shape is plotted. Its orientation is different from the first curve. It has been rotated about two different coordinate axis. The student is provided the concrete angles of rotation for rotations about each of the coordinate axis and the two axis used.
They need to find out, in which order the rotations where executed.


### Student perspective

The student sees a cartesian coordinate system and a curve plotted in 3D.

They are presented with angles of rotation for each of the coordinate axis. They are asked to select the correct order of operations from a multiple choice selection.

| ![Click draw button](https://private-user-images.githubusercontent.com/120648145/240390458-324d731c-3b73-40d6-8402-5c8720412594.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY4MTQyLCJuYmYiOjE2ODQ4Njc4NDIsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM5MDQ1OC0zMjRkNzMxYy0zYjczLTQwZDYtODQwMi01Yzg3MjA0MTI1OTQucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg1MDQyWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MDQxOTkxNTllMDIzMjM3MDRmZGExZDc2Y2Q0ZDc2YWI0MDc0ZTk0NzgzN2M5ODgzZTY2OWVjMzcwMDIzOTA1ZSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.5frJZdFhLl-cvzfFmYWStVMzFyqKv9Ng7TIYeS4EoWs) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for angles of rotation. In order to do this, they simply need to modify the entries in the lists specified e.g. change `alphar : rand([1,2,3,4,5,6])/4*%pi;` to `phaser : rand([1/4,1/3,1/2,2/3])*%pi;`. 

For an explanation of the processing of the values read **Question variables** and **Question text**.


### Question variables used

+ the possible answers are saved to list `ap_ta` along with the information whether the answer is correct to allow for the radiobuttons (multiple choice) format
+ one possibility is randomly selected and assigned the bool `true` - this is the correct answer
+ `alphar`, `ap_betar` are randomly selected rational multiples of $\pi$ created using `rand()`, division and multiplication
+ the matrices `M2` and `M3` are the possible matrices 
+ `ap_in` is a random value for the election of the order of operations
+ the matrices `ap_M1r` and `ap_M2r` are a random tuple of the possible matrices, where no duplicates are allowed 
+ the results are evaluated for the angles and saved to the variable `ap_matres`
+ the matrix is converted to a list `ap_res` in order to export the results to JSXGraph



### Question Text
+ Task explanation using LaTex, importing the random values from **Question variables**
+	JSXGraph applet using and variables defined in **Question variables** plotting the 3D curve
+	`[[input:ans7]]` at the end of JSXGraph code to allow input of  answers of the student for the order of operations
+	`[[validation:ans7]]`is used for checking of answer


## Answers
### Answer ans 7
|property | setting| 
|:---|:---|
|Input type | Radiobuttons|
|Model answer | `ap_ta` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | No |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---

## Potential response tree
### prt5

In the following, the feedback variables are given. Here, the student answer is processed to be able to show them how their incorrect answer would look like. That way, they can compare their result to the correct solution and reflect on their train of thought leading up to the error.

+ `ap_checker` specifies what to look for in the list `ap_ta`, namely the student's answer `ans7`
+ in the list, the position of `ans7` is saved as the variable `ap_location`
+ from that, the corresponding matrices `ap_M1s` and `ap_M2s`can be found to depict the student's answer
+ the curve is calculated and exported like the reference solution and can later be displayed using JSXGraph

Feedback variables:
```
ans7;

ap_checker: ans7;
for i:1 thru length(ap_ta) step 1 do(if member(ap_checker, [ap_ta[i][1]]) then ap_location:i);
ap_location;

ap_M1s: ap_matlist[ap_location][1];
ap_M2s: ap_matlist[ap_location][2];

/* calculate matrix product and evalutate angles */
ap_studentmatres: ev(ap_M2s.ap_M1s.v,  b:alphar, c: ap_betar);

/* turn matrix to list for export*/
ap_studentres: [mattolist(ap_studentmatres)[1][1],mattolist(ap_studentmatres)[2][1],mattolist(ap_studentmatres)[3][1]];

```

| ![prt5](https://private-user-images.githubusercontent.com/120648145/240390751-3cbfd2ea-0c7b-4fad-ad06-78b2c30b9bc2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY4MjMxLCJuYmYiOjE2ODQ4Njc5MzEsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM5MDc1MS0zY2JmZDJlYS0wYzdiLTRmYWQtYWQwNi03OGIyYzMwYjliYzIucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg1MjExWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YjJmZjk4M2YwN2E4MTM2ZGNmZjcwNzEzNWEyMmU4OGRiMzUyYjY0M2UwY2QwOGEzZWJjYjFhNDFmNjBlMjQ2MCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.9DVt8IshZQ_YR1rJhHiQgrAoqYgeZ3OqW2VW2eB1Kds) |
|:--:|
| *Visualization of **prt5*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | String|
|SAns | `ans7`|
|TAns | `ap_tans[1]`| 
#### Node 1 true feedback 
```
<p> Well done! You got the order of operations right! </p>
<br>
<p> You are now presented with the same task as in the beginning. Good luck trying it again!
  <p>
        <button type="button" onclick="hide('task3');show('taskagain');">Continue</button>
    </p>`|
```

#### Node 1 false feedback:
```
<p> Unfortunately, this is not the correct order of operations.  A correct answer is {@ap_tans[1]@}. </p><br>
<br> In the following applet, you can see, how your answer would have looked like with the angles provided. The blue and orange curves are the way they were presented before. Your solution is displayed in purple. </p>
```
| ![Node 1](https://private-user-images.githubusercontent.com/120648145/240390743-c5b7954f-e80d-47a8-b613-a6e40a87f578.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY4MjMxLCJuYmYiOjE2ODQ4Njc5MzEsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM5MDc0My1jNWI3OTU0Zi1lODBkLTQ3YTgtYjYxMy1hNmU0MGE4N2Y1NzgucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg1MjExWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YzUzNDIwMTNiNWE4OTBhYTI1NDYyZWNlYjNiMDlhZDFjMThhNDMyMzk2ZTFlYWNjNzVhYTAwOGI2ZGI3NDNlNCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.nEUMHCDqwm6gs_6UnfHjYsRghIMvK106ztaiCggh3XY) |
|:--:|
| *Node 1* |


Here, the student's answer is evaluated as a rotated curve and plotted for them to compare it to the correct answer.



| ![Feedback](https://private-user-images.githubusercontent.com/120648145/240390456-dc20c28d-8235-4d16-ae36-2d9f763f743b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg0ODY4MTQyLCJuYmYiOjE2ODQ4Njc4NDIsInBhdGgiOiIvMTIwNjQ4MTQ1LzI0MDM5MDQ1Ni1kYzIwYzI4ZC04MjM1LTRkMTYtYWUzNi0yZDlmNzYzZjc0M2IucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMDUyMyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzA1MjNUMTg1MDQyWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9ZWUzYWNiMTVkOTRlZGZhMjU3YzRmODgzYmM2NTFkZTZjOTc1YjA5Y2ViMTgzMWM1MjVjOTZjODZjYzljNTRiMCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.zE0TiTA7SDNQPElNLBjOudcBAY3LuJtcuLyiNftDZKk) |
|:--:|
| *Feedback upon incorrect answer * |

# Repetition of initial task

Analogous to the initial task, it is presented again. This time, some of the variables are named slightly different to prevent ambiguities in the code. The answer is `ans8`.
Another JSXGrap applet is presented upon answering incorrectly.


## Todo:
* [] Update figures

