- A simple 3D render engine, fully capable of producing nice-looking 3D images
  Goal:
  - Understand how real modern engines do their black magic
  - Adds 3D rendering capabilities to your application without calling to huge external dependencies
  - Can build 3D viewer app with zero dependencies (apart from Java APIs) that will run almost anywhere - and fit into 50kb


*GUI WRAPPER*
- for rendering images
- has two sliders to adjust rotation


> Jframe : Provides GUI, main window with components like labels, buttons, textfields
> Jframe is the top level container. When using JFrame, to appear onscreen, it MUST be part of a containment hierarchy. 

Containment hierarchy: Tree of components that has a top-level container as its roots(JFrame)
Jframe can only be contained once, if its already in a container and you try to add another container, Jframe wil be moved to the second container

Jframe has a content pane that contains the visible components in Jframe's GUI

Graphics2D for providing sophisticated control over geometry, coordinate transformations, colour management and text layout

Jframe - top level GUI 
renderpanel - the space INSIDE the gui, for whatever that needs to be rendered
g2- black rectangle; sort of like a canvas for the shapes to be drawn on
- is from Graphics2D class
- can set colour to black, then fill rectangle with fillRect()

pane.add : headingSlider -> control horizontal rotation; put at SOUTH of border layout
pitchSlider -> control vertical rotation, put at EAST of border layout
renderPanel -> to render stuff, contains g2, place at CENTER of border layout


Create separate classes to; each is to model a 
Vertex (point) : contains x, y, z (double)

Triangle : contains 3 vertexes and a colour

EG. Tetrahedron: 4 triangles
For each triangle, plot each point on 3D cartesian plane
(all triangles should)

To show only wireframe :discard z - coordinates
1) move the point of path to triangle 1's (x,y) (put the origin ot the center of our drawing area) (initially, 2d origin is located in top left corner of screen)
2) Draw a path line from 1(x,y) to 2(x,y)
3) Draw a path line from 2(x,y) to 3(x,y) (all these is done for all 3 points of the triangle, and for all 4 triangles)
5) remember to closePath()
6) g2.draw(path) so that the path shows up in render panel

orthographic projection: A way of representing 3D object by using several 3D views of the object. (Also known as multiviews)

Use **Matrices** to achieve transformations(rotations) on 3D points.
-> To manipulate 3D points : matrix multiplication
--> Represent points as 3x1 vectors, then transformation is multiplication by 3x3 matrix.
E.g. point A / input vector A : A = [ax, ay, az]

Next, multiply it with **transformation matrix T** to get output vector / point B:
	AT = [ax ay az] * [txx txy txz]
							   [tyx tyy tyz]
							   [tzx tzy tzz]
		= [axtxx+aytyx+aztzx axtxy+aytyy+aztzy aztxz+aytyz+aztzz]
		= [bx by bz]
Using 3x3 matrices, translation is off-limits, only possible with 4x4 matrices, effectively doing skew in 4D space

***Rotation***
- Any rotation in 3D space can be expressed as a combination of **3 primitive rotations**
-> Rotation in XY plane || Rotation in YZ plane || Rotation in XZ plane


NOTE: If you need to rotate in 2 or more planes , you can precompute the transformation matrices FIRST, then use it again with the point. (Instead of recomputing multiple rotations on each point)
I.E. **(AT1)T2 = A(T1T2)**

To create 3x3 Matrix:
1) Create a new class, Matrix3
2) List of values of type double
3) Multiply method with another 3x3 matrix (result[row*3+col] += this.values[row*3+i]*other.values[i*3+col]; notice how i is swapped between this and other matrices)
4) Transform method of each vertex (take each point's x,y,z coordinates and multiply with corresponding value in matrix)

**Rotation sliders**
- Horizontal slider for "heading" - XZ direction (left-right)
- Vertical slider for "pitch" - YZ direction (up-down)





****