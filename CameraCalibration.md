<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">December 4th 2018 </div>
<div style="text-align: right">Fall 2018 </div>

# Camera Calibration

---

## What is Camera Calibration?
- Finding quantities internal to the camera that affect the imaging process
    + Position of image center in the image (where optical axis meets image plane)
    + Focal length (Distance from camera to image plane)
    + Different scaling factors for row/column pixels
    + Skew factor
    + Lens distortion (pin-cushion effect)

## Techniques
- Roger Tsai
- Linear algebra method
    + Can be used as initialization for iterative non linear methods
- Methods using vanishing points 

## Procedure
- Calibration target: 2 planes at right angle with checkerboard pattern (Tsai grid)
- *Incomplete*

## Image Processing of Image of Target
- Canny Edge detection
- Straight line fitting
- Intersection of lines to obtain corners
- Matching image corners and 3D target checkerboard corners
    + Counting if whole target is visible in image
- Get pairs of image points and world points $(x_i,y_i) \rightarrow (X_i,Y_i,Z_i)$

## Central Projection
- If world and image points are represented by homogeneous vectors, central projection is a linear transformation
$$
x_i = \frac{u}{w} , y_i = \frac{v}{w}
\\[1em]
\begin{bmatrix} u \\ v \\ w \end{bmatrix} = \begin{bmatrix}f & 0 & 0 & 0 \\ 0 & f & 0 & 0 \\ 0 & 0 & 1 & 0\end{bmatrix} \begin{bmatrix} x_i \\ y_i \\ z_i \\ 1 \end{bmatrix}
$$

$$
\begin{bmatrix} u' \\ v' \\ w' \end{bmatrix} = \begin{bmatrix}\alpha_x & 0 & x_0 & 0 \\ 0 & \alpha_y & y_0 & 0 \\ 0 & 0 & 1 & 0\end{bmatrix} \begin{bmatrix} x_s \\ y_s \\ z_s \end{bmatrix}
\\[.5em]
\alpha_x = fk_x, \alpha_y = fk_y, x_i = f\frac{x_s}{z_s}, y_i = f\frac{y_s}{z_s}
\\
\text{image center} \implies (x_0, y_0)
\\
\text{scaling factors} \implies k_x,k_y
$$
- $\alpha$ is the focal length in pixels in each direction
- s is skew parameter
- K is the *calibration matrix* $\implies$ 5 degrees of freedom
    + 3x3 upper triangular matrix

$$
K = \begin{bmatrix} \alpha_x & s & x_0 \\ 0 & \alpha_y & y_0 \\ 0 & 0 & 1\end{bmatrix}
\\[.5em]
K[I_3 | 0_3] = \begin{bmatrix}\alpha_x & 0 & x_0 & 0 \\ 0 & \alpha_y & y_0 & 0 \\ 0 & 0 & 1 & 0\end{bmatrix}
$$
