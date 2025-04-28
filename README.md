# cs280-homework-2-solved
**TO GET THIS SOLUTION VISIT:** [CS280 Homework 2 Solved](https://www.ankitcodinghub.com/product/cs280-1-2/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;117354&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS280 Homework 2 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
In this problem, we will see how we can recover the 3D shape of an object given its image from two different viewpoints. In particular, given 2D point correspondences in the 2 images, we will estimate their 3D position in the scene and also estimate the camera positions and orientations.

1.1 Camera Models

Assume OXY Z is the global coordinate system in the 3D scene, while OcXcYcZc is the camera coordinate system.

(in global coordinates), and Xecam be the coordinates for the same point in the camera coordinate system. It holds that

Xecam = R(Xe − Ce) (1)

where Ce is the center of the camera in the global coordinate system and R is a 3×3 rotation matrix which describes the orientation of the camera coordinate system with respect to the global coordinate system.

If X is the 3D point in homogeneous coordinates (4th coordinate is 1) and x is the corresponding 2D point in the image, then

x X (2)

In case of two cameras, it is often easier to assume the global coordinate system to be same as the first camera’s coordinate system. In that case, P1 = K1[I|0] and P2 = K2[R|t].

1.2 Fundamental Matrix

The fundamental matrix F is a 3×3 matrix which relates corresponding points in stereo images. Assume x1 ↔ x2 are corresponding points in an image pair, then the following relation holds:

x = 0 (3)

Note that the fundamental matrix is of rank 2. (Why? – because Essential Matrix E is rank 2 and F is uncalibrated version of E)

1.3 The Essential Matrix

The essential matrix E relates calibrated corresponding image points, and it can be defined from the fundamental matrix as follows:

(4)

If P1 = K1[I|0] and P2 = K2[R|t], the essential matrix can also be written as

E = [t]xR (5)

where [t]x is the representation of the cross product with t. We can also show that the essential matrix is of rank 2 and has two identical real singular values while the third one is zero (as an optional exercise, you can try to prove it!). For more details refer to Chapter 7 in [1].

Eqn. 5 also tells us that knowing the essential matrix can allow us to estimate the camera orientation and center location as is described below.

1.4 Algorithms

In this section, we describe algorithms that are used to solve various problems related to the task of 3D reconstruction.

1.4.1 Eight-Point Algorithm

This algorithm fits the fundamental matrix defined by corresponding points x1 ↔ x2 in an image pair. In particular, assume points x ) in the first image corresponds to points x ) in the second image for i = 1,…,N. Note that, N ≥ 8, we need at least 8 corresponding points.

the origin), and scaling them by σ (so that the mean distance from the origin is a constant (e.g. 2)). Assume that the linear transformation described above is represented by the matrices T1 and T2 for the two images respectively.

Optimization. Eq. 3 can be rewritten equivalently as Af = 0, where f is formed from the entries of F stacked to a 9-vector row-wise and A is a N × 9 dimensional matrix. In particular, the i-th row of A is equal to

1] (6)

where the point coordinates have already been normalized, i.e. x ← Tx.

An approximate solution can be found by solving the following optimization problem

min ||Af||2 s.t. ||f||2 = 1 (7) f

which can be solved by using the singular value decomposition of matrix A.

The solution F∗ found by the approximately solving the problem Af = 0, does not guarantee that the fundamental matrix will be of rank 2. We can enforce this constraint, by solving another optimization problem:

min ||F − F∗||F s.t. rank(F) = 2 (8)

F

Again, this problem can be solved using the singular value decomposition of F∗. In particular, if F∗ = USV t, where S = diag(s1,s2,s3) and s1 ≥ s2 ≥ s3 then F = USVˆ t, where Sˆ = diag(s1,s2,0), is the matrix that solves the above optimization problem.

Denormalization. After enforcing the rank-2 constraint, we need to remove the normalization such that the fundamental matrix corresponds to points in the actual 2D image space, i.e. .

1.4.2 Estimating Extrinsic Camera Parameters from the Essential Matrix

Another problem is to estimate the extrinsic camera parameters, i.e. R,t for the second camera, when only the essential matrix E is known.

The operation [t]x can also be written as

[t]x = SZR90oSt (9)

where S = [s0 s1 t] is an orthogonal matrix, Z = diag(1,1,0) and R90o is the rotation matrix for rotation angle θ = 90o.

From Eq. 5

E = [t]xR = SZR90oStR = UΣV t (10)

Since we know that Σ = diag(1,1,0) (remember in homogeneous coordinates we define everything up to a multiplication factor), it holds that U = S and . Thus, t is the third left singular vector of E.

