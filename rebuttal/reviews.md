# Review 1

## Summary

This paper presents a fast synthesize and verify approach for 3D
object detection. It builds upon existing work in 2D object detection to
improve the detection speed. The proposed work provides 3D pose output in a
continuous output space and can also be used to augment output of existing 2D
detectors with rich pose information.

Main strengths

1. The paper is well written and explains the proposed technique well
2. The authors propose considerable improvements (both speed and detection performance) to the WHO approach of Hariharan et al. This I believe is their key contribution.
3. The proposed algorithm can be used on top of the output of existing 2D detection methods. 
4. As opposed to existing work on 3D detection, the presented work is much cleaner to understand and optimize.

Main weaknesses

1. The work relies on using realistic (with texture) 3D models. This limits the applicability where such rich models are not available.
2. The proposed technique relies on a large number of templates, and their evaluation at many scales. 
3. The finetuning approach presented is slow and doesn't seem
very effective

## Strength

The main contribution of this paper lies in thoroughly analyzing
the existing WHO approach and suggesting improvements to it. These improvements
are well motivated (both final detection results and theoretically, e.g. Fig 5)
The authors have performed extensive experiments to validate their approach,
comparing against all variations of WHO and justifying their insights. I think
this part of the work is very well done.

The proposed method shows considerable improvement over the existing state of
the art techniques. It is much simpler to understand and optimize than existing
techniques which is an added advantage.

Another good thing about this approach is that it can augment the output of 2D
detectors which is very valuable.

## Weakness

The main weakness of the proposed approach is with regard to the
number of explicit template evaluations needed to produce output. With this in
mind, the main question is scalability to a number of categories and detectors.

The MCMC fine tuning procedure isn't particularly effective at least when
compared to template evaluations required for it.

The results in Table 2 show saturation and thus their significance is limited.

## Rating & Reason

Weak Accept

I think this work is valuable for its contributions in Sections 4.2-4.4 which
affect the broader recognition community as a whole. However, the huge number
of template evaluations associated with the process make me doubt it's
scalability. Another issue is how applicable will your contributions in Sec
4.2-4.4 be for non-rendered training images (which have complex backgrounds).


## Rebuttal Request


I have the following questions for the authors

1. How did you account for calibration time per image in Table 1? Isn't calibration a one time process?
2. Why does fine tuning not improve RCNN at crude viewpoints (Table 3)? In fact, I thought crude viewpoints is where you would get most performance benefit. 
3. How significant are the results in Table 2 given that they are highly saturated in terms of AP?

# Review 2

## Summary

This paper presents a technique to efficiently compute WHO features, as well as
a simple variant of WHO to be used with rendered CAD models. It is validated in
a detection setup and used to perform pose estimation using detection provided
by another method. Despite the results on pascal 3d+, I don't think this paper
should be accepted for publication in cvpr because it lacks interesting content
and has writing issues beyond what is acceptable.

Strength:
- speeding up detector computation could be useful (but see concerns below)
- improvement of pose estimation on 2 classes of Pascal 3D dataset (but only 2) 

Weakness:
- Lack of novelty
- important writing issues
- concerns about the reality of the speed-up
- limited experiments

## Strength

- IMPROVEMENT OF WHO COMPUTATION This is a good idea and could be useful.
  However, I was not completely convinced by the results provided in the
  article for 2 reasons: 

    1. 0.1 second is not so fast
    2. almost 4 seconds for original WHO computation seems very bad. From the text, it seems to me that
        the authors considered the time of the inversion of Sigma. Since it can be
        done only once (or downloaded from internet) there is no reason to consider
        it! Also, a fair comparison would consider a GPU implementation of the
        (sparse) matrix product involved, and that would probably be extremely fast
        as well.

- POSE ESTIMATION ON PASCAL 3D+ This is a good dataset to report results in
  pose estimation, and improving the baseline is one of the strength of the
  paper. However, the strength of the dataset is that it has more than 10
  categories: why report results only on cars and bicycles?

## Weakness

- LACK OF NOVELTY I found only three very moderate novelties in the paper: 

    1. speed up of WHO computation (very moderate contribution + see concerns in the
        Strengths paragraph) 
    2. the introduction of Non-Zero WHO, which is only a
        very small variation of [1] which already has a mask to suppress background.
    3. using the model to refine an existing detection (very moderate
        contribution)

- WRITING the paper should be proof-read before submission, eg.

    * paragraph 4.1  reference missing (eg. l 674 "[]" 4.1 which rendering engine? which CAD
      models?)
    * proofread references (eg. [23])

SPEED-UP See Strength paragraph

LIMITED EXPERIMENTS Using only the 2 simplest classes on 12 available leads to
doubts about the robustness of the approach.

## Rating & Reason

Strong Reject

Despite the effort to provide many quantitative evaluations and the improvement
of some results on PASCAL 3D+, I don't think this paper can be published in
CVPR because it lacks any real novelty. The contributions are only very minor
modification of common methods.


## Rebuttal Request

- answer in details the concerns about the time reported for direct whitening
  computation.
- report results for other Pascal 3D+ classes or argue why they are not
  meaningfull for the paper


# Review 3


## Summary

The authors build on the idea of whitened histograms of orientations
(WHO) in order to perform close-to real time object detection and viewpoint
estimation. The idea is to generate discriminative viewpoint templates on the
fly by whitening the HOG templates generated by rendering CAD models. The
contribution of this paper is to 1.) whiten only the non-zero cells (which
avoids dealing with the background and thus negative images), and 2.) speed up
the original WHO by performing iterative Conjugate Gradient to whiten a matrix.
The obtained speed-up over WHO is two orders of magnitude. Given this fast
discriminative template generation the authors use an MCMC sampling method to
sample a set of possible poses, scales and focal lengths in order to find the
best fit of CAD models to the image (or bounding box). The method is tested on
3D Object Classes and Pascal3D showing that it clearly outperforms related
work.

plus:
- uses CAD models in an efficient way
- method can "train" from synthetic CAD renderings alone
- nice contribution
- fast inference
- good results

negative:
- a little more background on WHO could be given
- could be tested on KITTI
- missing baseline

## Strength

This is a nice paper that tackles an important problem in an efficient way. The
results are convincing.

## Weakness

The authors do test on two datasets, but it would be nice to see results on
KITTI which has good ground-truth for viewpoint estimation. Also several
related methods have been tested there.

While the method itself is different from Zia et al, they both tackle the
problem of viewpoint estimation in a similar way: generate proposals and fit
CAD models by sampling poses. It would be informative to compare both methods.

## Rating & Reason

Weak Accept

I like the idea of the paper and the results are convincing. It would be good
to compare to a related approach that uses CAD models, eg Zia et al.


## Rebuttal Request

N/A
