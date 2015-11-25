# Tree Week!

This week we'll add trees to our collection of abstract data structures.

## Graphs

In computer science, graphs are collections of **vertices** or **nodes**, which usually store or represent some data, and **edges**, which connect the nodes. Each edge connects two nodes together.  If you think of nodes as airports, edges would be the flight paths between them.  Here are some use cases for graphs:

* graph databases
* relationships among users in a social network
* links between pages on a website
* finding a route between two locations
* planning the order of classes to take based on prerequisites 

A sequence of edges is called a "path".

<img src="images/paths.jpg" width="300px">

## Trees

Trees are a special kind of graph with some extra rules about their nodes and edges. First, every tree has a unique, special start node called the "root" node. 
(We usually draw trees vertically with the "root" node at the top of the tree.)Second, each node in a tree can only ever have one "parent". This means there's only ever one direct path from any node to the root of the tree.  One classic example of a tree is a file sytem, where directories contain other directories and/or files. The `/` directory is called the "root" directory because it's literally the root of the computer's directory tree.  Here are a few other example use cases of trees:

* the DOM tree
* comment trees (where users can comment on comments)
* data compression algoritm trees (Huffman coding)
* tournaments 
* parser trees or syntax trees that help interpret code
* calculators

The edges in a tree are sometimes referred to as "branches".  Nodes of the tree that do not have any children are called "leaves" because no branches lead away from them. The length of the longest path from the root to a leaf is called the tree's "height".

<img src="images/tree_terms.jpg" width="300px">


Tree data structures adopt language from family trees. If an edge in a tree connects two nodes, the one closer to the root is the "parent", and the other is a "child".  From the perspective of a single node, some other nodes will be on the path between that node and the root. These are the node's "ancestors." Other nodes might be children of the  node, or children of the node's children. These are called the node's "descendants."  Nodes that share the same "parent" can be called "siblings," but that's rarer.


## Trees to Know for Interviews

### Balanced Binary Search Trees

Balanced Binary Search Trees (balanced BSTs) are trees, binary trees, binary search trees, and balanced trees.  

#### Binary Trees

The most common types of trees for interviews are "binary trees," which allow each node to have up to 2 children. We say each node can have a "left child" and a "right child."  The left child can be considered the root of a "left subtree", and the right child can be considered the root of a "right subtree".

#### Binary Search Trees

Binary search trees add on an extra restriction to binary trees. In each node's left child subtree (if it has one), all nodes will will have values *less* than the original node's value.  In each node's right child subtree (if it has one), all nodes must have a **greater** value than the original node itself. Left is less!


<img src="images/bst.jpg" width="300px">


#### Balanced Binary Trees

Balanced binary trees are another basic variant of binary trees. A "balanced" tree has a height about as low as it can possibly be while still holding all its nodes.  For binary trees, that means the height is `O(log<sub>2</sub>(n))`, where `n` is the number of nodes in the tree.  There are different definitions of exactly how to balance a tree, but you can tell a tree is balanced if all of the leaves are either at the very bottom level of the tree or just one level higher.

#### And finally... Balanced Binary Search Trees

Balanced binary search trees combine the balanced structure requirement with the node value requirement of binary search trees.  If an interview question asks about a tree, it's probably a balanced binary search tree. Ask your interview to clarify, though, whether the tree is balanced and whether it is a binary search tree. 


### N-ary Trees

N-ary trees don't have to be binary; their nodes can have more than two children. These are also known as "just regular trees". They can be balanced, but they can't be binary search trees because they're not binary. 

### Tries

Tries, also called prefix trees, aren't usually binary.  They allow each node to have as many children as needed. The special thing about tries is how they store data. The data builds up over the path from the root to each node.  Here's an example:

<img src="images/trie.jpg" width="300px">

## Challenges

PLEASE DO NOT CODE UNLESS A CHALLENGE SPECIFICALLY INSTRUCTS YOU TO

### Binary Search Trees

Assume for the following challenges that you have a binary search tree data structure. The structure will be recursive, meaning each node is actually represented as a full subtree, an instance of `BinarySearchTree`. 

The constructor for a `BinarySearchTree` instance requires that you specify the value for the current node, and it sets the left and right subtrees/nodes to  `"None"`.

The data structure allows you to do the following:

* given a tree called `my_bst`, access the "root node" with `my_bst`
* given any node, find the parent of that node with `my_node.parent` (the parent of the root node is `"None"`)
* given any node, find the left child node/subtree of that node with `.left`
* given any node, find the right child node/subtree of that node with `.right`
* given any node, find its value with `.value`

