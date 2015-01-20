We appreciate the valuable comments from all the reviewers. We are happy to
hear RWs agree that we address a

The paper present major improvements to the WHO approach (speed and performance) by thoroughly analyzing exisitn gWHO and performed extensive experiments to validate as pointed by [R1] and 


# Weakness


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

As [R2] pointed out, we thank [R2] for pointing out missing references. The final version will not have any writing issues.

# Ambiguity

## Calibration, Inversion one time process?

almost 4 seconds for original WHO computation seems very bad. From the text, it seems to me that the authors considered the time of the inversion of Sigma. Since it can be done only once (or downloaded from internet) there is no reason to consider it! Also, a fair comparison would consider a GPU implementation of the (sparse) matrix product involved, and that would probably be extremely fast as well [R2]

Rebuttal : The matrix $\Sigma \in \mathcal{R}^{(W\times H\times F) \times (W\times H\times F)}$ where $W$ is the number of HOG cells in width and $H$ is the number of HOG cells in the height and $F$ is the number of features which is 31 for HOG. Usually, the sigma matrix is about $7000 \times 7000$ for a specific template size and if you save it as a 4Byte double this takes 180MByte which is prohibitive. Not only the matrix is aspect ratio specific, but it also is specific for foreground mask. Our approach, which we experimentally validated, decorrelates only the foreground thus requires foreground mask specific sigma. Thus there is no way to cache/download the large matrix sigma. The other reviews [R1, R3] considered as a great improvement over WHO feature. The matrix is very dens due to the fact that the lines are usually continuous. All templates have different aspect ratio which cannot be cached nor downloadable. The inversion is unique for each template. We will emphasize  this point in the final paper.


## Variation of WHO.

almost 4 seconds for original WHO computation seems very bad. From the text, it seems to me that the authors considered the time of the inversion of Sigma. Since it can be done only once (or downloaded from internet) there is no reason to consider it! Also, a fair comparison would consider a GPU implementation of the (sparse) matrix product involved, and that would probably be extremely fast as well [R2]
Rebuttal : All templates have different aspect ratio which cannot be cached nor downloadable. The inversion is unique for each template.
analyzing the existing WHO approach and suggesting improvements to it. The authors have performed extensive experiments to validate their approach, comparing against all variations of WHO and justifying their insights. I think this part of the work is very well done. The proposed method shows considerable improvement over the existing state of the art techniques. It is much simpler to understand and optimize than existing techniques which is an added advantage. [R1]


