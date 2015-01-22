
## Scalability [R1]

* The proposed technique relies on a large number of templates, and their evaluation at many scales. [R1]
* questionable scalability to a number of categories and detectors[R1]

## Realistic Textured Model as oppose to Simple Geometric Model

* The work relies on using realistic (with texture) 3D models. This limits the applicability where such rich models are not available. [R1]
* Uses CAD model only for training[R3]


## Effectiveness of Fine Tuning [R1]

This gives the user degree of accuracy they aim

* The finetuning approach presented is slow and doesn't seem very effective.[R1]


# More experiments

## Limited PASCAL 3D+ Experiments

* Good dataset to measure the performance. but limited number of categories [R2]

    [Zia et al PAMI13]

## Other Dataset

* Zia et al.[R3]
* KITTI which has good ground-truth for viewpoint estimation[R3]


# Saturated Result on Table 1

* The results in Table 2 show saturation and thus their significance is limited.[R1]


# Modularity, Work with Existing Detectors

* The proposed algorithm can be used on top of the output of existing 2D detection methods.[R1]
* it can augment the output of 2D detectors which is very valuable.[R1]
* Using the model to refine an existing detection (very moderate contribution)[R2]


## Improvements over WHO

* The authors propose considerable improvements (both speed and detection performance) to the WHO approach of Hariharan et al. This I believe is their key contribution. [R1]
* Comparing against all variations of WHO and justifying their insights[R1]
* The proposed method shows considerable improvement[R1]
* Cache inverse sigma (this point is wrong explain) [R2]
* GPU implementation of the (sparse) matrix product involved, and that would probably be extremely fast as well.[R2]??? Don't understand what he wants
* Minor improvement of WHO when mask exists[R2]
* whiten only the non-zero cells (which avoids dealing with the background and thus negative images)[R3]
* speed up the original WHO by performing iterative Conjugate Gradient[R3]

## Writing [R2]

* The paper is well written and explains the proposed technique well [R1]
As [R2] pointed out, we thank [R2] for pointing out missing references. The final version will not have any writing issues.

## Ease of Use

* As opposed to existing work on 3D detection, the presented work is much cleaner to understand and optimize. [R1]

# Ambiguity

* More elaboration on WHO [R3]


## Calibration, Inversion one time process?

almost 4 seconds for original WHO computation seems very bad. From the text, it seems to me that the authors considered the time of the inversion of Sigma. Since it can be done only once (or downloaded from internet) there is no reason to consider it! Also, a fair comparison would consider a GPU implementation of the (sparse) matrix product involved, and that would probably be extremely fast as well [R2]


# Explicit Rebuttal Requests

- Reviewer 1

    1. How did you account for calibration time per image in Table 1? Isn't calibration a one time process?
    2. Why does fine tuning not improve RCNN at crude viewpoints (Table 3)? In fact, I thought crude viewpoints is where you would get most performance benefit. 
    3. How significant are the results in Table 2 given that they are highly saturated in terms of AP?

- Reviewer 2

    1. answer in details the concerns about the time reported for direct whitening
      computation.
    2. report results for other Pascal 3D+ classes or argue why they are not
      meaningfull for the paper



