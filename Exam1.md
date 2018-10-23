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