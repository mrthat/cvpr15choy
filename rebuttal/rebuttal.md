We appreciate the valuable comments from all the reviewers. We are happy to
hear reviewers agree that we proposed “efficient”[R2,R3] and “considerable
improvements to WHO”[R1] in terms of “speed”[R1,R3] and “detection
performance”[R1]. The method was “well motivated”  was validated with
“extensive experiments”[R1].

R1.1 & [R2 one-time]: Our method proposed a way to fine tune the viewpoint in
continuous space without expensive training thus providing vision community a
modular framework for view estimation. However, caching all possible templates
would be intractable and difficult to cover continuous azimuth, elevation,
in-plane rotation, focal length and intraclass CAD models. To overcome, our
method generates proposals on-the-fly which requires covariance inversion which
we handled by Conjugate Gradient.

R1 & R2, effectiveness of fine-tuning: The continuous viewpoint estimation not
only recovers from wrong pose but also accurately refine the viewpoint.
Unfortunately, the PASCAL 3D+ and 3D Object datasets only measures the number
of correct viewpoint bins from bird-eye view. If a viewpoint estimation fall
into the correct bin in the coarse estimation, the improvement from the
fine-tuning cannot be measured. So the improvements comes from the fine-tuning
measured using the criteria is the number of recovers from wrong initialization
only. We will explain this point in our final paper. 

R1, RCNN + Ours: DPM-VOC+VP method templates are made from ground truth
bounding boxes so the bounding boxes are more tight and informative compare to
region based bounding boxes (RCNN). Our algorithm tries to handle such
incorrect bounding boxes by creating HOG scale pyramid for the given bounding
box but more accurate the bounding box is, better the performance. This effect
is dominant for coarser viewpoint where RCNN and DPM-VOC+VP have similar
performance.

R2, inversion time: Sigma is a covariance matrix of size (W x H x F) x (W x H x
F) where W and H are the number of HOG cells in a row and a column, F is the
dimension of HOG feature [Hariharan et al. 12]. In practice, we used
high-resolution template and the resulting covariance matrix was around
7000x7000 (~180MByte in single precision). Thus, using the Cholesky
decomposition, it took more than 4 seconds on i7-4770K. To get extra speed up,
we also tried to make use of the Toeplitz-Block-Toeplitz structure and achieved
O(n log n) time complexity using DFT but the time complexity coefficient was
too large and the non-zero pattern destroys the Toeplitz structure so we did
not incorporated in our paper. We did not emphasize this point in detail
[Sec.4] but will try to incorporate this point in the final version.

Second point raised by [R2] is that the sigma matrix product can be done in GPU
implementation. We think the reviewer meant matrix decomposition since we
compared the matrix inversion time. We thank [R2] for correctly pointing this
out and we will incorporate GPU implementation of Cholesky decomposition
experiment in our final paper.

R3, Zia el al.: We thank the reviewer for point this out. We agree that Zia et
al. tackles the similar problem. However, due to their complex model, their
model requires accurate bounding box and viewpoint estimation. On the other
hand, our method can work as a standalone detector and performs on par with
many state-of-the-art detectors though the dataset is saturated as correctly
pointed by [R1]. But we think this is a good comparison and we will add
discussion and comparison with Zia et al on the final version.

We thank R2 for pointing out writing errors and missing references. Although
our article is “well written”[R1] and “explains ... well”[R1], we also noticed
the errors and fixed them including the ones pointed out by R2. We apologize
for such mistakes.

We will try our best to incorporate all the remaining issues pointed out by the
reviewers to the final paper should it be accepted.
