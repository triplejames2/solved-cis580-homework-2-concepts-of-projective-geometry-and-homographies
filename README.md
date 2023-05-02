Download Link: https://assignmentchef.com/product/solved-cis580-homework-2-concepts-of-projective-geometry-and-homographies
<br>
Homework 2

Barcelona

Introduction

In this programming assignment, we will use the concepts of projective geometry and homographies to allow us to project an image onto a scene in a natural way that respects perspective. To demonstrate this, we will project our logo onto the goal during a football match. For this assignment, we have provided images from a video sequence of a football match, as well as the corners of the goal in each image and an image of the Penn Engineering logo. Your task is, for each image in the video sequence, compute the homography between the Penn logo and the goal, and then warp the goal points onto the ones in the Penn logo to generate a projection of the logo onto the video frame (e.g. Figure 1)

<h2><img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/05/572.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/05/572.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript><span style="font-size: 2em">Technical Details</span></h2>

The Python script <strong>project logo.py </strong>will be the main script to run this assignment. In this script, we provide you the following:

<ul>

 <li>A sequence of images onto which you will project a logo image.</li>

 <li>The corners in each video frame that the logo should project onto.</li>

 <li>The logo image itself.</li>

</ul>

Your goal will be to complete the functions <strong>est homography </strong>and <strong>warp pts </strong>in their respective .py files. <strong>est </strong><strong>homography </strong>estimates the homography that maps the video image points onto the logo points (i.e. <strong>x</strong><em><sub>logo </sub></em>∼ <strong>x</strong><em><sub>video</sub></em>), and <strong>warp pts </strong>then warps the sample points according to this homography, returning the warped positions of the points (that is, the corresponding points in the logo image). We then use these correspondences to copy the points from the logo into the video image. Once you finish these two functions, change your current directory to the directory of “Part 1”, and run “python project logo.py”. It will use the two functions you completed to project logo, visualize them in a video, and save sampled results.

<h2>1.3         Homography Estimation</h2>

To project one image patch onto another, we need, for each point inside the goal in the video frame, to find the corresponding point from the logo image to copy over. In other words, we need to calculate the homography between the two image patches. This homography is a 3×3 matrix that satisfies the following:

<strong>x</strong><em>logo </em>∼<em>H</em><strong>x</strong><em>video                                                                                                                  </em>(1)

Or, equivalently:

<em>λ</em><strong>x</strong><em>logo </em>=<em>H</em><strong>x</strong><em>video                                                                                                                   </em>(2)

Where <strong>x</strong><em><sub>logo </sub></em>and <strong>x</strong><em><sub>video </sub></em>are homogeneous image coordinates from each patch and <em>λ </em>is some scaling constant. To calculate the homography needed for this projection, we provide, for each image, the corners of the patches that we would like you to warp between in each image. You must calculate the homography using the provided corner points and the technique covered in the lectures and Appendix A. You can then warp each image point using <em>H </em>to find its corresponding point in the logo (note that the homography equation is estimated up to a scalar, so you will need to divide <em>H</em><strong>x</strong><em><sub>image </sub></em>by the third term, which is <em>λ</em>), and then return the set of corresponding points as a matrix.

<h2>1.4         Inverse Warping</h2>

You may be wondering why we are calculating the projection from the video frames to the logo image, when we want to project the logo image onto the video frames. We do this because, if we compute the inverse homography, and project all the logo points into the video frame, we will most likely have the case where multiple logo points project to one video frame pixel (due to rounding of the pixels), while other pixels may have no logo points at all. This results in ’holes’ in the video frame where no logo points are mapped. To avoid this, we calculate the projection from video frame points to logo points to guarantee that every video frame gets a point from the logo.

We can then replace every point in the video frame (<strong>x</strong><em><sub>video</sub></em>) with the corresponding point in the logo (<strong>x</strong><em><sub>logo</sub></em>) using the correspondences (<strong>x</strong><em><sub>image</sub>,</em><strong>x</strong><em><sub>logo</sub></em>). This is already done for you in <strong>inverse warping</strong>, and you should not need to change it.

<h2>1.5         Files to complete and submit</h2>

<ol>

 <li><strong>est homography.py</strong></li>

</ol>

This function is responsible for computing the homography given correspondence

<h3>2.    warp pts.py</h3>

This function is responsible for computing the warped points given correspondence and a set of sample points

<h2>1.6         Visualizing Results</h2>

To play the projected images as a video, run the <strong>project logo.py </strong>script. First open a terminal window and change the current directory to the directory of “Part 1”. Then run command:

<strong>python project logo.py</strong>

You can also use an IDE to run the script. If you would like to play with your own data, you can edit <strong>project logo </strong>and generate your own video with a set of points.

<h2>1.7         Appendix A: Calculating Homographies</h2>

As we learned in the lectures, a homography <em>H </em>maps a set of points <strong>x </strong> to another set of points <strong>x</strong> up to a scalar:

