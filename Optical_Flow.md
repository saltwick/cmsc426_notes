<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">October 11th 2018 </div>
<div style="text-align: right">CMSC426 Fall 2018 </div>

# Optical Flow
---
## Optical Flow Vectors
- Vector field of pixel movements
- Can be used to detect moving objects
- Visual Correspondance
    + Points that correspond to the same thing in 3D space, across two different times
- Vector between two visual correspondances -> optical flow vector 
- Field of optical flow vectors -> vector field 
- Pencil = Geometric term for all lines through point
    + Optical flow vectors lie on pencils
- Solving Problem of *Ego Motion*
    + Ego Motion = How the system itself is moving
## Benefits of Measuring Optical Flow
- Allows you to find translations between points
- **Inertial sensors**
    + Measure velocity/acceleration/rotation to estimate location/motion
    + Much less accurate than optical flow -> Smallest unit is a pixel

## Handling Rotation
- Cyclotortion with velocity $\gamma$
- *How does this change the optical flow?*
    + Flow becomes **tangential** to concentric circles centered on the axis of rotation

- Some rotation around vertical axis with velocity $\beta$
- *How does this change the optical flow?*
    + Flow becomes **tangential** to concentric **hyperbolas** that limit to x-axis
- What about rotation around x-axis with velocity $\alpha$?
    + Flow becomes **tangential** to concentric **hyperbolas** that limit to the y-axis
- Rotation around multiple axis
    + $\begin{bmatrix} \alpha \\ \beta \\ \gamma \end{bmatrix}$ is the rotation vector
    + Sum vectors to get final outcome

## Rotation and translation
- Rotational Vector -> $\begin{bmatrix} \alpha \\ \beta \\ \gamma \end{bmatrix}$    Translational vector -> $\begin{bmatrix} u \\ v \\ w \end{bmatrix}$<br><br>
- (X,Y,Z) -> (x,y) where $x = \frac{fX}{Z},  y = \frac{fY}{Z}$<br><br>
- $(\frac{dx}{dt}, \frac{dy}{dt}) = (u,v)$<br><br>
- $\begin{bmatrix} \dot{x} \\ \dot{y} \\ \dot{z} \end{bmatrix} = - \begin{bmatrix} u \\ v \\ w \end{bmatrix} \therefore \dot{x} = u, \dot{y} = v, \dot{z} = w$<br><br>

- $\frac{\dot{x}  = \dot{x}Z - x\dot{z}}{Z^2}$

- Flow equations for only translation
    + $u = \frac{W}{Z} (x - \frac{U}{W})$<br><br>
    + $v = \frac{W}{Z} (y - \frac{V}{W})$<br><br>
    + $(\frac{U}{W},\frac{V}{W})$ is the point where all vectors meet<br><br>
- Optical flow will be the same for multiples of velocity equal to multiples of distance
    + Causes ambiguity -> Depth required to find exact translation

- Flow equations for only rotation
    + $\begin{bmatrix} X \\ Y \\ Z  \end{bmatrix} = -\vec{\omega}x\begin{bmatrix} X \\ Y \\ Z  \end{bmatrix}$<br><br>
    + $\dot{x} = \alpha x y - \beta(1+x^2) + \gamma y$<br><br>
    + $\dot{y} = \alpha(1 + y^2) - \beta x y + \gamma x$<br><br>
- Flow with unrestricted movement (rotation and translation)
    + Sum of translational and rotational equations
    + $u = \frac{W}{Z} (x - \frac{U}{W}) + \alpha x y - \beta(1+x^2) + \gamma y$<br><br>
    + $v = \frac{W}{Z} (y - \frac{V}{W}) + \dot{y} = \alpha(1 + y^2) - \beta x y + \gamma x$<br><br>
-  \**Note*: Rotation is separate from scene
    + Rotational flow will be the same across scenes
    + Independent of distance
    + On the other hand, translational flow is dependent on depth $(Z)$
<br>
- Concluding Remarks
    + Translation -> Easy pattern, only expansion vectors
    + Rotation -> Easy pattern, only circles/ hyperbolas
    + Translation + Rotation -> Not easy. Need to separate effects of translation and rotation
    + Depends on FOV -> Larger FOV = Easier separation
    + Imagine spherical eye model (like an insect)
        - Spherical eye moving through space -> Flow expanding along geodesics (*think longitude*) with the transational axis as their axis on front side, and will contract on back side
        - Spherical eye rotating -> Flow will be tangential to concentric circles around sphere (*think longitude*)
    + Spherical eyes have focus of contraction and focus of expansion 
    + Allows them to separate the problem and have better optical flow abilities
