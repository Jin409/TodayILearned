```java
package 이진탐색트리;

class Node {
    private int key;
    private Node parent;
    private Node left;
    private Node right;

    public Node(int key) {
        this.key = key;
    }

    public int getKey() {
        return key;
    }

    public Node getParent() {
        return parent;
    }

    public Node getLeft() {
        return left;
    }

    public Node getRight() {
        return right;
    }

    public void setParent(Node parent) {
        this.parent = parent;
    }

    public void setLeft(Node left) {
        this.left = left;
    }

    public void setRight(Node right) {
        this.right = right;
    }
}

class BinarySearchTree {
    private Node root;
    private int size;

    public BinarySearchTree(Node root) {
        this.root = root;
        this.size = 1;
    }

    // 있으면 해당 노드, 없으면 부모의 위치 반환
    public Node findLocation(int searchKey) {
        Node parent = null;
        Node node = root;
        while (node != null) {
            if (node.getKey() > searchKey) {
                parent = node;
                node = node.getLeft();
            } else if (node.getKey() < searchKey) {
                parent = node;
                node = node.getRight();
            } else {
                return node;
            }
        }
        return parent;
    }

    public void insert(int key) {
        Node insertNode = new Node(key);
        Node location = findLocation(key);

        if (location.getKey() == key) {
            return; // 중복되므로 아무것도 하지 않는다
        } else if (location.getKey() < key) {
            location.setRight(insertNode);
        } else {
            location.setLeft(insertNode);
        }
    }


}
```