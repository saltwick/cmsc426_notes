<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">October 16th 2018 </div>
<div style="text-align: right">CMSC426 Fall 2018 </div>

# Image Motion
---

## Information from Image Motion
- 3D motion between observer and scene + structure of the scene
    + Motion Parallax -> two static points close by in image with different image motion
    + Larger translational motion corresponds to the point closer by (smaller depth
- Create new image out of magnitudes of horizontal and vertical motion components
    - Edge detection to get motion components

## Motion Analysis Problems
- Correspondence Problem
    + Track corresponding elements across frames
- Reconstruction PRoblem
    + Given a number of corresponding elements, and camera parameters, what can we say about 3D motion and structure of the observed scene?
- Segmentation Problem
    + What regions of the image correspond to *different* moving objects?

## The Aperture Problem
- Line moving through aperture (hole) -> only information is motion perpendicular to line.
- Can only find one component of optical flow
    + Only the flow componenet perpendicular to the line feature -> Normal Flow
- $I(x,y,t) = I(x,y,t) + \frac{\partial{I}}{\partial{x}} \frac{dx}{dt} + \frac{\partial{I}}{\partial{y}} \frac{dy}{dt} + \frac{\partial{I}}{\partial{t}} \frac{dt}{dt} $
    + Taylor Series Expansion -> Ignore non-linear terms since they are so small with regard to images

## Optical Flow Equation
- $0 = I_t + \triangledown I \cdot [u,v]$
- Use more equations for a pixel
    + Impose additional constraints
    + Assume flow field is smooth -> Same flow within small window ($5\times5$)
        - ($5\times5$) window gives 25 equations per pixel
        - $0 = I_t(p_i) + \triangledown I(p_i) \cdot [u\space v]$
        - $A_{25\times2} \cdot d_{2\times1} = b_{25\times1}$
        - Use least squares to solve -> Minimize $\left\lVert Ad-b\right\rVert^2A
        $
