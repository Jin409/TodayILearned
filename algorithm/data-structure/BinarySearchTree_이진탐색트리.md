```java
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

    public void delete(int key) {
        Node location = findLocation(key);

        if (location.getKey() != key) {
            return; // 없으므로 삭제를 하지 않는다
        }
        Node a = location.getLeft();
        Node b = location.getRight();
        Node pt = a.getParent();
        Node m = null;
        Node c = null;

        // 왼쪽이 없다면
        if (a == null) {
            c = b; // 바로 지우고자 하는 노드의 자리에 오른쪽을 붙여버린다.
        } else { // 왼쪽이 있다면
            c = a;
            m = a;
            while (m != null) {
                m = m.getRight(); // 가장 큰 노드를 찾는다
            }
            if (b != null) {
                m.setRight(b);
            }
        }

        // 지우고자 하는 노드가 루트이다
        if (pt == null) {
            root = c;
        } else {
            c.setParent(pt);
            if (pt.getKey() < key) {
                pt.setRight(c);
            } else {
                pt.setLeft(c);
            }
        }
    }
}
```