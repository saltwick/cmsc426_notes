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


## From Camera Coordinates to World Coordinates
- *Some Equations omitted here*
$$
P = K[I_3 | 0_3]\begin{bmatrix}R & -R\bar{C}\\0_3^T & 1\end{bmatrix}\begin{bmatrix}X_s\\Y_s\\Z_s\\1 \end{bmatrix}
\\[1em]
P = KR[I_3 | -\bar{C}]
\\[1em]
\begin{bmatrix} u \\ v \\ w \end{bmatrix} = P \begin{bmatrix} X \\ Y \\ Z \\ 1 \end{bmatrix}
$$
- $P$ has 11 DOF
    + 5 from triangular calibration $K$, 3 from $R$, 3 from $\bar{C}$
- $P$ is fairly general 3x4 matrix
    + Left 3x3 submatrix $KR$ is non-singular

## Calibration Steps
1. Estimate $P$ using scene points and their images
2. Estimate the interior parameters and the exterior parameters 
$$
P = KR[I_3 | -\bar{C}]
$$
    - Left 3x3 submatrix of $P$ is product of upper triangular matrix and orthogonal matrix

## Finding Camera Translation
- Find homogeneous coordinates of C in the scene
- C is the null vector of matrix $P$
    + $PC = 0$
- Find null vector $C$ of $P$ using SVD
- C is the unit singular vector of $P$ corresponding to the smallest singular value (last column of $V$, where $P = UDV^T$ is the SVD of $P$)

## Finding Camera Orientation and Internal Parameters
- Left 3x3 submatrix $M$ of $P$ is $M=KR$
    + $K$ is upper triangular
    + $R$ is orthogonal rotational matrix
- Any non-singular square matrix $M$ can be decomposed into the product of an upper triangular matrix $Q$ and an orthogonal matrix $R$ using $RQ$ factorization
    + Similar to QR but reversed

## Improved Computation of P
- $x_i = PX_i$ involves homogeneous coordinates, thus $x_i$ and $PX_i$ just have to be proportional $\implies x_i \times PX_i = 0$
- Let $p_1^T, p_2^T, p_3^T$ be the 3 row vectors of $P$
- $x_i \times PX_i$ yields matrix of knowns times 12x1 matrix of unknowns ($p_{1-3}$) that equals 0
- Can easily solve for $\begin{bmatrix}p_1 \\ p_2 \\p_3\end{bmatrix} = \hat{p}$ using SVD if A in $A\bar{p} = \bar{0}$

## Radial Distortion Modelling
- Minimize $f(\kappa_1, \kappa_2) = \sum_i (x'_i - x_{ci})^2 + (y'_i - y_{ci})^2 $ using lines known to be straight
- $(x'_i, y'_i)$ is the radial projection of $(x_i,y_i)$ onto straight lines
- Needs precisely known 3D points
- **Zhang's approach**
    - Capture various positions of calibration grid
    - Transformations between images are homographies $\rightarrow$ can match corners of boxes to find homography
    - Use homographies to solve for parameters
    - image point = Calibration matrix A * [R | T] * World point
    - Assume plane at z=0
    