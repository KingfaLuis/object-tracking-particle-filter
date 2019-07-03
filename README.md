# Object tracking through a particle filter
Basic object tracker based on a particle filter

This GitHub repo contains the code for an object tracker built over a particle filter.  The code is a generic and simple implementation, with no specialized code for handling occlusion and target re-acquisition (this is a separate follow-up project).

The problem of object tracking is straightforward.  We select or are given an image patch, and as the video stream changes, we have to scan the frame and identify the most likely location of the original target.  We can do this by searching each location and matching against the reference object image.  But this is inherently inefficient, so we want to limit these locations to a smaller set of candidate locations deemed more likely to be the next object location (i.e., nearby pixels).  Even limiting to nearby pixels can still cause a huge calculation load (e.g., a 100x100 grid around the original location would mean checking 100,000 locations).  We can limit this further by conducting the selection based on approximations and probabilities and using a subset of these candidate locations.  This is exactly a job well suited to a particle filter.

> Side comment: On the other hand, object tracking is also a difficult problem.  The result of the comparison between the target image and a candidate image patch is sometimes unreliable and misleading, either confused by noise and irrelevant pixels or a limitation of the statistical comparison.  Losing the target is common, and in practice, the movement of the target and the behavior of objects near and around the target are unpredictable.  This leads to a complex segmentation and identification problem.  We brush aside these complications in this implementation.  We simply rely on pixel-wise (or some related pixel-based metric) comparisons as a measure of similarity.  We also set aside execution efficiency concerns, although under certain reasonable settings, the code is fast enough to track small movements in real time.

The code is a basic particle filter.  After grabbing a frame from a camera feed (e.g., the one attached to your desktop/laptop), the code extracts a small image patch in the middle of the frame.  The code then generates a number of particles, each of which represents a candidate location.  The particle with the best similarity –the code implements multiple types of similarity metrics—is used as the estimate for the image/object location in the following frame, repeated ad infinitum.

As a demonstrator, the code is limited in functionality, for example, there is no occlusion handling.  As a particle filter method, the code is also inherently subject to small errors which can accumulate over time.  This manifests as a slow deviation away from the original target image patch.  As a randomized prediction mechanism, it can also be affected by the choice of parameters that govern its capacity to recover from loss of tracking, for example, due to fast image movement.  Particle filters are also dependent on the number of particles and the number of sensor calculations.  However, increasing either (good for tracking fidelity) slows down execution, creating image lag (bad for tracking).

With all these said, enjoy the code.

这次下载下来，在电脑上的位置是
D:\code\object_detection\object-tracking-particle-filter
在我的环境之下就可以直接运行了