<table width="0">

 <tbody>

  <tr>

   <td width="374"><strong>x</strong><sup>0 </sup>∼<em>H</em><strong>x</strong></td>

   <td width="48">(3)</td>

  </tr>

  <tr>

   <td width="374"></td>

   <td width="48">(4)</td>

  </tr>

  <tr>

   <td width="374"><em>λx</em>0 =<em>h</em>11<em>x </em>+ <em>h</em>12<em>y </em>+ <em>h</em>13</td>

   <td width="48">(5)</td>

  </tr>

  <tr>

   <td width="374"><em>λy</em>0 =<em>h</em>21<em>x </em>+ <em>h</em>22<em>y </em>+ <em>h</em>23</td>

   <td width="48">(6)</td>

  </tr>

  <tr>

   <td width="374"><em>λ </em>=<em>h</em>31<em>x </em>+ <em>h</em>32<em>y </em>+ <em>h</em>33</td>

   <td width="48">(7)</td>

  </tr>

 </tbody>

</table>

In order to recover <em>x</em><sup>0 </sup>and <em>y</em><sup>0</sup>, we can divide equations (5) and (6) by (7):

(8)

(9)

Rearranging the terms above, we can get a set of equations that is linear in the terms of <em>H</em>:

<table width="0">

 <tbody>

  <tr>

   <td width="561">−<em>h</em>11<em>x </em>− <em>h</em>12<em>y </em>− <em>h</em>13 + <em>h</em>31<em>xx</em>0 + <em>h</em>32<em>yx</em>0 + <em>h</em>33<em>x</em>0 =0</td>

   <td width="28">(10)</td>

  </tr>

  <tr>

   <td width="561">−<em>h</em>21<em>x </em>− <em>h</em>22<em>y </em>− <em>h</em>23 + <em>h</em>31<em>xy</em>0 + <em>h</em>32<em>yy</em>0 + <em>h</em>33<em>y</em>0 =0Finally, we can write the above as a matrix equation:</td>

   <td width="28">(11)</td>

  </tr>

 </tbody>

</table>

=0                                                                             (12)

Where:

(13)

(14)

(15)

Our matrix <em>H </em>has 8 degrees of freedom, and so, as each point gives 2 sets of equations, we will need 4 points to solve for <em>h </em>uniquely. So, given four points (such as the corners provided for this assignment), we can generate vectors <em>a<sub>x </sub></em>and <em>a<sub>y </sub></em>for each, and concatenate them together:

 <em>a</em><em>x,</em>1 

 <em>a</em><em>y</em><sub>1 </sub>

       …                                                                    (16)

<em>A </em>= 

 <em>a</em><em>x,n </em>



<em>a</em><em>y,n</em>

Our problem is now:

<em>Ah </em>= 0                                                                                             (17)

As <em>A </em>is a 8×9 matrix, there is a unique null space. Normally, we can use MATLAB’s <strong>null </strong>function, however, due to noise in our measurements, there may not be an <em>h </em>such that <em>Ah </em>is exactly 0. Instead, we have, for some small <em>~</em>:

(18)

To resolve this issue, we can find the vector <em>h </em>that minimizes the norm of this <em>~</em>. To do this, we must use the SVD, which we will cover in week 3. For this project, all you need to know is that you need to run the command:

[U, S, V] = svd(A);

The vector <em>h </em>will then be the last column of <em>V </em>, and you can then construct the 3×3 homography matrix by reshaping the 9×1 h vector.

<h1>2           Invictus vs Harleysville – 50 pts</h1>

<h2>2.1         Introduction</h2>

In this programming assignment, we will use the concepts of projective geometry and vanishing points to project a virtual line that would be parallel as seen from above. We have provided a video sequence, as well as the relevant annotations. The task is to compute the vanishing point then find the line segment in the image that represents the referee’s location on the field. (e.g. Figure 2)

Figure 2: Example of the referee’s line (blue) projected onto the field.

<h2>2.2         Technical Details</h2>

The Python script <strong>visualize ref line.py </strong>will be the main script for this question. We provide the following:

<ul>

 <li>A sequence of images onto which you will draw the referee’s line</li>

 <li>All annotated points (referee and 4 field points)</li>

 <li>Drawing utilities for all points</li>

</ul>

<h2>2.3         Data given</h2>

Figure 3 shows the layout of the provided keypoints as seen from a top down perspective. The mappings from figure to code are as follows:

<ul>

 <li>lower left keypoint</li>

 <li>lower right keypoint</li>

 <li>upper right keypoint</li>

 <li>upper left keypoint</li>

 <li>referee keypoint</li>

</ul>

Figure 3: Supplied keypoints for each frame.

<h2>2.4         Files to complete and submit</h2>

<ol>

 <li><strong>line from pts.py</strong></li>

</ol>

This function is responsible for computing the line that passes through two points in P<sup>2</sup>

<ol start="2">

 <li><strong>line intersection.py</strong></li>

</ol>

This function is responsible for computing the intersection between two lines in P<sup>2</sup>

<h3>3.    compute ref line segment.py</h3>

This function is responsible for computing the referee’s position on the field, represented as two end points (on either side of the field).

<h2>2.5         Visualizing Results</h2>

To visualize the results as a video, run the <strong>visualize ref line.py </strong>script. First open a terminal window and change the current directory to the directory of “Part 2”. Then run command:

<strong>python visualize ref line.py </strong>You can also use an IDE to run the script.