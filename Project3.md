<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">October 30th 2018 </div>
<div style="text-align: right">CMSC426 Fall 2018 </div>

# Project 3 - Rotobrush
### Segmenting Deformable Objects in a Video
---

## Segmentation
- Given a point/pixel $x_{i,j}$ in an image, where does it belong?
- Why do we need segmentation?
    + Localization
    + Object Detection
    + Tracking

## Deformable Objects
- Objects that change shape
- Changing shape -> Can't use static Mask

## SnapCut
1. Segmenting object of interest in first frame
    - Call it foreground, $F$ 
    - Everything else is the background $B$
2. Create Local Classifiers
    - Local windows along edge of initial mask $W_k^t$
    - Must have *some* overlap between windows (20-30%)
3. For each local window
    1. Initialize Color Model for GMM
    2. Initialize Shape Model
    3. Combine Shape + Color
    4. Update Color + Shape Model

## Digging Deeper
- Use *roipoly()* to select mask
- Select $k$ points around object 
    - $k$ ~60x60 windows -> Must have overlap
- **Color Model**
    - Per window
    $$
    p_c(x) = \frac{p_c(x|F)}{(p_c(x|F) + p_c(x | B))}
    $$
    - Fit GMM model -> can use MATLAB functions
    - Find probabilities of foreground 
- **Color Confidence**
    + Are foreground and background separable?
    $$
    f_c = 1 - \frac{\int_{W_c} |L^t(x) - p_c(x) | \cdot \omega_c(x) dx}{\int_{W_k} \omega_c(x) dx}
    \\[1em]
    \small{d = \text{euclidean distance between $x$ and foreground boundary}}
    \\[1em]
    \Large{\omega_c = e^{\frac{-d^2(x)}{\sigma^2_c}}}
    $$
    + $f_c$ is a single value
    + $\omega_c$ -> Weight function
    + |L^t(x) - p_c(x) | = Subtract probabilities from mask
- After doing this for every window -> Will have border around object
- **Shape Model** 
    $$
    \Large{f_s(x) = 1 - e^\frac{-d^2(x)}{\sigma^2_s}}
    \\[1em]
    \small{\sigma_s \text{is a parameter}}
    $$
    - Shape confidence decreases as color confidence increases
- **Local Window Propagation**
    + Use SIFT features -> track $k$ points across frames
    + Update window based on matched point in next frame
        - Use optical flow (MATLAB functions) to update windows
    + Update Color and Shape Models with next frame data

    $$
    p^k_F(x) = f_s(x) L^{t+1}(x) + (1-f_s(x))p_c(x)
    \\[1em]
    p_F(x) = \frac{\sum_k p_F^k(x)(|x - c_k| + \epsilon)^{-1}}{\sum_k(|x-c_k| + \epsilon)^{-1}}
    \\[1em]
    \small{c_k\text{ is the center of the window} \implies \text{closer points to center weighted more heavily}}
    \\[.5em]
    \small{\epsilon \text{ is a small value to regulate points next to or on center}}
    $$
- Visualization functions given
