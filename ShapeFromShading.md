<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">November 20th 2018 </div>
<div style="text-align: right">Fall 2018 </div>

# Shape from Shading
---

## Quantitative Shape Recovery
- Orthographic projection
- We have gray levels at pixels $(x,y)$
- We want to recover the orientations of the normals at points $(x,y,z)$
- By integration, we want to obtain $z = f(x,y)$

## Radiance
- Radiance $L (\theta _1)$ is power emitted per unit area (flux) into a cone having unit solid angle

## Reflectance
- Reflection is characterized by reflectance
- Ratio of radiance/irradiance
- Described by a function called Bidirectional Reflectance Distribution Function
- BRDF = $f(\theta _i, \phi _i, \theta _e , \phi _e) = \frac{L(\theta _e, \phi _e)}{dE(\theta _i, \phi _i)}$

## Labertian Surfaces
- If BRDF is a constant $K$, surface is called a Lambertian surface

## Simple Radiometric Modeling
- Pixel brightness is proportional to radiance of corresponding scene patch
- Pixel brightness is proportional to cosine of angle between normal to patch and direction of illumination source
- For a given pixel brightness, the locus of possible normals $(p,q)$ in gradient space is a conic

## Normals to $z = f(x,y)$
- Intersect surface plane $z = f(x,y)$ with red plane and blue plane
- Find tangents to red curve and blue curve
- Write that normal is perpendicular to 2 tangents and is in direction of cross-product

## Gradient Space
- Orientations of normal can be represented by 2 parameters
$$
p = \frac{\partial f}{dx}
\\[1em]
q = \frac{\partial f}{dy}
$$
- Components of p and q are called the gradient space coordinates of the normal
- Any direction $(a,b,c)$ can be represented by $(-a/c, -b/c, -1)$ and by a point with 2 components in the same 2D gradient space

## Geometric Interpretation of Gradient Space
- A direction $(a,b,c)$ can be represented by a point on a plane $Z=-1$ by constructing the intersection between the vector of the same direction drawn from the origin, and the plane 

## Reflectance Map
- 2D lookup table that gives the pixel brightness as a function of the orientation of the scene surface in camera coordinates