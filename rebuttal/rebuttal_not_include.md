



Another request from [R2] was to use sparse approximation of the matrix and compute product. We also interpreted as sparse matrix decomposition. This is an interesting question but unfortunately, the nature of the matrix sigma prohibits such approximation. The matrix is composed of second order correlation between all HOG bins. The second order correlation usually exists very strongly for at least 5~8 HOG cells from the reference cell and most of cells fall within the range, the matrix sigma is very dense. All templates have different aspect ratio which cannot be cached nor downloadable. The inversion is unique for each template. We will emphasize  this point in the final paper.


Since we focused on continuous viewpoint fine-tuning, the sigma is unique for specific aspect ratio and, in our approach, the sigma is also unique for each foreground pattern. Since creating all combination of fine pose and model is intractable, we proposed on-the-fly NZ-WHO template generation and each template generation requires unique sigma matrix and inversion. This point was not emphasized [Sec.4] and we will add this in the final version.

S




## Scalability [R1]

This gives the user degree of accuracy they aim


## Realistic Textured Model as oppose to Simple Geometric Model


## Effectiveness of Fine Tuning [R1]

This gives the user degree of accuracy they aim


## Limited PASCAL 3D+ Experiments

- This is a good dataset to report results in pose estimation, and improving
  the baseline is one of the strength of the paper. However, the strength of
  the dataset is that it has more than 10 categories: why report results only
  on cars and bicycles?[R2]


Another good thing about this approach is that it can augment the output of 2D detectors which is very valuable.[R1]


## Writing [R2]



Also for [R1] 

# Modularity, Work with Existing Detectors

Able to use existing 2D framework can be a strength as pointed out by [R1, R3] but only can be viewed as refining an existing detection[R2]. However, these popular 2D detectors cannot predict the pose, closest CAD models, the intraclass nor the depth information. Our modular framework, however, augment the bounding boxes with rich metadata.

* The proposed algorithm can be used on top of the output of existing 2D detection methods.[R1]
* it can augment the output of 2D detectors which is very valuable.[R1]

## Calibration, Inversion one time process?

One the of main weakness raised by [R2] was that the inverse of the sigma can be cached or downloaded. Unfortunately the matrix sigma has size (W x H x F) x (W x H x F) where W and H are the number of HOG cells in width and height respectively F is the dimension of HOG feature [Hariharan et al. 12] and, in practice, it is around 7000 by 7000. In double precision, each sigma takes more than 180MByte, too large to cache or download all possible sigmas. The sigma is unique for specific aspect ratio and, in our approach,  the matrix is also unique for each foreground pattern. Since creating all combination of fine pose and model is intractable, we proposed on-the-fly NZ-WHO template generation and each template generation requires unique sigma matrix and inversion. This point was not emphasized [Sec.4] and we will add this in the final version.

Second point raised by [R2] is that the sigma matrix product can be done in GPU implementation. We think the reviewer meant matrix decomposition since the matrix inversion is the bottleneck that we discussed in Figure.4 and 5. We thank [R2] for pointing this out and will incorporate the experiment on the final paper. 

Another request from [R2] was to use sparse approximation of the matrix and compute product. We also interpreted as sparse matrix decomposition. This is an interesting question but unfortunately, the nature of the matrix sigma prohibits such approximation. The matrix is composed of second order correlation between all HOG bins. The second order correlation usually exists very strongly for at least 5~8 HOG cells from the reference cell and most of cells fall within the range, the matrix sigma is very dense. All templates have different aspect ratio which cannot be cached nor downloadable. The inversion is unique for each template. We will emphasize  this point in the final paper.

## Experiments

[R3] suggested comparing 

 [R1]

We thank [R1] for pointing out the saturated performance of Table.1. We agree with reviewer that the AP is saturated. This experiment was meant to measure the performance of NZ-WHO templates as a standalone detector for sanity check. We will emphasize this point in the final version. 


## Variation of WHO.

almost 4 seconds for original WHO computation seems very bad. From the text, it seems to me that the authors considered the time of the inversion of Sigma. Since it can be done only once (or downloaded from internet) there is no reason to consider it! Also, a fair comparison would consider a GPU implementation of the (sparse) matrix product involved, and that would probably be extremely fast as well [R2]
Rebuttal : All templates have different aspect ratio which cannot be cached nor downloadable. The inversion is unique for each template.
analyzing the existing WHO approach and suggesting improvements to it. The authors have performed extensive experiments to validate their approach, comparing against all variations of WHO and justifying their insights. I think this part of the work is very well done. The proposed method shows considerable improvement over the existing state of the art techniques. It is much simpler to understand and optimize than existing techniques which is an added advantage. [R1]


We thank [R2] for pointing out missing references. The final version will not have any missing references.



