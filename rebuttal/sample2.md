We appreciate the valuable comments from all the reviewers. We are happy to
hear RWs agree that we address a “challenging problem” (R1) and propose an
“ambitious effort” (R1) through a “well-motivated” and designed method (R2). We
too believe this paper’s major strength is in its ability to solve activity
classification and object tracking problems in a coherent (joint) and
principled way. We believe we are among the first to address this. 

R1.1 : it needs to be evaluated carefully (layer by layer) We present such
evaluation in the Table.1. For example, the STL descriptors (denoted as
Isolated in Table1) are built upon the atomic activity labels from individuals,
so the isolated model can be thought of as a model that capture the direct
inference from atomic activities in isolation or connected with a HMM-like
chain for regularization (denoted as Chain in Table1). We show that naive chain
model does not provide much boost in the classification. 

R1.3 : Our  model “shows superior accuracy over the state-of-the-art methods”
(Page 2) but the “experiment setup in this paper is different from other
papers”.

We evaluate the accuracy of (collective) activity classification for the entire
scene (video), whereas [2][3] evaluate the classification accuracy for each
person (since their method is based on the STL descriptor which is applied to
each individual). We propose to present our results by transferring the
inferred scene (video) activity label to every individuals (line 696) which we
believe is a reasonable and fair way to compare our results with [2][3]. This
comparison indicates we achieve higher classification accuracy than [2][3].
Since [10] evaluate on single frame activity, we didn’t directly compare
against that work, but only report their results for completeness (line 698).
We will clarify this in the final version.

R3.1: built-in check mechanism in the framework so that errors won’t propagate
We don’t employ such a hard rule to identify and avoid error propagation in the
model. Instead, we introduce two types of complementary observations to avoid
error propagation: i) the global observation for collective activity (STL as in
[2][3]) and ii) individual observation for atomic activities (HoG and BoW).
These provide both (data-driven) top-down and bottom-up information for the
whole classification problem. E.g., the top-down information acts as an
“anchor” that helps avoid the collective activity to be associated to the wrong
labels. Experimental evaluation indicates that by using both top-down bottom-up
observations the system yields more stable and accurate (classification and
tracking) results than if these observations are used in isolation [xxx add
pointer to results in the paper].

R3.2 : How easy is it to apply the system to practical activity recognition
scenarios? That is a good point. In order to keep the model complexity
manageable, we assumed that there exists only one collective activity in a
scene at one time. This is a reasonable assumption in most cases, but there
might be some cases that such assumption does not hold. We are planning to
relax such assumption and allow multiple collective activities present in a
scene for a future direction. 

Even though interactions are noisy and might have a large degree of intra-class
variability as pointed and illustrated by R3, we show that they are still
useful and  help the overall recognition of the collective activity by
propagating bottom-up information. [xxx add pointer to results in the paper].
One possible extension to our work is to treat interactions as latent variables
and let the training algorithm find the best way to group interactions or
discover new latent interactions. This is an interesting direction for future
work.

We will try our best to incorporate all the remaining issues pointed out by the
reviewers to the final paper should it be accepted.
