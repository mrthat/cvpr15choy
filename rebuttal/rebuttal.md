We appreciate the valuable comments from all the reviewers. We're pleased that reviewers agreed our proposed method was “efficient”[R2,R3],  “well motivated”[R1], and validated with “extensive experiments”[R1], as well as demonstrating “considerable improvements to WHO”[R1] in terms of “speed”[R1,R3] and “detection performance”[R1].

Lack of novelty [R2]: we are quite surprised about R2’s ‘strong reject’ assessment due to missing novelty. We believe that both the main conceptual innovations of our paper: 1) training E-LDA template models on-the-fly from rendered CAD data, and 2) removing the need for calibration and speeding up WHO, are significant novel contributions. R1 believes they have the potential to ‘affect the broader recognition community as a whole’. Furthermore, we demonstrate how to exploit on-the-fly rendering and training for continuous viewpoint estimation using MCMC, which would be computationally prohibitive using offline training.

\begin{comment}
Contribution & caching templates [R1, R2]: Contribution in our paper is threefold: 1. WHO whitening speedup, 2. bypassing the expensive calibration stage with NZ-WHO, 3. on-the-fly template learning for continuous viewpoint estimation. These novelties enable us to generate rendering and learn calibrated template on-the-fly that makes MCMC procedure tractable. Thus we fine tune the viewpoint in continuous space without expensive training nor calibration, thus providing the vision community with a modular framework for continuous viewpoint estimation. Otherwise it would be intractable to cache and calibrate templates for continuous azimuths, elevations, in-plane rotations, focal lengths and intraclass CAD models.
\end{comment}

Number of templates [R1]: We partly agree. It is the problem inherent to all template-based-matching algorithm. However, we can reduce the number templates while maintaining the performance since we first use sparse viewpoints to initialize viewpoint and further optimize viewpoint continuously on-the-fly.

Effectiveness of fine-tuning [R1, R2]: Our continuous viewpoint estimation method not only accurately refines the coarse viewpoint estimation but also recovers from incorrect pose initializations. Unfortunately, the PASCAL 3D+ and 3D Object datasets only measure the number of correct viewpoint bins from a bird’s-eye view. If the coarse viewpoint estimation falls into the correct bin, we cannot observe further refinement using this metric. Therefore, the improvements only represent the recoveries of poses from grossly wrong estimations.

RCNN + Ours improvements [R1]: DPM-VOC+VP method templates were made from ground truth bounding boxes, so the bounding boxes tend to be tighter and more informative than the region-based bounding boxes (RCNN). Our algorithm handles over/under estimated bounding boxes by creating HOG scale pyramid but more accurate the bounding box is, the better the performance. This effect is dominant for coarser viewpoint where RCNN and DPM-VOC+VP have similar detection performance.

Calibration time [R1]: Yes, the calibration is a one-time process for each template (second column of Table.2). We followed the standard calibration technique [Aubry 14] and used 200k random negative patches for each template. The method calibrates each template independently.

Sigma inversion time [R2]: To enable on-the-fly template generation, we had to dramatically speed up the covariance inversion time and remove the calibration stage while maintaining the performance. Sigma is a covariance matrix of size (W x H x F) x (W x H x F) [Hariharan et al. 12] and is unique for each aspect ratio and foreground mask [Sec. 4.3]. In practice, we used high-resolution templates, resulting in a covariance matrix size of about 7000x7000 (~180MByte in single precision). Thus, it took ~4 seconds on i7-4770K to inverse matrix using the Cholesky decomposition.

The second point raised by [R2] is that the sigma matrix product can be done on GPU. We think the reviewer meant matrix decomposition since matrix product has been done on GPU using FFT and we compared the matrix inversion time only. We thank [R2] for correctly pointing this out and we will incorporate a GPU implementation of the Cholesky decomposition experiment in our final paper.

Related work from Zia et al. [R3]: We thank the reviewer for pointing this out. We agree that Zia et al. tackles the similar problem. However, due to the complexity, their model requires accurate bounding box as well as viewpoint estimation as an initialization. On the contrary, our method works also as a standalone detector and performs on par with many state-of-the-art detectors on the 3D Object dataset (though the dataset is saturated as correctly pointed out by [R1]). We will add comparison with Zia et al on the final version.

2 Classes [R2]: Unlike [Zia et al. PAMI 13](car,bike), [Hejrati el al. CVPR14](car) and [Fidler et al. NIPS12](car,box) we used the PASCAL challenge car class which exhibits large intraclass variation, from racing car to truck. Similarly, our bicycle class ranges from three-wheeled bicycles to acrobatic BMX bicycles. These classes are commonly found in real-world applications and include variability in viewpoint and intraclass appearance that allow us to fairly evaluate our method.

Saturated 3D Object [R1]: The AP results reported on Table 2 show some degree of saturation. However MPPE results show that it is still a challenging task and it evaluates the performance fairly since the dataset contains 480 images of cars from various poses and scales. Also the Table 2 has yet another significance that learning from synthetic images can be applied to real images. Also the qualitative results on Figure 7 on the paper and Figure 3. and 4 on the supplementary material are from the dataset and show that our algorithm can actually estimate 3D viewpoint accurately whereas other algorithms can only estimate rough geometry.

We thank [R2] for pointing out writing errors and missing references. Although our article is “well written” [R1] and “explains ... well” [R1], some minor errors slipped through, which will of course be fixed in the final version. We apologize for such mistakes.

6223/4000

-------------------------------------------------------------------------

R1's comments:
* Number of template evaluations [R1]: what do we want to say here? ...
* calibration time _per image_  [R1] - what are the runtimes reported in table 2? are they per image? if so, does _each of these_ runtimes contain the calibration time (I hope not)?
* in Tab. 3, I don't really see a difference in the performance of DPM-VOC-VP + fine-tuning and the corresponding RCNN-method - or am I missing something?

-------------------------------------------------------------------------

- R2's comment of lack of novelty: we have to strongly argue against that! we do have plenty of novelty, the most important one being the introduction of the on-the-fly rendering + template learning idea, that makes the MCMC procedure tractable! nobody has done that before!

- R2's concern about the speedup of WHO: 'why do we consider the inversion time at all' is not addressed! I can't see 'almost 4 seconds' in Tab. 1. also, our crucial argument is about the fact that we don't need _calibration_ in order to get good performance, and the speedup w/o considering calibration is not even very relevant?

- R2: we have to argue that making progress on 2 classes is already valuable (and give plenty of references that do that)

- R1's question about 1-time-calibration: is this incorporated in Tab. 1?
that's his question, so 'yes'! also, we have to argue that this in fact _not_ a 1-time-thing, but has to be repeated for templates of different sizes (as they arise all the time in our on-the-fly setting - we don't even know the dimensions beforehand)!

- R1's comment about the significance of the saturated results

----------------------Reviews not incorporated------------------------
From R1
“The work relies on using realistic (with texture) 3D models. This limits the applicability where such rich models are not available.”
“The proposed technique relies on a large number of templates, and their evaluation at many scales.”

From R2
“concerns about the reality of the speed-up” -- do some rough calculation about the naive approach to directly show the speedup of your method
“limited experiments”

From R3
“a little more background on WHO could be given”
“could be tested on KITTI”
“missing baseline”