Note that each "node" is acutally an instance of `BinarySearchTree`. 

1. Pseudocode a `min` function to find the minimum-valued node in a binary search tree. Pseudocode a `max` function to find the maximum-valued node in a binary search tree.  What is another data structure you could use to find the minimum or maximum value in a set of numbers? How does using a binary search tree compare to using an unsorted array? A sorted array?

	```python
	def min(tree)
		current_node = tree
		while current_node.left != "None"
			current_node = current_node.left
		return current_node.value


	def max(tree)
		current_node = tree
		while current_node.right != "None"
			current_node = current_node.right
		return current_node.value
	```




1. Pseudocode a `search` function to check if any node in the binary search tree has a given value. Your function should return `true` if the value is in the tree and `false` if not. 

	Note: The best worst-case run time for a `search` function for a binary search tree is the height of the tree, which for a balanced BST is `O(log<sub>2</sub>n)` where `n` is the number of nodes.

	```python
	def search(tree, val)
		current_node = tree
		while current_node != "None"
			if current_node.value > val 
				current_node = current_node.right
			else if current_node.val < val
				current_node = current_node.left
			else 
				return true
		return false
	```

1. Pseudocode an `insert` function to insert a new node into the binary search tree with a given value. The result must still be a binary search tree, but don't worry about keeping it balanced.

	```python
	def insert(tree, val)
		current_node = tree
		while current_node != "None"
			if current_node.val > val 
				if current_node.right != "None"
					current_node = current_node.right
				else
					current_node.right = new BinarySearchTree(val)
			else if current_node.left != "None"
				current_node = current_node.left
			else 
				current_node.left = new BinarySearchTree(val)
	```



1. Pseudocode a `successor` function to find the next-highest-valued node in a binary search tree, given one node/subtree. If there is no higher-valued node, return "None". (The corresponding term for the next-lowest is `predecessor`).

	```python
	def successor(node)
		if node.right == "None"
			return "None"
		current_node = node.right
		while current_node.left
			current_node = current_node.left
		return current_node
	```


1. Pseudocode a `lowest_common_ancestor` function that, given two nodes/subtrees, finds their lowest common ancestor. You can assume the two nodes/subtrees are from the same tree. (Application: Find the lowest-ranked member who commands the two given members in a military heirarchy.) Your algorithm should work on binary trees that aren't binary search trees.

	```python
	def lowest_common_ancestor(node1, node2)
		current1 = node1
		current2 = node2
		node1_ancestors = new Set(current1)
		node2_ancestors = new Set(current2)
		while current1.parent != "None" && curent2.parent != "None"
			current1 = current1.parent
			if node2_ancestors.includes(current1)
				return current1
			else
				node1_ancestors.add(current1)
			current2 = current2.parent
			if node1_ancestors.includes(current2)
				return current2
			else
				node2_ancestors.add(current2)
		while current1.parent != "None"
			current1 = current1.parent
			if node2_ancestors.includes(current1)
				return current1
		while current2.parent != "None"
			current2 = current2.parent
			if node1_ancestors.includes(current2)
				return current2
	```


1. A "min heap" is another abstract data structure often thought of as a type of binary tree. It has an additional restriction called the "min heap property:" every node's value is less than the values of its children. What is special about the root of a min heap?  


### Tries

1. Create a trie for the following word list: ["hey", "hello", "howdy", "g'day"].

1. Add the phrase "hello, govnuh" to your trie from above. 

1. In a normal tree, the number of nodes determines the tree's minimum possible height. What determines the minimum possible height of a trie?



### In-Person Technical Interview Questions

1. You're tasked with setting up a quiz that adapts to the user by displaying different questions based on the percent of questions the user has gotten right so far. If the user has above 70% right so far, the next question should be slightly harder. If the user has below 70% right, the next set question should be slightly easier.  Question difficulty is rated on a scale from 1 to 10. Describe how you could use a tree to run this quiz.

1. Your job is to write a program that recognizes common words typed in on a 10-digit phone keypad (see the image below). Assume the user input comes to you as a sequence of numbers types into the phone.  Also assume you get a list of all the words you should include ahead of time. How would you structure your data?  

  ![phone keypad with letters](https://parentsof10.files.wordpress.com/2013/03/phone-keypad-picture-application.png)




