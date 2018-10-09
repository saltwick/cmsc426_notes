#  Texture

## Issues
1. Analysis
    - Determining if textures are similar
2. Synthesis
    - Creating textures from other textures
    - Painting
3. Segmentation
4. Shape

## What is Texture?
- Repeats with variation
- Must separate what repeats and what stays the same
- Model as repeated trials of a random process
    + Probability distribution stays the same
    + Each trial is different

## How to Compare Textures
- Simplest comparison is SSD
- View histograms
    + Test probability samples drawn from same distribution
- Chi squared distance between histograms

$$
\chi^2(h_i, h_j) = \frac{1}2 \sum_{m=0}^k \frac{[h_i(m) - h_j(m)]^2}{[h_i(m) - h_j(m)]}
$$

## Gabor Filters
- Filters at different scales and spatial frequencies

## Markov Model
- Captures local dependencies
    + Each pixel depends on neighborhood

## Markov Random Field
- Generalization of Markov chains to two or more dimensions
- First Order MRF
    + Probability that pixel _X_ takes a certain value given the values of neighbors _A,B,C,D_

$$
    P(X|A,B,C,D) = \def\arraystretch{1.5}
   \begin{array}{c:c:c}
    & A &  \\ \hline
   D & X & B \\
   \hline
    & C & 
\end{array}

$$

## Texture Synthesis
- Given texture, apply it to another space

### Synthesizing One Pixel
- Find P(x|neighbors)
- Find all windows in image that match the neighborhood
    + Consider only pixels in neighborhood that are already filled in
- To synthesize __x__
    + Pick one matching window at random
    + Assign __x__ to be the center of that window
- Increasing window size -> Better results 


    
