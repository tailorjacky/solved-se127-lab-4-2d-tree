Download Link: https://assignmentchef.com/product/solved-se127-lab-4-2d-tree
<br>
In this assignment, you will implement a special data structure called a 2D-Tree (short for “2-dimensional tree”) that efficiently supports to search “what value in the container is X most similar to?”.

<h1>1.  Story</h1>

At a high level, a kd-tree(short for “k-dimensional tree”) is a generalization of a binary search tree that stores points in k-dimensional space. That is, you could use a kd-tree to store a collection of points in the Cartesian plane, in three-dimensional space, etc. You could also use a kd-tree to store biometric data, for example, by representing the data as an ordered tuple, perhaps (height, weight, blood pressure, cholesterol). However, a kd-tree cannot be used to store collections of other data types, such as strings. Also note that while it’s possible to build a kd-tree to hold data of any dimension, all of the data stored in a kd-tree must have the same dimension. That is, you can’t store points in two-dimensional space in the same kd-tree as points in four-dimensional space.




It’s easiest to understand how a kd-tree works by seeing an example. Below is a kd-tree that stores points in three-dimensional space:




Notice that in each level of the kd-tree, a certain component of each node has been bolded. If we zeroindex the components (i.e. the first component is component zero, the second component is component one, etc.), in level n of the tree, the (n % 3)-th component of each node is shown in bold. The reason that these values are bolded is because each node acts like a binary search tree node that discriminates only along the bolded component. For example, the first component of every node in the left subtree is less than the first component of the root of the tree, while the first component of every node in the right subtree has a first component at least as a large as the root node’s. Similarly, consider the kd-tree’s left subtree. The root of this tree has the value (2, 3, 7), with the three in bold. If you look at all the nodes in its left subtree, you’ll notice that the second component has a value strictly less than three. Similarly, in the right subtree the second component of each node is at least three. This trend continues throughout the tree.




Given how kd-trees store their data, we can efficiently query whether a given point is stored in a kd-tree as follows. Given a point P, start at the root of the tree. If the root node is P, return the root node. If the first component of P is strictly less than the first component of the root node, then look for P in the left subtree, this time comparing the second component of P. Otherwise, then the first component of P is at least as large as the first component of the root node, and we descend into the right subtree and next time compare the second component of P. We continue this process, cycling through which component is considered at each step, until we fall off the tree or find the node in question. Inserting into a kd-tree is similarly analogous to inserting into a regular BST, except that each level only considers one part of the point.

<h1>2.  Lab Requirement</h1>

You should implement the TreeNode and BinaryDimonTree(2D-Tree) classes.

TreeNode is a class which is used to store the binary dimension data. You should provide the following functions (at least):

<ol>

 <li><strong>int getX()</strong>: return x(the first value in the tree node);</li>

 <li><strong>int getY()</strong>: return y(the second value in the tree node);</li>

</ol>

BinaryDimonTree is a class for the Tree which supports the following functions (at least):

<ol>

 <li><strong>BinaryDimonTree()</strong>: the construct function of class BDT;</li>

 <li><strong>istream &amp;operator&gt;&gt;(istream &amp;in, BinaryDimonTree &amp;tree)</strong>: input a 2D-Tree and the rule is given below;</li>

 <li><strong>TreeNode* find_nearest_node(int x, int y)</strong>: search the 2D-Tree and find the point whose distance is smallest to the Point(x, y), and output the result to the console;</li>

</ol>

p.s. the distance between Point(x1, y1) and Point(x2, y2) is equal to [(x1-x2)^2 + (y1y2)^2]^(1/2);

p.s. If there are two points that have the same distance to the Point(x, y), then you are supposed to choose the point whose x is smaller. If their x’s are also the same, then choose the point whose y is smaller;

<ol start="4">

 <li><strong>~BinaryDimonTree()</strong>: the deconstruct function which is used to reclaim all the data in the 2DTree, and you should explain your implementation to us when your lab is examined. You must implement the Tree completely by yourself. And <strong>the names of the classes and their functions must be same with the above</strong>.</li>

</ol>

We have provided the main function and the test cases, you should just run the main.cpp and check if you can pass through all the test cases.




<h1>3.  Guidance</h1>

The algorithm to find the nearest node in the 2D-Tree:

<strong>Let the test point be (a<sub>0</sub>, a<sub>1</sub>). </strong>

<strong>Maintain a global best estimate of the nearest neighbor, called ‘guess.’ Maintain a global value of the distance to that neighbor, called ‘bestDist’ Set ‘guess’ to NULL. </strong>

<strong>Set ‘bestDist’ to infinity. </strong>

<table width="553">

 <tbody>

  <tr>

   <td width="553"><strong>Starting at the root, execute the following procedure: </strong><strong>if curr == NULL return </strong><strong> </strong><strong>/*  </strong>*  <strong>If the current location is better than the best known location, * update the best known location. </strong><strong>*/ if distance(curr, guess) &lt; bestDist bestDist = distance(curr, guess) guess = curr </strong><strong> </strong><strong>/* </strong>*  <strong>Recursively search the half of the tree that contains the test point.  </strong>*  <strong>i means the dimension index which is used to discriminate in the current level,  </strong>*  <strong>for example: the i = 0 when curr is the root </strong><strong>*/ if a<sub>i</sub> &lt; curr<sub>i</sub> recursively search the left subtree on the next axis </strong><strong>else recursively search the right subtree on the next axis  </strong><strong>/* </strong>*  <strong>If the vertical distance between the points is smaller than the best distance,  </strong>*  <strong>look on the other side of the plane by examining the other subtree. </strong><strong>*/ if |curr<sub>i</sub> – a<sub>i</sub>| &lt; bestDist recursively search the other subtree on the next axis </strong></td>

  </tr>

 </tbody>

</table>

<strong><em> </em></strong>

<h1>4.  Test</h1>

Input &amp; Output Format:

The test file is divided into two parts.

The first part is for constructing a 2D-tree.

The first line contains an integer M which represents the number of nodes in the tree.

Next, there are M lines following, each contains two integers divided by a space. The two integers at the same line represent the values on two dimensions respectively for the corresponding node.




The second part contains the test cases for <strong>find_nearest_node</strong> method.

The first line contains an integer N which represents the number of test cases.

Next, there are M lines following, each contains four integers divided by spaces. In each line, the first two integers represent the node to search and the other two integers are correct answer of the search.




The code for the second part has been already completed in <strong>main.cpp</strong>. Please refer to the rules and construct your own 2D-tree.




Coding format：

<ol>

 <li>Please add your own functions and variables in file <strong>h</strong> and do not change or delete those functions with tag /* DO NOT CHANGE */. Do not include other headers or libraries.</li>

 <li>Please write your code in Tree.cpp and do not include other headers or libraries. 3. Do not modify <strong>cpp</strong></li>

</ol>




Submission：

<ol>

 <li>Please compress your source code into a 7z file and rename it to <strong>7z</strong>.</li>

 <li>Only <strong>h</strong> and Tree.cpp are supposed to be submitted.</li>

 <li>Upload it to canvas</li>

</ol>




Hint：

<ol>

 <li>1000 &lt;= M &lt;= 5000, 30000 &lt;= N &lt;= 100000。</li>

 <li>In real-world cases, search time is more important, so you are supposed to reduce the execution time of</li>

</ol>




<h1>5.  Example</h1>

Testcase 1:

7

0 0

-1 2

1 6

-1 1

-1 3

3 5

3 7

1

3 6 3 5




In this case, M=7 and N=1. You can construct a 2D tree with 7 nodes like this:

We have only one testcase, that is to find the point whose distance is smallest to Point(3,6). As both Point(3,5) and Point(3,7) have the same distance to Point(3,6), we choose Point(3,5) as it has smaller y.