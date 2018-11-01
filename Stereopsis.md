<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">October 23 2018 </div>
<div style="text-align: right">Fall 2018 </div>

# Steropsis
---

## Why Stereo Vision?
- 2D images project 3D points into 2D
- 3D points on the same viewing line have the same 2D image
    + 2D imaging results in depth information loss

## Stereo
- Assumes two cameras with known positions
- Can recover depth from this information 
## Recovering Depth
- Depth recovered with two images and triangulation
- Find correspondences between images and see where their projective lines meet 
- Solution is not always unique
    - Looking at 3 points -> 9 intersections in space -> 3 possible solutions
- Find Correspondences and epipolar lines
    + Epipolar lines -> lines formed by the intersection between the plane created by 2 correspondences and their intersection and the camera plane
    + Reduces correspondence problem to 1D search in conjugate epipolar lines

## Simplest Case
- Image planes of cameras are parallel
- Focal points are at the same height
- Focal lengths are the same
- => Epipolar lines are horizontal scan lines

## Calculations
$$ 
\frac{T + x_r - x_l}{Z -f} = \frac{T}{Z}
\\[1em]
Z = f \frac{T}{x_l - x_r}
,
d = x_l - x_r
\implies \boxed{Z = f \frac{T}{d}}
$$
- T is the stereo baseline
- d measures the difference in retinal position between correspondences
- Given Z we can compute X and Y

## What Correspondences should we match?
- Objects? Edges? Pixels? Collections of pixels?
- Slide window along scanline and compare its contents with the reference window in the other image
- Matching Cost: SSD or normalized correlation
    + Minimize SSD or Maximized Correlation
- Correspondence at the minimum point of the matching cost
- **Effects of Window Size**
    + Window size too small -> A lot of noise
    + Window size too big -> Too much smoothing => loss of detail