# Algorithms

<h2>Table of Contents</h2>
<ol>
  <li><a href = "https://github.com/saisrikar8/algorithms/new/main?readme=1#bfs">Breadth-First Search</a></li>
</ol>

<h2>Breadth-First Search</h2>
BFS (Or breadth-first search) is one of the methods used to search for a node given the root node. First, you need to start at the root node of the tree. Then, you start searching its neighbors. After searching each node, the nodes will be stored in a queue. This allows the program to know which nodes it has already covered. As the program continues to keep traversing through the neighbors of multiple nodes, it will not visit a node it has already visited using the queue that stored all visited nodes. The following image represents how breadth-first search visits each node and does not repeat the nodes the program has already visited:
<img src = "https://miro.medium.com/v2/resize:fit:1200/0*OXJgetr0xmAQ-2_N.gif"/>
