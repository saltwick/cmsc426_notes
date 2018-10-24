<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">Fall 2018 </div>

# CMSC426 Exam 1 Notes

## Convolution and Filters
- Deconvolution process
    + Find individual values in the kernel based on where the convolution has only 1 nonzero input
- Some Kernel Examples

    $$
    \text{Gaussian Kernel} \implies \frac{1}{16}\begin{bmatrix} 1 & 2 & 1\\ 2&4&2\\1&2&1\end{bmatrix}
    $$
    $$
    \text{Sobel Kernel} \implies 
    G_x = \begin{bmatrix} 1 & 0 & -1\\ 2&0&-2\\1&0&-1\end{bmatrix},
    G_y = \begin{bmatrix} 1 & 2 & 1\\ 0&0&0\\-1&-2&-1\end{bmatrix}
    $$

    $$
    Sharpen \implies \begin{bmatrix} 0&-1&0 \\ -1&5&-1 \\ 0&5&0 \end{bmatrix}
    $$
- Padding Options
    + Zero padding -> Pad edges of matrix with all 0's
        $$
        \begin{bmatrix} {\begin{vmatrix} 0 & 0 \end{vmatrix}} a & b &... \end{bmatrix}
        $$
    + Reflection padding -> Reflect end of matrix 
        $$
        \begin{bmatrix} {\begin{vmatrix} b & a \end{vmatrix}} a & b &... \end{bmatrix}
        $$
    + Repeated Cyclic
        $$
        \begin{bmatrix} {\begin{vmatrix} y & z \end{vmatrix}} a & b &...&y&z \end{bmatrix}
        $$
    + Edge Values
        $$
        \begin{bmatrix} {\begin{vmatrix} a & a \end{vmatrix}} a & b &...&y&z{\begin{vmatrix} z & z \end{vmatrix}} \end{bmatrix}
        $$
## Camera Projections
- **Pinhole Model**
    + Projection from 3D onto 2D plane
    + Lines viewed with a pinhole camera will have their vanishing point at infinity if the line is in a plane parallel to the image plane
    + Focal length $f$ -> Distance from camera pinhole to plane
    + $(X,Y,Z)$ is the point in 3D space, $(x,y)$ is the point in 2D
    
    $$
        y = \frac{fY}{Z}
        \\[1em]
        x = \frac{fX}{Z}
    $$
- Orthographic Projection of 2 parallel lines must be parallel in the image

## Geometric Transformations
- **Types of Transformations**
    $$
    \text{Projective/Homography (8DoF/4pts)} \implies 
    \begin{bmatrix}h_{11}&h_{12}&h_{13}
    \\
    h_{21}&h_{22}&h_{23}
    \\
    h_{31}&h_{32}&h_{33}\end{bmatrix}
    \\[1em]
    \text{\textbf{Invariants -}  Colinearity, Cross Ratios}
    \\[1em]
    \text{Affine (6DoF/3pts)} \implies 
    \begin{bmatrix}a_{11}&a_{12}&t_x
    \\
    a_{21}&a_{22}&t_y
    \\
    0&0&1\end{bmatrix}
    \\[1em]
    \text{\textbf{Invariants -}  Parallelism, Area Ratios, Length Ratios}
    \\[1em]
    \text{Similarity (4DoF/2pts)} \implies 
    \begin{bmatrix}sr_{11}&sr_{12}&t_x
    \\
    sr_{21}&sr_{22}&t_y
    \\
    0&0&1\end{bmatrix}
    \\[1em]
    \text{\textbf{Invariants -}  Angles, Length Ratios}
    \\[1em]
    \text{Euclidean/Translation (3DoF/2pts)} \implies 
    \begin{bmatrix}r_{11}&r_{12}&t_x
    \\
    r_{21}&r_{22}&t_y
    \\
    0&0&1\end{bmatrix}
    \\[1em]
    \text{\textbf{Invariants -}  Angles, Length Ratios}
    \\[1em]
    $$
