<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">November 6th 2018 </div>
<div style="text-align: right">Fall 2018 </div>

# Epipolar Geometry
---

## Three Questions
1. **Correspondence Geometry**
    - Given an image point $x$ in the first view, how does this constrain the position of the corresponding point $x'$ in the second image?
2. **Camera Geometry (motion)**
    - Given a set of corresponding image points ${x_i \leftrightarrow x'_i}, i = 1,...,n$
    - What are the cameras $P$ and $P'$ for the two views?
    - What is the geometric transformation between the two views?
3. **Scene Geometry (structure)**
    - Given corresponding image points $x_i \leftrightarrow x'_i$ and cameras $P,P'$
    - What is the position of the point $X$ in space?

## Geometry
- Epipolar plane $\pi$ is the plane formed by $P,P',X$ 
- Plane passes through camera planes and points $x,x'$ lie on the edges of the plane
- Epipoles - Intersection of baseline with image plane
    + Projection of projection center in other image
    + Vanishing point of camera motion direction
- Baseline - Line formed by $\pi$ and the epipoles -> Translation between cameras

- Cross Produt 
$$
a \times b = \begin{bmatrix} 0 & -a_3 & a_2\\ a_3 &0 &-a_1\\-a_2 & a_1 & 0 \end{bmatrix}b = [a_x]b
$$
- Triple Scalar Product -> 3 points are coplanar
$$
(a\times b) \cdot c = 0
$$
- Equations
$$
P' = RP + t
\\[.5em]
p = MP , M = [I|0]
\\[.5em]
p' = M'P' , M' = [R|t]
\\[.5em]
\text{P is the point in space, p,p' are points in image}
$$

$$
\vec{O'p'} , \vec{OO'}, \vec{Op} \text{ are coplanar} \implies
p' \cdot [t \times (Rp)] = 0, \begin{cases} p = (u,v,1)^T \\ p' = (u',v',1)^T \end{cases}
\\[.5em]
p' \cdot [t \times (Rp)] = 0 \implies p' \cdot [(t \times R)p] = 0 \implies p' ([t_x]R)p = 0
\\[.5em]
\underbrace{E = [t_x]R}_\text{Essential Matrix} \implies \boxed{p'Ep = 0}
$$
- Essential Matrix
    + E can be used to find rotation and translation
    + Computed from point correspondences

