<div style="text-align: right">Sam Saltwick </div>
<div style="text-align: right">November 20th 2018 </div>
<div style="text-align: right">Fall 2018 </div>

# Pose from Projective Transformation
---

- Recall the projection from world to camera
$$
\begin{bmatrix}u \\ v \\ w\end{bmatrix} = K\begin{bmatrix}r_1 & r_2 & r_3 &T\end{bmatrix}\begin{bmatrix}X \\ Y \\Z \\ W \end{bmatrix}
$$
- Where $r_1, r_2, r_3$ are the columns of the rotation and T is the translation vector
$$
x = K(R | T) X
$$

- If you can assume that all points lie in the ground plane $Z = 0$
$$
\begin{bmatrix}u \\ v \\ w\end{bmatrix} = K\begin{bmatrix}r_1 & r_2 &T\end{bmatrix}\begin{bmatrix}X \\ Y\\ W \end{bmatrix}
$$

- This transformation can be seen as a homography $H = K\begin{bmatrix}r_1 & r_2 & T\end{bmatrix}$
- Is this a projective transformation?
$$
det(\begin{bmatrix}r_1 & r_2 & T\end{bmatrix}) = T^T(r_1 \times r_2)
$$
- This vanishes only if the camera lies in the ground plane
- If the determinant is not 0 $\implies$ invertible transformation
- Estimate H from $N \geq 4$
- Name the columns of $K^{-1}H$
$$
K^{-1}H = \begin{bmatrix}h'_1 & h'_2 & h'_3\end{bmatrix}
$$
- If the SVD of $\begin{bmatrix} h'_1 & h'_2 & h'_1 \times h'_2\end{bmatrix} = USV^T$ then you can solve for the translation 
