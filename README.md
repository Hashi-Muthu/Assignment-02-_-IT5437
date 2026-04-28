# Assignment-02-_-IT5437
This is to save the assignment
IT5437 Assignment 2 on Fitting and Alignment
Ranga Rodrigo
April 16, 2026
1. Table 1 shows the first five lines of the dataset in the file lines.csv. It represents three
points scatters conforming to three lines. The coordinates of the points are stored in columns
x1, x2, x3, y1, y2, and y3.
(a) Use total least squares to fit the lines to only using the data corresponding to the first
line. Report the resulting parameters.
(b) Now, use all the points as indicate in the code snippet below and fit three lines. Hint:
Run RANSAC to find a line, mask the consensus and run again and so on to find the
three lines
D = np. genfromtxt (" lines .csv ", delimiter =",", skip_header =1)
X_cols = D[:, :3]
Y_cols = D[:, 3:]
X_all = X_cols . flatten ()
Y_all = Y_cols . flatten ()
Table 1: First five rows of the dataset
x1 x2 x3 y1 y2 y3
-5.3055 -4.0601 -5.2613 -12.6663 -3.7962 3.6917
-5.5404 -5.0032 -3.9926 -11.0077 -3.9856 4.9000
-4.9821 -4.5845 -4.3312 -11.6973 -3.5893 5.0469
-4.4957 -5.0641 -4.7820 -11.9780 -3.5971 4.6359
-4.4422 -4.4114 -4.5675 -12.4150 -2.7995 4.7397
2. Fig. 1 shows an image ofa pair of earrings. Assume that a camera is mounted with the
optical axis perpendicular to the imaging plane (where the flat earrings are kept). If the
focal length of the camera is 8mm, the pixel size is 2.2 μm×2.2 μm, and the distance from
the lens to the imaging plane is 720mm, what are the sizes of the earrings?
3. Fig. 2 two circuit boards1. Listing 1 shows a code snippet that can be used to click and obtain
the four corners. It is possible to transform the image of one circuit board to the perspective
of the other using the homography transformation. This can be used to find the differences
between the two circuit boards. Perform the following steps:
(a) Manually click about 6 corresponding points in each circuit board, compute the homography,
and warp one image to the perspective of the other. Display the warped
image.
(b) Subtract the warped image from the other image to find the differences between the
two circuit boards. Display the difference image.
1In fact, the two images are of the same circuit board, manually transfromed.
1
Figure 1: Earrings.
(c) Use SIFT or ORB to find keypoints and descriptors in both images, match the descriptors,
and display the matches. You can use OpenCV functions for this purpose.
(d) Use the matches to compute a homography and warp one image to the perspective of
the other. Display the warped image and the difference image as in steps (a) and (b).
Compare the results with those obtained in steps (a) and (b). Discuss any differences
in the results and possible reasons for those differences.
(a) Circuit board c1. (b) Circuit board c2.
Figure 2: Two circuit boards.
Listing 1: Code for clicking a quadrangle.
import cv2 as cv
import numpy as np
N = 5
global n
n = 0
p1 = np. empty ((N ,2) )
2
p2 = np. empty ((N ,2) )
DISPLAY_W , DISPLAY_H = 900 , 650
# mouse callback function
def draw_circle (event ,x,y,flags , param ):
global n
p = param [0]
if event == cv. EVENT_LBUTTONDOWN :
cv. circle ( param [1] ,(x,y) ,5 ,(255 ,0 ,0) ,-1)
p[n] = (x,y)
n += 1
im1 = cv. imread (’a2_images /c1. jpg ’, cv. IMREAD_REDUCED_COLOR_4 )
im2 = cv. imread (’a2_images /c2. jpg ’, cv. IMREAD_REDUCED_COLOR_4 )
im1copy = im1. copy ()
im2copy = im2. copy ()
cv. namedWindow (’Image 1’, cv. WINDOW_AUTOSIZE )
param = [p1 , im1copy ]
cv. setMouseCallback (’Image 1’,draw_circle , param )
while (1) :
cv. imshow (" Image 1", im1copy )
if n == N:
break
if cv. waitKey (20) & 0xFF == 27:
break
param = [p2 , im2copy ]
n = 0
cv. namedWindow (" Image 2", cv. WINDOW_AUTOSIZE )
cv. setMouseCallback (’Image 2’,draw_circle , param )
while (1) :
cv. imshow (" Image 2", im2copy )
if n == N:
break
if cv. waitKey (20) & 0xFF == 27:
break
print (p1)
print (p2)
GitHub Profile
You must include the link to your GitHub (or some other SVN) profile, so that I can see that you
have worked on this assignment over a reasonable duration. Therefore, make commits regularly.
However, I will use only the pdf for grading to save time.
Submission
Upload a report (four pages or less) named as your_index_a02.pdf. Include the index number and
the name within the pdf as well. The report must include important parts of code, image results,
3
and comparison of results. The interpretation of results and the discussion are important in the
report. Extra-page penalty is 20 marks per page.
