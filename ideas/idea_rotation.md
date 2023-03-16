# Rotation matrices, order of operations and rotation angles

## Idea

Rotation of mathematical objects is usually introduced with rotational matrices. While the calculation is realatively straight-forward matrix algebra, an inuition is often not developed. This leads to misconceptions, when programming e.g. robotics applications or 3D visualizations.

The aim of this document is to present a possible succession of tasks using Moodle-STACK-exercises to visualize rotating systems and give an intuition for the topic.

## Aim

A possible final task would be the following:
A known object is plottet in a rotated manner (say, it has been rotated about 2 axis). The student knows the axis of rotation. They are then asked, in which order the rotation has been performed. Mathematically speaking, they need to reconstruct in which way the matrix product has been performed. Additionally they shall give the angles of rotation.

## Task components

### <b> Input: Introduction of rotational  matrices </b>

In a 3D vector-space with euklidian base, one can easily define 3 rotations $R_x ,R_y, R_z$ about the axis.

$$
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
\end{pmatrix} 
$$

A rotation of angle $\alpha$ is performed by multiplying a vector with the correspondend rotational matrix. 

### <b>Task 1: Rotation of a curve about 1 axis </b>

That way, if a curve's parametrization is given as a vector it can easily be rotated by multiplication of the rotational matrix and the vector.

The students are presented a curve, a direction of rotation and can find out the angle of rotation using a JSXGraph applet.

| ![Task 1](https://user-images.githubusercontent.com/120648145/225601390-9ba1d10e-0808-4ebf-b5a3-2f4de8c6b9fa.jpg) |
|:--:|
| *Task 1* |

### <b>Input: Rotations about multiple axis </b>

If a rotation is performed about multiple, say 2 axis, the corresponding rotational axis are multiplied. However, since matrix multiplication is not commutative, the order of execution matters.

For example, for a rotation about the $x$-axis with an angle of $\alpha=60^\circ$ and a rotation about the $y$-axis with an angle of $\beta=45^\circ$, we get the following results

$$R_x(60^\circ) \cdot R_y(45^\circ) =
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
$$

and with the switched order of operation

$$R_y(45^\circ) \cdot R_x(60^\circ) =
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
$$


Therefore, the resulting vector will be different.
### <b>Task 2.1: Rotation of a curve about 2 known axis </b>
The students are presented a curve rotated about two axis.
They are provided with the axis and the rotational matrices, as well as the matrix product used. Hence they already know the order of operations.

They need to find out the angle of rotation in both axis with the help of a slider in a JSXGraph applet.

| ![Task 2.1](https://user-images.githubusercontent.com/120648145/225601393-3ad6120b-d93d-436d-a855-1e4c7dd7bc5b.jpg) |
|:--:|
| *Task 2.1* |

### <b>Task 2.2: Rotation of a curve about 2 known axis </b>
The students are presented a curve rotated about two axis.
They are provided with the axis and the rotational matrices, as well as the matrix product used. Hence they already know the order of operations.

They need to find out the angle of rotation in both axis <b>without </b> the help of the slider previously used. That way, they have to actively think about the angles and order of execution.

| ![Task 2.2](https://user-images.githubusercontent.com/120648145/225601396-97e4d0b6-5d6f-4cb8-a7a1-20503e2a570e.jpg) |
|:--:|
| *Task 2.2* |

### <b> Input: Two ways of rotating a curve about two axis</b>

The students are presented two JSXGraph applets of a curve rotated about two axis. The rotation angles can be manipulated with sliders. They only differ in order of execution in the multiplication of the rotational matrices.

### <b> Task 3:  Rotation of a curve about 2 known axis in unknown order</b>
The students are presented a curve rotated about two axis.
They are provided with the axis and the rotational matrices, as well as the angles used. 

They need to find out the order of operations. They give their answer in a multiple choice mode.



### <b>Task 3 Feedback idea </b>

If the students pick the wrong order of execution, they are presented with another applet.
There, they see the same curve as before and can manipulate another curve with sliders. This second curve, however is determined by the wrong matrix multiplication. That way they can see, that the curves cannot line up in the intended way.

| ![Task 3 feedback](https://user-images.githubusercontent.com/120648145/225601384-019209ee-9ca2-40ee-b3f5-dd595a5cd995.jpg) |
|:--:|
| *Task 3 feedback* |

### <b> Task 4: Rotation of a curve about 2 unknwon axis </b> 
The students are presented a curve rotated about two axis.
They are provided with the rotational angles and need to find a way to rotate the original curve along two axis in the correct order. They give their answer in a multiple choice mode.

