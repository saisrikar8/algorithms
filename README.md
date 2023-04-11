# Algorithms

<h2>Table of Contents</h2>
<ol>
  <li><a href = "https://github.com/saisrikar8/algorithms/new/main?readme=1#bfs">Breadth-First Search</a></li>
</ol>

<h2>Breadth-First Search</h2>
<p>BFS (Or breadth-first search) is one of the methods used to search for a node given the root node. First, you need to start at the root node of the tree. Then, you start searching its neighbors. After searching each node, the nodes will be stored in a queue. This allows the program to know which nodes it has already covered. As the program continues to keep traversing through the neighbors of multiple nodes, it will not visit a node it has already visited using the queue that stored all visited nodes. The time complexity of this algorithm is <code>O(V+E)</code> where V is the number of vertices and E is the number of edges onn the graph. The following image represents how breadth-first search visits each node and does not repeat the nodes the program has already visited:</p>
<img src = "https://upload.wikimedia.org/wikipedia/commons/5/5d/Breadth-First-Search-Algorithm.gif?20100504223639"/>

<h2>Binary Search</h2>
<p><b>Binary Search</b> is an algorithm used to search through a sorted array and find the index of a target value. Binary search uses recursion to continue to split the array into multiple pieces until it finds the target value. Basically, it will split the beginning array in half. Then, it will try to find the range that the target value belongs to. If the target value is in the higher range, it will continue to split the higher range like a seperate array. The same occurs for the lower range of the array if the target belongs to it. The program does this by finding a "midpoint" value of the array using start and end indices. If the target is less than the midpoint, the program will continue recursing through the lower range of the array. The same occurs for the higher range of the array if the target is greater than the target value. The time complexity of this algorithm is <code>O(log(n))</code> where n is the length of the array. The following image represents a program searching through an example array for the value of 47 using the binary search algorithm.</p>
<img src = "https://d18l82el6cdm1i.cloudfront.net/uploads/bePceUMnSG-binary_search_gif.gif"/>

Here is a simple implementation of the image above using Java:

```java
public class Main{
    public static void main (String[] args){
        int[] sortedArr = {0,4,7,10,14,23,45,47,53};
        int target = 47;
        int targetIndex = binarySearch(sortedArr, 0, sortedArr.length - 1, target);
        System.out.println((targetIndex > -1)? "The target was found in the array at index " + targetIndex : "The target was not found in the array.");
    }
    public static int binarySearch(int[] nums, int start, int end, int target){
        if (start >= end){
            return -1;
        }
        int mid = (end + start)/2;
        if (nums[mid] == target){
            return mid;
        }
        else{
            if (nums[mid] > target){
                return binarySearch(nums, start, mid, target);
            }
            else{
                return binarySearch(nums, mid, end, target);
            }
        }
    }
}
```

Here is the output of the code:

```

The target was found in the array at index 7


```
