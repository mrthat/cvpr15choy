Not everything here applies to a CV conference (e.g., no metareviewer AC here),
but here’s the process I recommend for my students: Copy/paste all reviews into
a GDoc and share with your collaborators At the top of the GDoc, create a
bulleted list of high-level feedback that you aggregate across the reviews.
Under each theme bullet, copy paste quotes from R1, R2, R3 and AC that are
arguing the point. Rank order the importance of each piece of feedback. Pay
attention to the associate chair (AC)’s metareview --- they are very important.
Add your own sub-bullet points to air your own thoughts on each of the major
points of critique. Can we respond thoughtfully to this critique? After talking
with me about the high-level points and responses, draft a rebuttal in the GDoc
where you focus only on the most important points. Then iterate with me on it.
Below is an example rebuttal, from Ethan’s DeduceIt UIST paper. Remember you
have very limited space, typically about one page.

~~~~
We’d like to thank the reviewers for their insights. We’ll focus on
questions of related work, interface novelty, and assignment creation,
and address all other feedback directly.

RELATED WORK
R1 wonders whether our references are too old to be relevant, echoed by
AC1 and AC2. This is a good insight, and we will integrate discussion of
more recent contributions including Burstall, Back, Bornat and others
into our paper. There are two classes of this related work. One class of
modern work (e.g., Weidenbach) focuses on optimizations in more elaborate
theories. This is valuable but largely unnecessary for our assignments.
The second class of work (e.g., ProveEasy) is more pedagogically oriented
but grounds all proofs in complete formalisms. In contrast, DeduceIt aims
to support many (incomplete) formalisms at just enough depth for students
to explore. DeduceIt’s rewrite languages are much smaller, with rules
tailored to each assignment; complex rules that are difficult to
implement generally can be handled via assignment-specific rewrite rules,
providing students with an illusion of working in the general theory. For
this reason, DeduceIt is not limited in the exercises it supports, and it
can handle induction principles, higher-order and modal logics (R1). We
agree that the suggested related work is valuable, and we’ll revise our
paper to reflect this discussion.

INTERFACE NOVELTY
R1 and AC1 suggest we further articulate our user interface
contributions. DeduceIt contributes novel interfaces for grading systems
in online education. Foremost is the ability to aggregate students’
solution processes into a (proof) tree for analytics. Instructors can
view and navigate proof trees, benefitting from insights into students’
understanding of assignment domains. This analysis leads to course
improvements — as R3 suggests, we will add more specific examples in
revision. Further, DeduceIt allows instructors to annotate nodes of a
proof tree with hints; these are typically added for common errors,
easily detectable since the tree tells an instructor how many students
have traversed a given faulty path. Hints also present a novel interface
from the student perspective by providing context-specific help.

ASSIGNMENT CREATION
RC2 and AC1 worry that “the main weakness of the system is the complexity
of the rule language and the rules.” We agree that setting up rulesets is
DeduceIt’s most involved task. However, DeduceIt is for pedagogical
purposes and not for large, general proofs, and we’ve found instructors
do not need support for completeness, correctness, and consistency (R2,
AC1) because its rewrite languages are so small. As a result, the
simplicity of most assignment languages makes debugging fairly
straightforward (R2). In practice, assignments take between 5 and 30
minutes to prepare and up to another 30 to test (as reported by our TA).
This time is short because instructors implement rules necessary for a
given exercise, not a complete formalism: e.g., example for Regular
Expressions II at http://i.imgur.com/5cUXdJ3.png, which we will include
in the paper. Also, as we discuss in the paper, rewrite languages can be
shared and copied across similar assignments. DeduceIt could easily
provide a “standard library” of rewrite languages for common assignment
types. We will revise the paper to add further discussion of assignment
authoring (AC2). 

CONCLUSION
Our work contributes a novel solution for online assignments that cannot
be multiple-choice. We suggest our work should not be compared against
high-end theorem provers; they solve a different problem for a different
audience and represent a poor solution to our problem. As reviewers
suggest, strengths of this paper include its clear presentation, solid
evaluation, and potential to spark additional work in an important area
of research. We’d like to thank the reviewers again for their time and
effort, and we hope they agree this paper merits inclusion in UIST.
