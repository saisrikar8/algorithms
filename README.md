# Algorithms

<h2 id = "toc">Table of Contents</h2>
<ol>
  <li><a href = "#bfs">Breadth First Search</a></li>
  <li><a href = "#binarysearch">Binary Search</a></li>
</ol>

<h2 id = "bfs">Breadth First Search</h2>
<p>BFS (Or breadth-first search) is one of the methods used to search for a node given the root node. First, you need to start at the root node of the tree. Then, you start searching its neighbors. After searching each node, the nodes will be stored in a queue. This allows the program to know which nodes it has already covered. As the program continues to keep traversing through the neighbors of multiple nodes, it will not visit a node it has already visited using the queue that stored all visited nodes. The time complexity of this algorithm is <code>O(V+E)</code> where V is the number of vertices and E is the number of edges onn the graph. The following image represents how breadth-first search visits each node and does not repeat the nodes the program has already visited:</p>
<img src = "https://upload.wikimedia.org/wikipedia/commons/5/5d/Breadth-First-Search-Algorithm.gif?20100504223639"/>

Here is a basic implementation of Breadth First Search. The object type `TreeNode` is being used to create a tree of values. You can see the implementation of this class is shown below `Main.java` under `TreeNode.java`.

### Main.java

This is the main code that is run as it is under `class Main` and the `main()` method. Aside from the `breadthFirstSearch()` method and the `findValueInTree()` method, there is also a `getRandomNumber()` method that uses the `Math.random()` method to generate a random number for testing purposes. The purpose of the `main()` method is to acquire multiple values to insert into the tree being inputted into the `findValueInTree()` method. This method then uses the `breadthFirstSearch()` method to recurse through the tree. In the `breadthFirstSearch()` method, there is a for loop that traverses through the `ArrayList<TreeNode>` of the given root `TreeNode`. If any of the values of the neighbors match the target value, the method will return the reference to the matched node. If a neighbor does not match the given target value, the method will call itself and the value of the parameter `TreeNode root` will change to the neighbor. Every time the `breadthFirstSearch()` method visits a node, it will store it in an object `queue` of type `Queue<TreeNode>`. If the neighbors of a node has already been visited, the node will be ignored a it is already known that it is not a node with the target value. If a node with the target value cannot be found, the method will return `null`. Once the method is over, the queue will be cleared, so the method `findValueInTree()` can be called multiple times.

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static Queue<TreeNode> queue = new LinkedList<TreeNode>();
    public static void main(String[] args){
        ArrayList<TreeNode> neighbors = new ArrayList<TreeNode>();
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        System.out.println("Starting processes...");
        TreeNode randomNode = new TreeNode(getRandomNumber(1, 20), new ArrayList<TreeNode>());
        randomNode.addNeighborNode(new TreeNode(getRandomNumber(1, 20)));
        randomNode.addNeighborNode(new TreeNode(getRandomNumber(1, 20), neighbors));
        neighbors.clear();
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        randomNode.addNeighborNode(new TreeNode(getRandomNumber(1, 20), neighbors));
        neighbors.clear();
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        randomNode.addNeighborNode(new TreeNode(getRandomNumber(1, 20), neighbors));
        neighbors.clear();
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        randomNode.addNeighborNode(new TreeNode(getRandomNumber(1, 20), neighbors));
        neighbors.clear();
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        neighbors.add(new TreeNode(getRandomNumber(1, 20)));
        randomNode.addNeighborNode(new TreeNode(100, neighbors));
        randomNode.addNeighborNode(new TreeNode(getRandomNumber(1, 20)));
        TreeNode targetNode = findValueInTree(randomNode, 100);
        System.out.println("The reference to the node with the value 100 was found at " + targetNode);
    }
    public static TreeNode findValueInTree(TreeNode tree, int target){
        System.out.println("Searching Nodes...");
        queue.add(tree);
        if (tree.val == target){
            return tree;
        }
        TreeNode targetNode = breadthFirstSearch(tree, target);
        System.out.println("Value match found");
        queue = new LinkedList<TreeNode>();
        return targetNode;
    }
    //returns first node with target value
    public static TreeNode breadthFirstSearch(TreeNode tree, int target){
        if (tree.getNeighbors() == null){
            return null;
        }
        for (int i = 0; i < tree.getNeighbors().size(); i++){
            TreeNode neighbor = tree.getTreeNodeFromNeighborArrayList(i);
            queue.add(neighbor);
            if (queue.contains(neighbor)){
                continue;
            }
            if (neighbor.val == target){
                return neighbor;
            }
            else{
                TreeNode searched = breadthFirstSearch(neighbor, target);
                if (searched != null && searched.val == target){
                    return searched;
                }
            }
        }
        return null;
    }
    public static int getRandomNumber(double min, double max){
        return (int) ((Math.random() * max) + min);
    }
}

