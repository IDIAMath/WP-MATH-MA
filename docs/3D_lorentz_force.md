---
title: Lorentz force
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

The Lorentz-force $\vec{F}_L$ acts on moving charges in a magnetic field. The force is maximal, when the particle moves in a plane perpendicular to the magnetic field. It can be expressed as a vector product:
```math
\vec{F}_L = q\vec{v} \times \vec{B} 
```
In a homogeneous magnetic field, the force acts as a centripetal force, since it is always directed perpendicular to the component of $\vec{v}$ in the plane normal to $\vec{B}$. Hence the charge carrier with a charge $q$ is accelerated perpendicular to this velocity component. The result is a circular motion in the special case or a spiraling motion in the more general case.

The trajectory can be obtained by solving a differential equation. One solution for the trajectory is
```math
\vec{r}(t)= \vec{r_0}+ \begin{pmatrix}r\cdot \cos(\omega(t-t_0))\\ r\cdot \sin(\omega(t-t_0)) \\ v_z\cdot t \end{pmatrix} - \begin{pmatrix}r\cdot \cos(\omega(t_0))\\ -r\cdot \sin(\omega(t_0)) \\ 0 \end{pmatrix}
```
Here, $r_0$ is the starting point of the particle. $\omega = \frac{qB}{m}$ is the angular frequency given by the charge $q$, absolute value of the magnetic field density $B$ and mass $m$. $r$ is the radius of the helix given by $r= \frac{m(v_x^2+v_y^2)^{1/2}}{qB}$. Lastly $t_0$ is a phase shift that may take different values depending on the case. It can take the values $t_{0x}= -\frac{\arcsin(\frac{v_x}{-r\omega})}{\omega}$ or $t_{0y}= \frac{\arccos(\frac{v_x}{r\omega})}{\omega}$.


### Student perspective

The student sees a cartesian coordinate system, a 3D vector field and a single vector in 3D.

It is the task to qualitatively predict the curve followed by the particle given by the acting lorentz force. In order to do this they have to take into account the charge, initial velocity and magnetic field given in the introduction.

The answer is given in multiple choice format.