- Given 4 points solve for their transformations

    $$
    \begin{bmatrix}\prime{x_1} \\ \prime{y_1}\end{bmatrix} = \begin{bmatrix} m_1 & m_2 \\ m_3 & m_4\end{bmatrix} + \begin{bmatrix} t_1 \\ t_2 \end{bmatrix}
    $$


## Solving Problems in Class
- Given 4 points on an image and the vanishing lines, compute the vanishing points from the coordinates of A,B,C,D
- Use projective coordinates
- Draw 3D projection onto plane
- *Example*
    $$
    A = (2,3) , B = (5,6) , C = (10,15) , D = (11,17)
    $$
    + Convert to 3D coordinates using $z= f$
    $$
    A = (2,3,1) , B = (5,6,1) , C = (10,15,1) , D = (11,17,1)
    $$
    + Find $V_1$ by finding intersection of  $\overline{AB}$ and $\overline{BC}$
    $$
    \overline{AB} = \vec{a} \times \vec{b}
    \\[1em]
    \begin{vmatrix} a_x & a_y & a_z \\ b_x & b_y & b_z \\ i&j&k\end{vmatrix} = i \cdot \underbrace{\begin{vmatrix} a_y & a_z \\ b_y & b_z\end{vmatrix}}_{\text{x}} - j \cdot \underbrace{\begin{vmatrix} a_x & a_z \\ b_x & b_z\end{vmatrix}}_{\text{y}} + k \cdot \underbrace{\begin{vmatrix} a_x & a_y \\ b_x & b_y\end{vmatrix}}_{\text{z}}
    $$
    + Alternate Cross Product calculation
    $$
    c_x = a_y \cdot b_z - a_z \cdot b_y \\
    c_y = a_z \cdot b_x - a_x \cdot b_z \\
    c_z = a_x \cdot b_y - a_y \cdot b_x
    $$
    + Repeat cross product of $\vec{c}$ and $\vec{d}$ to get $\overline{CD}$
    $$
    \overline{AB} = (-3, 3, -3), \overline{CD} = (-,-,-)
    $$
    + Vanishing Point $V_1$ is where $\overline{AB}$ and $\overline{CD}$ cross
        - Cross Product of the two lines gives their intersection -> Vanishing Point

- Given camera with focal length $f$, translation $(U,V,W)$ and a 3D plot with 2 planes -> Find Optical Flow function
    $$
    u(x,y) = \frac{-U + xW}{Z}  \\[1em]
    v(x,y) = \frac{-V + yW}{Z}  \\ 
    $$
    + Since $Z$ is constant we can replace it with $z_0$ (distance to plane)
    $$
    u(x,y) = \frac{-U + xW}{z_0}  \\[1em]
    v(x,y) = \frac{-V + yW}{z_0}  \\ 
    $$
    + Flow will be along lines that pass through the camera center
    + Flow values increase as you move further away from the origin since they are linear with $x$ and $y$
    $$
    (u(x,y), v(x,y)) = \frac{W}{k} \cdot (x,y)
    $$

- What if the camera is rotating in the previous problem? Find new optical flow function
    + Sum of translational and rotational optical flow
    $$
    u = \frac{W}{Z} (x - \frac{U}{W}) + \alpha x y - \beta(1+x^2) + \gamma y \\[1em]
    v = \frac{W}{Z} (y - \frac{V}{W}) + \dot{y} = \alpha(1 + y^2) - \beta x y + \gamma x
    $$
- Suppose a camera is rotating & translating -> Find rotation & translation given an optical flow field
    + Only have W and $\gamma$ -> Moving straight and rotating around axis of translation (*i.e. corkscrew*)
    + Derotate -> Check if flow makes a pencil

- Find probability of success for RANSAC
    + $p$ is the probability of choosing a good set of points
    + What is the probability of success after $N$ iterations?
    + Need to pick 4 points for homography 

    $$
    p_success = 1 - (1-p^4)^N
    $$

