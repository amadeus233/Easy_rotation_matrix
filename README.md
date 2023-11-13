# Easy_rotation_matrix

##Insights into matrix rotation type questions encountered on the entry-level algorithms test😀😀😀

😁Title.

Given an image represented by an N x N matrix, where each pixel in the image is 4 bytes, write a method to rotate the image by 90 degrees. Can you do this in place?
Example 1:

Given matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

Rotate the matrix in place. It becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
Example 2:

Given matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

Rotate the matrix in place. It becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]

## II. Cognizance😉😉😉
Matrix of length N
Rotate the matrix 90 degrees clockwise and you'll see that
Row I becomes the penultimate column.
Column J becomes row J
So the correspondence is [I,J] -> [J,N-1-I] (N-1 here because the coordinates start at 0 so the largest coordinate is N-1).
When rotating, each coordinate has 3 points corresponding to it, and the total of 4 points are interchanged with each other
[I,J] -> [J,N-1-I] -> [N-1-I,N-1-J] -> [N-1-J,I] -> [I,J].
So all we need to do is iterate through 1/4 of the coordinates and change the corresponding 4 sets of coordinates to replace them all.

## II. Determining the scope of traversal

There are two ways to traverse the range of 1/4: ↓↓↓↓↓↓


  <img src="/output1_2.png" alt="GitHub Logo" width="290" height="290"/>

The traversal range of output_1 is I(0-> N/2),J(0->N/2) The total area is N/2 * N/2 = N square / 4
is the easiest way to think of, it is equivalent to divide the square into 4 small squares horizontally and vertically
When N is an even number of no problem, but when N is an odd number, such as the figure N is 5, a total of 5 * 5 = 25 points,
remove the middle of a point without change, we need to traverse 24/4 = 6 points
At this time with this way of cutting there is no way to achieve equal traversal!
<img src="/output1_2_3.png" alt="GitHub Logo" width="290" height="290"/>

The traversal of Figure 2 is I(0->N),J(I->N-1-I) The total area is N * N/2 * 1/2 = N square/4 (the area of the triangle)
This is equivalent to dividing the square into 4 isosceles right triangles
This way of partitioning can be normal even if N is odd, in the example, you can take the exclusive 6 points in each triangle.
Note that the points (0,4), (1,3) can not be included, so the traversal condition can not be equal to

So use the traversal in Figure 2 to rotate each point by swapping the values of the traversed points with the other three corresponding points.

##III. Doesn't take up extra space
At this point we already know that the question only needs to find the correct pair of coordinates to swap the values.
The question asks whether this can be done without taking up extra memory space.
That is to ask how to swap the two values of A and B without taking up extra memory space.
You've already figured out how to do it
A = A+B
B = A-B
A = A-B
After these three steps we have achieved the exchange of the values of AB without taking up extra memory space.

#IIII. Code

<pre>
```python
  
class Solution:
    def rotate(self, matrix):
        n = len(matrix)
        for i in range(n // 2):
            for j in range(i, n - 1 - i):
                self.exchange(matrix, i, j, j, n - 1 - i)
                self.exchange(matrix, i, j, n - 1 - i, n - 1 - j)
                self.exchange(matrix, i, j, n - 1 - j, i)

    def exchange(self, matrix, i1, j1, i2, j2):
        matrix[i1][j1], matrix[i2][j2] = matrix[i2][j2], matrix[i1][j1]

# 示例
solution = Solution()
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

solution.rotate(matrix)
print(matrix)

  ```
</pre>