| ![Click draw button](https://user-images.githubusercontent.com/120648145/213679631-30d42545-5805-4ed7-8ec7-5ab5812c95ef.png) |
|:--:|
| *When the student solves the problem* |


### Teacher perspective
The teacher is able to give a list of possible values for parameters. In order to do this, they simply need to modify the entries in the lists specified e.g. change `r0:  rand([[0, 1, 1], [-2, 0 ,-1], [1, 2, -1], [1, -1, 1]]);` to `r0:  rand([[0, 1, 0], [2, 0 ,-1], [1, 0, -1], [1, 1, 1]]);`. 
They can also change the values the velocity components are randomly selected from by changing `v: [rand([-0,-1,-2,1,2]),rand([-0,-1,-2,1,2]),rand([-1,-0.5,0,0.5,1])];` to desirded values in each component.

Lastly, they can change the absolute value of the magnetic field to values they desire.

<b> Note, that it is currently only supported to have the magnetic field be homogeneous and oriented along the $z$-axis. If you want to have a different direction, there will have to be a lot of changes made to the task!</b>

For an explanation of the processing of the values read **Question variables** and **Question text**.


| ![values the teacher can change](https://user-images.githubusercontent.com/120648145/213679633-b475a068-2a0f-4882-9bd0-001c98901157.png) |
|:--:|
| *The above image shows which values the teacher may wish to change* |


## Question code

### Question Variables
+  `r0` and `v` are randomly selected lists created using `rand()` representing the initial values of the problem
+  `B0` and `q` are randomly selected integer numbers created using `rand()` representing the absolute value of the magnetic field density and the charge of the particle
+ `v_normr` is the absolute value of the initial velocity `v`
+ `v_norm` is the numerical value of `v_normr` used to plot the curve
+ `mag_list` contains possible magnetic field constellations - currently there is only one supported
+ `mag` is the selected magnetic field from `mag_list` and multiplied by `B0`
+ `mag_normr` is the absolute value of processed `mag`
+ `mag_norm` is the numerical value of `mag_normr`
+ `v_orth_list` contains the value of the velocity orthogonal to the magnetic field, based on the entries in `mag_list`
+ `v_orthr` is the value taken from `v_orth_list`
+ `v_orth` is the numerical value of `v_orthr` 
+ `ta` is a list containing possible answers to the multiple choice question. Each answer is given alongside a boolean that specidifes whether it is true or false
+ The individual cases are distinguished and the correct answer is marked true



#### Question variable code
```
r0:  rand([[0, 1, 1], [-2, 0 ,-1], [1, 2, -1], [1, -1, 1]]);
v: [rand([-0,-1,-2,1,2]),rand([-0,-1,-2,1,2]),rand([-1,-0.5,0,0.5,1])];
v_normr: (v[1]**2+v[2]**2+v[3]**2)**(1/2);
mag_list: [[0, 0, 1]];
v_orth_list: [(v[1]**2+v[2]**2)**(1/2)];
index: 1;
mag: mag_list[index] ;
B0: rand([0.5,1,1.5,2]);
mag: B0*mag;
mag_normr: (mag[1]**2+mag[2]**2+mag[3]**2)**(1/2);
v_orthr: v_orth_list[index];
q: rand([-3,-2,-1,1,2,3]);
m: 1;


v_orth: v_orthr,numer;
v_norm: v_normr, numer;
mag_norm: mag_normr, numer;
ta: [["Straight line going along direction of v",false],["Straight line going along direction of B",false],["Straight line going in another direction",false],["Circular motion with clockwise direction",false],["Circular motion with counter-clockwise direction",false],["Spiralling up in clockwise direction",false],["Spiralling up in counter-clockwise direction",false],["Spiralling down in clockwise direction",false],["Spiralling down in counter-clockwise direction",false], ["Parabolic motion in direction of B",false], ["Parabolic motion in direction opposed to B", false]]

if v[3]=0 and sign(q)#sign(mag[3]) then ta[5][2]:true;
if v[3]=0 and sign(q)=sign(mag[3]) then ta[4][2]:true;
if v_orth = 0 and sign(v[3])=sign(mag[3]) then block(ta[1][2]:true, ta[2][2]:true);
if v_orth = 0 and sign(v[3])#sign(mag[3]) then ta[1][2]:true;
if v[3]>0 and sign(q)#sign(mag[3]) then ta[7][2]:true;
if v[3]>0 and sign(q)=sign(mag[3]) then ta[6][2]:true;
if v[3]<0 and sign(q)#sign(mag[3]) then ta[9][2]:true;
if v[3]<0 and sign(q)=sign(mag[3]) then ta[8][2]:true;

```

### Question Text
+	"Given is a charge particle of charge $q=$ {@q@} starting at location $\vec{r}_0=${@r0@} with a velocity vector of $\vec{v}=$ {@v@}. It is moving in a constant magnetic field $\vec{B}=${@mag@}. The Lorentz force will act on the particle following the equation $\vec{F} = q\cdot \vec{v}\times \vec{B}$.
 What will the trajectory of the particle look like qualitatively from the starting perspective? 
”
+ Task explanation using LaTex
+	JSXGraph applet using and variables defined in **Question variables** plotting the vector field and vector
+	`[[input:ans1]]` at the end of JSXGraph code to allow input of  answers of the student
+	`[[validation:ans1]]` are used for checking of answer

#### Question text code


```javascript
<p>Given is a charge particle of charge \(q=\) {#q#} starting at location \(\vec{r}_0=\){@r0@} with a velocity vector of \(\vec{v}=\) {@v@}. It is moving in a constant magnetic field \(\vec{B}=\){@mag@}. The Lorentz force will act on the particle following the equation \(\vec{F} = q\cdot \vec{v}\times \vec{B}\).</p>
<p> What will the trajectory of the particle look like qualitatively from the starting perspective?</p>

[[jsxgraph width="500px" height="500px"]]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

            var box = [-5,5];
            var view = board.create('view3d',
		        [[-6, -3], [8, 8],
		        [box, box, box]],
		        {});

			//curve from STACK values
			var r1 = {#r0[1]#};
            var r2 = {#r0[2]#};
            var r3 = {#r0[3]#};
            var v1 = {#v[1]#};
            var v2 = {#v[2]#};
            var v3 = {#v[3]#};
            var v_norm = {#v_norm#};
            var mag_norm = {#mag_norm#};  
            var v_orth = {#v_orth#};
			var m = {#m#};
            var q = {#q#};
			var r = m*v_orth/(q*mag_norm);
            var omega = q*mag_norm/m;
            var t0x = -Math.asin(v1/(-r*omega))/omega;
            var t0y =  Math.acos(v2/(r*omega))/omega;
                        
                         
            var v_vec = view.create('line3d', [[r1,r2,r3],[r1+v1,r2+v2,r3+v3]], {point1: {visible: true, size: 1, color: "#1f84bc",strokeColor: '#EE442F', withLabel: false},lastArrow: true,strokeColor: "#1f84bc", strokeWidth: 3});  
			 
			/*plotting vector field */
			
			var TF1 = board.jc.snippet('0', true, 'x,y,z');
			var TF2 = board.jc.snippet('0', true, 'x,y,z');
			var TF3 = board.jc.snippet('z*0+2', true, 'x,y,z');    
 
			var vector=[];
			var scaleVec = 0.5;

			
			function clearVectorField(){
   				board.removeObject(vector);
    			vector=[];
				}

			function vectorField(){
   				clearVectorField();
   				board.suspendUpdate();
    			var i,j,k,vx,vy;
   				var pout=[];
    			for(k=-5; k<6; k+=2){
        			for(i=-5; i<6; i+=2){
            			for(j=-5;j<6; j+=2){   
                            var norm =1;
                 			vector.push(view.create('line3d',[[i, j,k ],
                            [TF1(i,j,k),TF2(i,j,k),TF3(i,j,k)],[0,scaleVec]],
                            {point: { withLabel: false},
                            point1: {visible: false, size: 1, color: '#EE442F',strokeColor: '#EE442F', withLabel: false},
                            point2: {visible: false, withLabel: false},
                            lastArrow:true, fixed: true, strokeColor:'#EE442F', highlight:false})
                            );

            				}
        				}
    				}
				board.unsuspendUpdate();
				}
				/* end helper functions */
				vectorField();

				board.update(); 	
                        
				/* axis labels*/
                var xlabel=view.create('point3d',[0.9*box[1],0,(0.6*box[0]+0.4*box[1])], {size:0,name:"x"});
                var ylabel=view.create('point3d',[0,0.9*box[1],(0.6*box[0]+0.4*box[1])], {size:0,name:"y"});
                var zlabel=view.create('point3d',[
                    0.7*(0.6*box[0]+0.4*box[1]),
                    0.7*(0.6*box[0]+0.4*box[1]),
                    0.9*box[1]], 
                    {size:0,name:"z"});


[[/ jsxgraph]]<p>[[input:ans1]] [[validation:ans1]]</p>


```
## Answers
### Answer ans 1
|property | setting| 
|:---|:---|
|Input type | Radio|
|Model answer | `ta` defined in **Question variables** |
| Forbidden words | none |
| Forbid float | Yes |
| Student must verify | Yes |
| Show the validation | Yes, with variable list|
---

## Potential response tree
### prt1

Feedback variables:
```
checker: true;
for i:1 thru length(ta) step 1 do(if member(checker, [ta[i][2]]) then location:i);
location;
tans: ta[location];
```

| ![prt1](https://user-images.githubusercontent.com/120648145/213417669-8735a0da-5074-4b7c-9870-8b287ab42be6.png) |
|:--:|
| *Visualization of **prt1*** |



### Node 1
|property | setting| 
|:---|:---|
|Answer Test | String|
|SAns | `ans1`|
|TAns | `tans[1]`| 
|Node 1 true feedback | `<p> Well done! You got the type of trajectory right! Will you dare to try again for a different set of starting parameters?</p>`|
|Node 1 false feedback |`<p> Unfortunately, this is not the correct type of trajectory.<br> Remember to use the right hand rule for a cross product!<br> Also, due to the properties of the vector product, the velocity component parallel to the magnetic field does not contribute to the Lorentz force. Hence there is no acceleration along the \(z\)-axis.</p>`|


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

## General Feedback code

Have a look at the correct trajectory and compare it to your answer.
```javascript
[[jsxgraph width="500px" height="500px"]]
var board = JXG.JSXGraph.initBoard(divid,{boundingbox : [-10, 10, 10,-10], axis:false, shownavigation : false});

            var box = [-5,5];
            var view = board.create('view3d',
		        [[-6, -3], [8, 8],
		        [box, box, box]],
		        {});

			//curve from STACK values
			var r1 = {#r0[1]#};
            var r2 = {#r0[2]#};
            var r3 = {#r0[3]#};
            var v1 = {#v[1]#};
            var v2 = {#v[2]#};
            var v3 = {#v[3]#};
            var v_norm = {#v_norm#};
            var mag_norm = {#mag_norm#};  
            var v_orth = {#v_orth#};
			var m = {#m#};
            var q = {#q#};
			var r = m*v_orth/(q*mag_norm);
            var omega = q*mag_norm/m;
            var t0x = -Math.asin(v1/(-r*omega))/omega;
            var t0y =  Math.acos(v2/(r*omega))/omega;
                        
                         
            var v_vec = view.create('line3d', [[r1,r2,r3],[r1+v1,r2+v2,r3+v3]], {point1: {visible: true, size: 1, color: "#1f84bc",strokeColor: '#EE442F', withLabel: false},lastArrow: true,strokeColor: "#1f84bc", strokeWidth: 3});  
			
			/*curve from STACK values*/
			 
			 
			if (v_orth>0) {
				if (v1>=0 && v2>=0){  
					var c_base = view.create('curve3d', [   
					(t)=> r1- r*Math.cos(omega*(t+t0x))+ r*Math.cos(omega*t0x),   
					(t)=> r2+ r*Math.sin(omega*(t+t0y))- r*Math.sin(omega*t0y),     
					(t)=> r3+ v3*t,  
					[0, 7]], {strokeWidth: 2, strokeColor: "#1f84bc"}); 
				}
				else if (v1<=0 && v2<=0){ 
					var c_base = view.create('curve3d', [ 
					(t)=> r1+ r*Math.cos(omega*(t-t0x))-  r*Math.cos(omega*t0x),   
					(t)=> r2+ r*Math.sin(omega*(t-t0y))+ r*Math.sin(omega*t0y),      
					(t)=> r3+ v3*t, 
					[0, 7]], {strokeWidth: 2, strokeColor: "#1f84bc"}); 
				}
				else  {
					if (Math.sign(v1)==-1){
					var c_base = view.create('curve3d', [ 
					(t)=> r1- r*Math.cos(omega*(t-t0y))+ r*Math.cos(omega*t0x),     
					(t)=> r2+ r*Math.sin(omega*(t-t0y))- r*Math.sin(omega*t0x),         
					(t)=> r3+ v3*t,    
					[0, 7]], {strokeWidth: 2, strokeColor: "#1f84bc"});    
					}
					
					else if  (Math.sign(v1)==1){
					var c_base = view.create('curve3d', [ 
					(t)=> r1+ r*Math.cos(omega*(t-t0x))+ r*Math.cos(omega*t0y),    
					(t)=> r2- r*Math.sin(omega*(t-t0x))- r*Math.sin(omega*t0y),     
					(t)=> r3+ v3*t,    
					[0,7]], {strokeWidth: 2, strokeColor: "#1f84bc"});   
					} 
					}}
			else {
				var c_base = view.create('curve3d', [
					 
					(t)=> r1,  
					(t)=> r2,  
					(t)=> r3+ v3*t, 
					[0, 7]], {strokeWidth: 2, strokeColor: "#1f84bc"}); 
			}


			/*plotting vector field */
			
			var TF1 = board.jc.snippet('0', true, 'x,y,z');
			var TF2 = board.jc.snippet('0', true, 'x,y,z');
			var TF3 = board.jc.snippet('z*0+2', true, 'x,y,z');    
 
			var vector=[];
			var scaleVec = 0.5;

			
			function clearVectorField(){
   				board.removeObject(vector);
    			vector=[];
				}

			function vectorField(){
   				clearVectorField();
   				board.suspendUpdate();
    			var i,j,k,vx,vy;
   				var pout=[];
    			for(k=-5; k<6; k+=2){
        			for(i=-5; i<6; i+=2){
            			for(j=-5;j<6; j+=2){   
                            var norm =1;
                 			vector.push(view.create('line3d',[[i, j,k ],
                            [TF1(i,j,k),TF2(i,j,k),TF3(i,j,k)],[0,scaleVec]],
                            {point: { withLabel: false},
                            point1: {visible: false, size: 1, color: '#EE442F',strokeColor: '#EE442F', withLabel: false},
                            point2: {visible: false, withLabel: false},
                            lastArrow:true, fixed: true, strokeColor:'#EE442F', highlight:false})
                            );

            				}
        				}
    				}
				board.unsuspendUpdate();
				}
			/* end helper functions */
			vectorField();

			board.update(); 	
                        
			/* axis labels*/
            var xlabel=view.create('point3d',[0.9*box[1],0,(0.6*box[0]+0.4*box[1])], {size:0,name:"x"});
            var ylabel=view.create('point3d',[0,0.9*box[1],(0.6*box[0]+0.4*box[1])], {size:0,name:"y"});
            var zlabel=view.create('point3d',[
                0.7*(0.6*box[0]+0.4*box[1]),
                0.7*(0.6*box[0]+0.4*box[1]),
                0.9*box[1]], 
                {size:0,name:"z"});


[[/ jsxgraph]]

```
## Todo:
