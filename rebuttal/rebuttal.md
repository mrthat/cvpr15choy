We appreciate the valuable comments from all the reviewers. We are happy to
hear reviewers agree on that we proposed “efficient”[R2,R3] and “considerable
improvements to WHO”[R1] in terms of “speed”[R1,R3] and “detection
performance”[R1]. The method was “well motivated”  and validated with
“extensive experiments”[R1].

Caching Sigma inverse for the templates [R1, R2]: 
We propose a way to fine tune the viewpoint in
continuous space without expensive training, thus providing the vision community
with a modular framework for viewpoint estimation. However, caching all the possible
templates for continuous azimuth, elevation, in-plane rotation, focal length and
intraclass CAD models is intractable. To overcome this, our
method generates proposals on-the-fly which requires covariance inversion. 

Effectiveness of fine-tuning [R1, R2]:
Our continuous viewpoint estimation method not only accurately refines the coarse
viewpoint estimation but also recovers from incorrect pose initializations.
Unfortunately, the PASCAL 3D+ and 3D Object datasets only measure the number
of correct viewpoint bins from bird-eye view. If the coarse viewpoint estimation
falls into the correct bin, we cannot observe further refinement using this metric.
Therefore, the improvements we present only represent the refinement of poses that
are initially estimated incorrectly.
This point was not explicit in the paper abd we will add it to our final paper. 

R1, RCNN + Ours: DPM-VOC+VP method templates were made from ground truth
bounding boxes so the bounding boxes tend to be tighter and more informative than
the region based bounding boxes (RCNN). Our algorithm handles over/under 
estimated bounding boxes by creating HOG scale pyramid but more accurate 
the bounding box is, the better the performance. This effect
is dominant for coarser viewpoint where RCNN and DPM-VOC+VP have similar
detection performance.

Sigma inversion time [R2]:
Sigma is a covariance matrix of size (W x H x F) x (W x H x F)
where W and H are the number of HOG cells in a row and a column, and F is the
dimension of HOG feature [Hariharan et al. 12]. In practice, we used
high-resolution template and the resulting covariance matrix was around
7000x7000 (~180MByte in single precision). Thus, using the Cholesky
decomposition, it took more than 4 seconds on i7-4770K. To get extra speed up,
we also tried to make use of the Toeplitz-Block-Toeplitz structure and achieved
O(n log n) time complexity using DFT but the time complexity coefficient was
too large and the non-zero pattern destroys the Toeplitz structure. We 
did not fully explain the size of the matrix [Sec.4] but will
incorporate this point in the final version.

The second point raised by [R2] is that the sigma matrix product can be done in GPU
implementation. We think the reviewer meant matrix decomposition since we
compared the matrix inversion time. We thank [R2] for correctly pointing this
out and we will incorporate a GPU implementation of the Cholesky decomposition
experiment in our final paper.

Related work from Zia el al. [R3]:
We thank the reviewer for pointing this out. We agree that Zia et
al. tackles the similar problem. However, due to the complexity, their
model requires accurate bounding box as well as viewpoint estimation as an 
initialization. On the other hand, our method can work as a standalone detector 
and performs on par with many state-of-the-art detectors on the 3D Object dataset
(though the dataset is saturated as correctly pointed out by [R1]).
We will add comparison with Zia et al on the final version.

We thank [R2] for pointing out writing errors and missing references. Although
our article is “well written” [R1] and “explains ... well” [R1], some minor errors
slipped through, which will of course be fixed in the final version.
We apologize for such mistakes.

We will try our best to incorporate all the remaining issues pointed out by the
reviewers in the final paper should it be accepted.
