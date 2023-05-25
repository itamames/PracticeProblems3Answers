# PracticeProblems3Answers

1)

DFS Pre-order: 10, 3, 1, 7, 12, 13, 15
DFS In-order: 1, 3, 7, 10, 12, 13, 15
DFS Post-order: 1, 7, 3, 15, 13, 12, 10
BFS: 10, 3, 12, 1, 7, 13, 15

2)
```java
public void mirror() 
{
        mirror(root);
}

private void mirror(BTNode<E> localRoot) 
{
        if (localRoot == null) return;
        mirror(localRoot.left);
        mirror(localRoot.right);
        BTNode<E> temp = localRoot.right;
        localRoot.right = localRoot.left;
        localRoot.left = temp;
}
```

3) For a Tree t, the lowest common connection for node 7 and node 13 will be
node 10. Find the common connection of any 2 nodes or return -1 if there isn't one.
```text
    10
   / \
  3  12
 / \   \
1   7   13
         \
          15

```
```java
public static int sameAncestor(Tree t, int x, int y) 
{
    if (t == null) 
    {
        return 0;
    }
    boolean here = (t.value() == x) || (t.value() == y);
    int a = sameAncestor(t.leftChild(), x, y);
    int b = sameAncestor(t.rightChild(), x, y);
    if ((a == -1 && b == -1) || ((a == -1 || b == -1) && here)) 
    {
    //The current node is the common ancestor if
    // 1. x and y are located on different branches
    // 2. one of x or y is the current label and the other is farther
    // down the tree
        return t.value();
    } 
    // if one of our children or us is a find, we pass it up.
    else if (here || a == -1 || b == -1)
    {

        // We "flag" this node by sending -1 up the recursive calls
        return -1;
    } else 
    {
        // If the node is not the common ancestor nor contains x/y as a label,
        // we can just ignore it and all his children
        return 0;
    }
}
```


4) Given both implementations of a min and max heap, convert a max heap into a min heap without recursion.

```java
public static ArrayList<Integer> convertMaxHeapToMinHeap(ArrayList<Integer> maxHeap) {
    // Traverse the max heap from the last parent to the root
    for (int i = (maxHeap.size() / 2) - 1; i >= 0; i--) {
        // Perform a top-down heapify starting from each parent
        int j = i;
        while (true) {
            // Find the index of the minimum child
            int leftChild = 2 * j + 1;
            int rightChild = 2 * j + 2;
            int minChild = leftChild;

            if (rightChild < maxHeap.size() && maxHeap.get(rightChild) < maxHeap.get(leftChild)) {
                minChild = rightChild;
            }

            // Swap the current node with the minimum child if it is larger
            if (minChild < maxHeap.size() && maxHeap.get(minChild) < maxHeap.get(j)) {
                int temp = maxHeap.get(j);
                maxHeap.set(j, maxHeap.get(minChild));
                maxHeap.set(minChild, temp);
            } else {
                break;
            }

            // Update the index to continue the top-down heapify
            j = minChild;
        }
    }
    return maxHeap;
}
```

5)

```java
public List<Node> getNodesAtHeight(Node root, int height) {
    List<Node> nodes = new ArrayList<>();
    getNodesAtHeightHelper(root, 0, height, nodes);
    return nodes;
}

private void getNodesAtHeightHelper(Node node, int currentHeight, int targetHeight, List<Node> nodes) {
    if (node == null) {
        return;
    }
    if (currentHeight == targetHeight) {
        nodes.add(node);
        return;
    }
    getNodesAtHeightHelper(node.left, currentHeight + 1, targetHeight, nodes);
    getNodesAtHeightHelper(node.right, currentHeight + 1, targetHeight, nodes);
}
```


6) 

The following code should check if a given binary tree is a BST. However, for some trees, it
returns the wrong answer.
```java
public static boolean brokenIsBST(TreeNode T) 
{
    if (T == null) 
    {
        return true;
    } 
    else if (T.left != null && T.left.val > T.val ||
    T.right != null && T.right.val < T.val) 
    {
        return false;
    } 
    else 
    {
        return brokenIsBST(T.left) && brokenIsBST(T.right);
    }
}
```
a) Give an example of a binary tree for which brokenIsBST fails.

      5

     / \

    4    7

        / \

       3    8
The method fails for some binary trees that are not BSTs because it only checks that the value
at a node is greater than its left child and less than its right child, not that its value is greater
than every node in the left subtree and less than every node in the right subtree. 
It is important to note that the method does indeed return true for every binary tree that actually
is a BST (it correctly identifies proper BSTs).

b) Now, write isBST that fixes the error encountered in part 

```java
public static boolean isBST(TreeNode T) 
{
    return isBSTHelper(T, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

public static boolean isBSTHelper(TreeNode T, int min, int max) 
{
    if (T == null) 
    { 
        return true;
    } 
    else if (T.val < min || T.val > max) 
    {
        return false;
    } 
    else 
    {
        return isBSTHelper(T.left, min, T.val)
            && isBSTHelper(T.right, T.val, max);
    }
}

```


7)
```java
public static boolean isMinHeap(ArrayList<Integer> minHeap) {
        // Traverse the max heap from the last parent to the root
        
        for (int i = (maxHeap.size() / 2) - 1; i >= 0; i--) 
        { 
            int j = i;
            // check both children are bigger than parent
            int leftChild = 2 * j + 1;
            int rightChild = 2 * j + 2;

            if(maxHeap.get(i)>maxHeap.get(rightChild) || maxHeap.get(i) > maxHeap.get(leftChild))
                return false;
                
        }
        return true;
}
```