```

### TreeNode.java

Here is a simple implementation of a single node in a tree. It includes an `ArrayList<TreeNode>` that stores the neighbors of the values. There is also the variable `val` that stores the integer value being stored in this node. This class also features a few helper methods that allows editing and viewing the contents of the node's neighbors.

```java
import java.util.ArrayList;

public class TreeNode {
    private ArrayList<TreeNode> neighbors;
    public int val;
    public TreeNode(){
    }
    public TreeNode(int value){
        val = value;
    }
    public TreeNode(int value, ArrayList<TreeNode> neighborNodes){
        val = value;
        neighbors = neighborNodes;
    }
    public void addNeighborNode(TreeNode neighborNode){
        neighbors.add(neighborNode);
    }
    public TreeNode getTreeNodeFromNeighborArrayList(int index){
        return neighbors.get(index);
    }
    public ArrayList<TreeNode> getNeighbors(){
        return neighbors;
    }
}

```

Here is the output for the program:

```
Starting processes...
Searching Nodes...
Value match found
The reference to the node with the value 100 was found at TreeNode@5fd0d5ae

```

Here is a similar implementation in Python.

## main.py

```python
from out.Python.TreeNode import TreeNode
import random

queue = list()


def breadthFirstSearch(root: TreeNode, target: int):
    if root is None:
        return
    for neighbor in root.neighbors:
        if neighbor in queue:
            continue
        if neighbor.val == target:
            print("Value match found")
            return neighbor
        else:
            searched = breadthFirstSearch(neighbor, target)
            if searched is not None and searched.val == target:
                return searched
    return


def findValueInTree(root: TreeNode, target: int) -> TreeNode:
    print("Searching through tree...")
    if root.val == target:
        return root
    queue.append(root)
    matchedNode = breadthFirstSearch(root, target)
    queue.clear()
    return matchedNode


def main():
    print('Starting processes...')
    randomNode = TreeNode(random.randint(1, 20), list())
    neighbors = list()
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    randomNode.neighbors.append(TreeNode(random.randint(1, 20), neighbors))
    neighbors.clear()
    neighbors = list()
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    randomNode.neighbors.append(TreeNode(random.randint(1, 20), neighbors))
    neighbors.clear()
    neighbors = list()
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    randomNode.neighbors.append(TreeNode(random.randint(1, 20), neighbors))
    neighbors.clear()
    neighbors = list()
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    neighbors.append(random.randint(1, 20))
    randomNode.neighbors.append(TreeNode(random.randint(1, 20), neighbors))
    neighbors.clear()
    randomNode.neighbors.append(
        TreeNode(40, [random.randint(1, 20), random.randint(1, 20), random.randint(1, 20), random.randint(1, 20)]))
    targetNode = findValueInTree(randomNode, 40)
    print("The target value was found in the tree node. Here is some info on it:\n" + str(targetNode))


if __name__ == '__main__':
    main()
```

## TreeNode.py

```python
class TreeNode:
    val = None
    neighbors = None

    def __init__(self, value: int = None, neighborlist: list = None):
        self.val = value
        self.neighbors = neighborlist

    def __str__(self):
        return f'Value: {self.val}\nNeighbors: {self.neighbors}.'
        
```

Here is the output of the program:

```
Starting processes...
Searching through tree...
Value match found
The target value was found in the tree node. Here is some info on it:
Value: 40
Neighbors: [19, 9, 14, 5].

```

<h2 id = "binarysearch">Binary Search</h2>

<a href = "#toc"><< Back to table of contents</a>

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

Here is another implentation of the example using Python:

```python
def binarySearch(nums: list,start: int, end: int, target: int):
    if (start >= end):
        return -1
    mid = (start + end)//2
    if (nums[mid] == target):
        return mid
    else:
        if (nums[mid] > target):
            return binarySearch(nums, start, mid, target)
        else:
            return binarySearch(nums, mid, end, target)


def main():
    sortedArr = [0, 4, 7, 10, 14, 23, 45, 47, 53]
    target = 47
    targetIndex = binarySearch(sortedArr, 0, len(sortedArr) - 1, target)
    if (targetIndex > -1):
        print(f"The value was found at index {targetIndex}")
    else:
        print("The value was not found in this array")


if __name__ == '__main__':
    main()

```

Here is the output of the code:

```
The value was found at index 7


```
