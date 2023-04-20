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

<h3 id = "bfs">Main.java</h3>

This is the main code that is run as it is under `class Main` and the `main()` method. Aside from the `breadthFirstSearch()` method and the `findValueInTree()` method, there is also a `getRandomNumber()` method that uses the `Math.random()` method to generate a random number for testing purposes. The purpose of the `main()` method is to acquire multiple values to insert into the tree being inputted into the `findValueInTree()` method. This method then uses the `breadthFirstSearch()` method to search through the tree. The `breadthFirstSearch()` method uses a queue to visit all the nodes in a tree. First, the root node is visited and dequeued. Then, the neighbor nodes of the current node are added to the queue. The `while` loop will continue to traverse through the tree until all nodes have been visited. The program will remember which nodes have been visited by storing them in a `ArrayList<TreeNode>` called `visited`. If the target value is not found, the method will return `null`. After the program runs the `breadthFirstSearch()` method, it will clear the queue and empty the visited TreeNodes that were stored.

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

public class Main {
    public static Queue<TreeNode> queue = new LinkedList<TreeNode>();
    public static List<TreeNode> visited = new ArrayList<TreeNode>();
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
        System.out.println("The reference to the node with the value 100 was found:\n" + targetNode);
    }
    public static TreeNode findValueInTree(TreeNode tree, int target){
        System.out.println("Searching Nodes...");
        queue.add(tree);
        TreeNode targetNode = breadthFirstSearch(target);
        System.out.println("Value match found");
        queue = new LinkedList<TreeNode>();
        visited = new ArrayList<TreeNode>();
        return targetNode;
    }
    //returns first node with target value
    public static TreeNode breadthFirstSearch(int target){
        while(!queue.isEmpty()){
            TreeNode currentNode = queue.poll();
            if (!visited.contains(currentNode)){
                if (currentNode.val == target){
                    return currentNode;
                }
                if (currentNode.getNeighbors() != null) {
                    queue.addAll(currentNode.getNeighbors());
                    visited.add(currentNode);
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

<h3 id = "treenode">TreeNode.java</h3>

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
The reference to the node with the value 100 was found:
out.Java.TreeNode@2d98a335

```

Here is a similar implementation in Python.

## main.py

```python
from out.Python.TreeNode import TreeNode
import random

queue = list()
visited = list()


def breadthFirstSearch(target: int):
    while not (len(queue) == 0):
        currentNode = queue[0]
        queue.pop(0)
        if currentNode.val == target:
            return currentNode
        for neighbor in currentNode.neighbors:
            queue.append(neighbor)


def findValueInTree(root: TreeNode, target: int) -> TreeNode:
    print("Searching through tree...")
    queue.append(root)
    matchedNode = breadthFirstSearch(target)
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
        TreeNode(40, [TreeNode(random.randint(1, 20)), TreeNode(random.randint(1, 20)), TreeNode(random.randint(1, 20)), TreeNode(random.randint(1, 20))]))
    targetNode = findValueInTree(randomNode, 40)
    print("The target value was found in the tree node. Here is some info on it:\n" + str(targetNode))


if __name__ == '__main__':
    main()

```

<h3 id = "treenodepy">TreeNode.py</h3>

```python
class TreeNode:
    val = None
    neighbors = None

    def __init__(self, value: int = None, neighborlist: list = list()):
        self.val = value
        self.neighbors = neighborlist

    def __str__(self):
        return f'TreeNode: Value: {self.val}, Neighbors: {self.neighbors}.'
        
```

Here is the output of the program:

```
Starting processes...
Searching through tree...
The target value was found in the tree node. Here is some info on it:
TreeNode: Value: 40, Neighbors: [<Python.TreeNode.TreeNode object at 0x0000018928084590>, <Python.TreeNode.TreeNode object at 0x00000189280845D0>, <Python.TreeNode.TreeNode object at 0x0000018928084610>, <Python.TreeNode.TreeNode object at 0x0000018928084650>].

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


## Depth First Search

Depth-first search is another way to search through a graph or tree. Depth-first search is used a lot to augment other tasks such as counting connected components and finding articulation points in trees. The depth-first algorithm starts by searching the root node's value. Then, it will continue to search through a path of neighbor nodes until the program reaches a dead end. The program will backtrack from the dead end to the last node with unvisited neighbor elements. A dead end of the program is when there is no unvisited neighbor nodes of the current node. The program will continue to backtrack until it reaches a node that has unvisited neighbor elements. If there are no longer any unvisited neighbor nodes in the tree, the program will backtrack to the root node and the algorithm will be over. The time complexity of this program is `O(V+E)` where V is the number of vertices in the tree and E is the number of edges in the tree.

<img src = "https://upload.wikimedia.org/wikipedia/commons/7/7f/Depth-First-Search.gif"/>

Here is a simple implementation of the depth-first search algorithm using the previous <a href = "#treenode">TreeNode implementation</a> for the breadth-first search algorithm.

This implementation is very similar to the <a href = "#bfs">previously shown breadth-first search implementation</a>. First, the tree is created. Then, the `findValueInTree()` method is called. This method then calls the `depthFirstSearch()` method, which finds the target value with the dfs algorithm. First, it will check the value of the node it is currently visiting. Then, if the current node has neighbors, the method will traverse through the `ArrayList<TreeNode>` of neighbors in a `for` loop. In each iteration of the `for` loop, the program will check if a neighbor has not already been visited. If it has been visited, the neighbor node will be ignored. If it hasn't been visited, the method will store the neighbor node in a queue and call the `depthFirstSearch()` method again where the `TreeNode root` parameter is the neighbor node. The method will continue to recurse until it reaches a dead-end, where all the neighbors of the node it is currently on are already visited. If the method doesn't find a matched node for the target value, the method will return null. 

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class dfs {
    public static Queue<TreeNode> queue = new LinkedList<TreeNode>();
    public static void main(String[] args) {
        TreeNode node1 = new TreeNode(12,new ArrayList<TreeNode>());
        TreeNode node2 = new TreeNode(24,new ArrayList<TreeNode>());
        TreeNode node3 = new TreeNode(11,new ArrayList<TreeNode>());
        TreeNode node4 = new TreeNode(47,new ArrayList<TreeNode>());
        TreeNode node5 = new TreeNode(62,new ArrayList<TreeNode>());
        node1.addNeighborNode(node2);
        node1.addNeighborNode(node3);
        node2.addNeighborNode(node1);
        node2.addNeighborNode(node3);
        node2.addNeighborNode(node4);
        node3.addNeighborNode(node1);
        node3.addNeighborNode(node5);
        TreeNode targetNode = depthFirstSearch(node1, 47);
        System.out.println("The target value 47 was found at the TreeNode reference: " + targetNode + "\nHere is some info on it:\nThe value is " + targetNode.val + " and its neighbors are " + targetNode.getNeighbors());
    }
    public static TreeNode findValueInTree(TreeNode root, int target){
        TreeNode targetNode = depthFirstSearch(root, target);
        queue.clear();
        return targetNode;
    }
    //returns the first node matching the tree value
    public static TreeNode depthFirstSearch(TreeNode root, int target){
        if (root.val == target){
            return root;
        }
        if (root.getNeighbors() == null){
            return null;
        }
        for (int i = 0; i < root.getNeighbors().size(); i++){
            TreeNode neighbor = root.getTreeNodeFromNeighborArrayList(i);
            //Checking if the neighbor has been visited
            //If neighbor is visited, skip this neighbor
            if (queue.contains(neighbor)) {
                continue;
            }
            queue.add(neighbor);
            //Searching through the neighbor nodes of the neighbor
            TreeNode searched = depthFirstSearch(neighbor, target);
            //If null is returned, the searched nodes did not provide a matched node for the target value
            if (searched != null){
                return searched;
            }
        }
        //null is returned from method when there are no unvisited neighbor nodes of parameter 'root'
        return null;
    }
}

```

Here is the output of the program shown above.

```
The target value 47 was found at the TreeNode reference: TreeNode@378bf509
Here is some info on it:
The value is 47 and its neighbors are []


```

Here is a similar Python implementation using the <a href = "#treenodepy">previous TreeNode implementation</a> used for breadth first search.

```python
from Python.TreeNode import TreeNode
import random

visited = list()


def depthFirstSearch(tree: TreeNode, target: int):
    if tree.val == target:
        return tree
    for neighbor in tree.neighbors:
        if neighbor in visited:
            continue
        visited.append(neighbor)
        searched = depthFirstSearch(neighbor, target)
        if searched is not None:
            return searched
    return None


def findValueInTree(tree: TreeNode, target: int):
    targetNode = depthFirstSearch(tree, target)
    visited.clear()
    return targetNode


def main():
    tree = TreeNode(random.randint(1, 20), list())
    for i in range(10):
        tree.neighbors.append(TreeNode(random.randint(1, 20)))
        tree.neighbors[len(tree.neighbors) - 1].neighbors.append(TreeNode(random.randint(1, 20)))
        if i > 7:
            tree.neighbors[len(tree.neighbors) - 1].neighbors.append(tree.neighbors[random.randint(0, i - 1)])
    randomNum = random.randint(1, 20)
    randomNeighbors = [TreeNode(random.randint(1, 20)), TreeNode(random.randint(1, 20)), TreeNode(random.randint(1, 20)), TreeNode(random.randint(1, 20))]
    node = TreeNode(randomNum, randomNeighbors)
    tree.neighbors.append(node)
    targetNode = findValueInTree(tree, randomNum)
    print('The value ' + str(randomNum) + ' was found.\n' + str(targetNode))


if __name__ == '__main__':
    main()
```