Thus, the direction of t as well as R can be determined by the SVD analysis of E. Notice that there is no way we can determine the actual norm of the vector t from just image point correspondences. Absolute values can only be determined if we have a known reference distance in the scene. In addition, the signs of both t and R also can not be determined from SVD decomposition. Therefore, this algorithm generates numerous candidate positions and orientations for the camera. You can also see Ch-7 of [1] for detailed explanation.

Different combinations of t and R result in different camera matrix P2 = K2[R|t]. After triangulation (3D reconstruction of the point cloud), the combination that gives the largest number of points in front of the image planes is selected.

1.4.3 Triangulation

Triangulation refers to the estimation of the 3D position of a point when the corresponding points in the two image planes are given as well as the parameters of the camera. In particular, assume x1 ↔ x2 are two corresponding points in the image plane and the camera matrices are P1 and P2 respectively. We want to find the 3D point X = (X,Y,Z,W) such that

x1 = P1X

Eq. 11 can also be written as: and x2 = P2X (11)

(12)

(13)

where j = 1,2 are the two camera indices and xj = (xj,yj).

The above system of non linear equations can be turned into a linear system, if both equations are multiplied by the denominators. The system will be homogeneous if the point in 3D is represented in homogeneous coordinates and thus can be solved via SVD. Alternatively, if we set W = 1 then the system is no longer homogenous and can be solved using least squares, i.e. by taking pseudo inverse by reducing it to AX = b where A and b are appropriate matrices.

1.5 3D reconstruction

In this assignment, we give you two sets: house and library. Since the intrinsic parameters of a camera are nowadays known and stored when a picture is taken, we provide the calibration matrices K1 and K2 for the pair of images in each example. In general, these parameters also need to be estimated via calibration when they are unknown. We also give you corresponding points for both pairs of images. In general, the corresponding points are found by detecting interest points in images and then comparing their descriptors across images to find matches.

Given a pair of images and their corresponding points as well as the intrinsic parameters for the two cameras, you will have to estimate the 3D positions of the points as well as the camera matrices. In particular, initially you will have to compute the fundamental matrix. You can implement the 8-point algorithm described above or any other algorithm you wish. Subsequently, you will estimate the extrinisic camera parameters of the second camera from the essential matrix. From all the possible combination of parameters, you will keep the one that results in most points in front of the two image planes. Last, you will plot the 3D points as well as the two camera centers. It is up to you how you want to show the point cloud.

1.5.1 Starter Code and Data

starter code/code/reconstruct 3d.m contains the starter code. This function is the main function and should output the points in the 3D space as well as the camera matrices. The input argument to this function is either ‘house’ or ‘library’ to select which dataset you want to use. starter code/data contains the image pairs and camera matrices for the house and the library. You will write the following four functions:

1. fundamental matrix.m: This function computes the fundamental matrix F given the data provided. It should return F as well as the residual res err. The residual is defined as the mean squared distance between the points in the two images and the corresponding epipolar lines. More precisely, if the fundamental matrix is F and the 2 corresponding points are x1 and x2, then the epipolar line corresponding to the point x2 in the first image is given by Fx2. So the distance between x1 and Fx2 is

The distance between x2 and Fx1 is similar. So the residual is

residual =

2. find rotation translation.m: This function estimates the extrinsic parameters of the second camera. The function should return a cell array R of all the possible rotation matrices and a cell array t with all the possible translation vectors. Deliverables: Your answer in your report should include – all possible choices for t and R for the 2 sample inputs.

3. find 3d points.m: This function reconstructs the 3D point cloud. In particular, it returns a N × 3 array called points, where N is the number of the corresponding matches. It also returns the reconstruction error rec err, which is defined as the mean distance between the 2D points and the projected 3D points in the two images. Deliverables: Your answer in your report should include – exactly how you calculate the reconstruction error, and reconstruction error for the 2 sample inputs

4. plot 3d.m: This function plots the 3D points in a 3D plot and displays the camera centers for both cameras. Plotting in 3D can be done using the plot3 command. A plot of the point cloud and the camera centers is enough for the purpose of the assignment. Note in this part, use that combination of R and t obtained in part-2 which gives the largest number of points in front of the image planes is selected. Deliverables: Your answer in your report should include – a plot for each of the 2 sample inputs from a reasonable viewpoint after selecting appropriate R and t

2 Instructions

1. You’re welcome to do the assignment in Python/NumPy instead of Matlab after re-implementing the (relatively simple) started code in Python/NumPy. If you do this, please maintain the same directory structure and implement all the functions in &lt;filename&gt;.py instead of &lt;filename&gt;.m.

2. Please submit the assignment using gradescope. Upload the following files:

(b) A tar/zip file. The file should be a folder with subdirectories for each coding problem, containing any code you wrote (in Matlab or Python) for the assignment.

4. This assignment should be done individually.

References

[1] Richard Szeliski. Computer vision: algorithms and applications. Springer, 2011.
