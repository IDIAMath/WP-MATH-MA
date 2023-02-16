# Documentation of Stack exercises in IDIAM at FAU

## General remarks

This document is a piece of information supplementary to Moodle-Stack exercises constructed in the Erasmus+ project IDIAM. It aims to provide additional information about the nature of the exercises as well as a clarification of its structure.
The aim of the project is to provide a Sandbox of exercises in the realm of visualization of higher dimensional calculus to facilitate learning of this subject for university students. 
Teachers should be able to apply these exercises in a web-based system like Moodle for the students to access it, as well as making slight changes to the exercises in order to fit their needs.
For every task, aims of the task are formulated and referenced with competencies of university students in mathematics based on [A Framework for Mathematics Curricula in Engineering Education, SEFI (2013) (last checked on December 22 2022)](https://sefi.htw-aalen.de/Curriculum/Competency%20based%20curriculum%20incl%20ads.pdf).

### Overview of competencies
+ Thinking mathematically
+ Reasoning mathematically
+ Posing and solving mathematical problems
+ Modelling mathematically
+ Representing mathematical entities
+ Handling mathematical symbols and formalism
+ Communicating in, with, and about mathematics
+ Making use of aids and tools

The exercises aim to develop these competencies in students with an emphasis on graphical representation of otherwise hard to grasp concepts.

### Structure of Stack exercises


### <u>Learner's perspective</u>

1. The problem is presented using a brief text. Fundamental variables are named, values are provided and the problem is posed.
1. Next, a JSXGraph applet can be provided. This is a JavaScript-based language used to visualize mathematics in 2D and 3D. Hence, there are plenty of possibilities starting from geometric constructions with moveable points ranging to 3D volumes that can be inspected by turning and modified by the user.
1. Lastly, an input is demanded. It is the solution to the problem posed and can be given in a suitable way depending on the task. It can be multiple choice, calculated numbers, functions etc. .
1. Upon confirming the input, the learner gets feedback. This is comprised of the correct solution, a general feedback on the method or solution as well as a specified feedback based on the learner's answer.

### <u> Programmer's perspective </u>

From the programmer's point of view, a Stack exercise is composed of multiple components. We will briefly go over them now.

1. General information such as the name of the exercise
1. Question variables

    The variables generated in this window are used to randomize tasks. This makes the question more general and enables solving the same problem repeatedly with different parameters. It is also important to disable cheating in exams.
    
    Here all of the important parameters are randomized using Stack, a modified programming language based on the symbolic language Maxima. This way, fractions like `1/2` can be represented as $\frac{1}{2}$ as opposed to $0.5$. Also it is capable of simplifying algebraic terms or calculating derivatives.

1. Question text

    Here, everything that is visible to the student is specified. It starts with an explanation of the task, typically intertwined with LaTex text setting. Here formulas and special charakters can be read as LaTex using an evironment. For example `\(\frac{1}{2}\)` will be interpreted as $\frac{1}{2}$ and shown to the student this way.

    Consequently the actual task is programmed. Within this project, this will always contain a JSXGraph environment. It begins with `[[jsxgraph width="500px" height="500px" ]]` or a similar expression and ends with `[[/jsxgraph]]`.

    In between, code is programmed either in JavaScript or JesseCode.
    The code imports information from the Question variables, making it dependend on the randomization process.

1. General feedback

    The text in this field will be displayed to every user upon answering the question. It can contain LaTex as well as the randomized parameters in order to clarify the solution of the task.

1. Specific feedback using a potential respone tree (PRT)

    It is helpful to clarify for the student, which parts exactly of the answer were correct and which were faulty. If the answer contains more than one piece of information, this specific feedback can be given with the help of a potential response tree. Here each part of the answer is checked seperately in the nodes of a tree graph. Nodes can be weighted individually and connected as desired. That way, if a node is correct different feedback is given from the case where it is correct. The branching enables very specific feedback providing helpful tips.


## Programming basics

   ### Stack

   Stack is used in Moodle's Question variables. It is a symbolic language. Therefore a variable of value e.g. `1/2` will be displayed as $\frac{1}{2}$. Stack is based on the language Maxima and uses its syntax with slight modifications. We will go over some of the features of Stack and how to use it.

+ In Stack, equations can be saved to a variable in order to solve for a variable. Hence variable names cannot given in the form `x = 2`, since all of this would be just an entity of type equation. <br>
Instead variables are defined using the character `:`, e.g.: `x: 2`, `eq: 2*x+y=0`.
+ Lines end with the characted `;`.
+ Comments can be made with `//`. The content in a line after this will be neglected. Alternatively, anything between `/*` and `*/` will also be neglected. This can be used for comments over more than one line of code.
+ Expressions are automatically simplified.
+ Equations can be solved using `solve(equation_name, variable_name)`. This command gives a list as result.
+ Lists are containers of elements in the shape `[element_1, element_2,...]`, e.g.: `list_1: [a,b,c]`. The elements can be individually accessed using indexing in square brackets `[]`. Indexing starts with `1` for the first element. In this case `list_1[1]` results in `a`.  
+ Functions are generated using `:=` e.g.: `f:= a*x^2+b*x+c`. Functions can be evaluated using parentheses `()`. In this case `f(0)` results in `c`.
+ Numbers or expressions can be randomly selected from a list with the command `rand()`. If an element of the list `list_1` shall be randomly selected, the command `selection: rand(list_1)` will do so. Here a new variable called `selection` is generated. For `list_1` from above, `selection` can have the values `a`,`b` or `c`. If these are variables themselves, `selection` can be used in just the same way as they would. <br>
This enables writing one program and inputting randomly selected variables. That way, the result changes slightly upon execution, depending on the result of `rand()`.
+ The irrational number $\pi$ can be used using `%pi`
+ If expressions shall be interpreted numerically, the code needs to be enwrapped by a `numer` environment. The environment begins with `numer: true` and ends with `numer: false`. For example, the value of $\pi$ can be given as an approximation using 
```
numer: true
numerical_pi: %pi;
numer: false
``` 
+ In Moodle's Question text, Stack variables can be taken from Question variables using `{#variable_name#}`. For example, `{#numerical_pi#}` will be treated as the number `3.1415...`. 

### HTML

HTML is used in web pages. Here it specifies, how text, applets or code is displayed to the user in Moodle questions.
+ Environments are declared with `<>`. They begin with `<environment_name>` and end with `</environment_name>`.
+ Blocks of text are enwrapped in `<p>` and `</p>`. If a new bock is declared, there will be a new paragraph displayed.
+ Bold text can be displayed using `<b>` and `</b>`.
+ Inline-LaTex expressions can be displayed using `\(` and `\)`. Similarly, LaTex equations in a standalone, centered line can be displayed using `\[` and `\]`.
+ In Moodle Question Text, JSXGraph applets can be included using `[[jsxgraph]]` and `[[/jsxgraph]]`. This is different from normal HTML, where JSXGraph applets are included with a `<div>` and `</div>` environment.
+ Similarly, answers and validtadion of answers are included using `[[input: ans1]]` and `[[validation: ans1]]`.

### JSXGraph

JSXGraph is a JavaScript-based library. It can be used for visualisation of mathematics in an interactive manner. It is included in HTML code in a dedicated environment. A detailed documentation is available [here](https://jsxgraph.uni-bayreuth.de/wp/docs/index.html).
+ Variables are created explicitly with the command `var variable_name = variable_value`, e.g.: `var a= 0.3`.
+ A "board" is the base of the applet, defining its size. It is created using `var board = JXG.JSXGraph.initBoard()`.
+ Displayed objects such as lines, curves, surfaces, points etc. are created using the `board.create()`method.
+ For 3D applications a "view3d" object is necessary additionally. It is created using `var view = board.create('view3d', args)` as well.
+ In 3D, points, lines etc. are created using the `view.create()` method.
+ In Moodle Question text within the JSXGraph environment, Stack variables can be imported using `{#variable_name#}`. They are typically assigned a new variable name upon importing.
+ The irrational number $\pi$ is included using `Math.PI`.
+ Functions such as $\cos, \sin$ and $\exp$ are included using `Math.cos()`, `Math.sin()`and `Math.exp()`.