# ds
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


class BinarySearchTree:
    def __init__(self):
        self.root = None

    def insert(self, root, key):
        if root is None:
            return Node(key)
        elif key < root.key:
            root.left = self.insert(root.left, key)
        elif key > root.key:
            root.right = self.insert(root.right, key)
        else:
            print("Duplicate key not allowed:", key)

        return root

    def search(self, root, key):
        if root is None or root.key == key:
            return root

        if key < root.key:
            return self.search(root.left, key)

        return self.search(root.right, key)

    def minValueNode(self, node):
        current = node

        while current.left is not None:
            current = current.left

        return current

    def delete(self, root, key):
        if root is None:
            return root

        if key < root.key:
            root.left = self.delete(root.left, key)

        elif key > root.key:
            root.right = self.delete(root.right, key)

        else:
            if root.left is None:
                return root.right

            elif root.right is None:
                return root.left

            temp = self.minValueNode(root.right)
            root.key = temp.key
            root.right = self.delete(root.right, temp.key)

        return root

    def inorder(self, root):
        if root:
            self.inorder(root.left)
            print(root.key, end=" ")
            self.inorder(root.right)


# Create Binary Search Tree
bst = BinarySearchTree()

# Insert elements
for key in [50, 30, 20, 40, 70, 60, 80]:
    bst.root = bst.insert(bst.root, key)

# Display inorder traversal
print("Inorder traversal of BST:")
bst.inorder(bst.root)
print()

# Search an element
key = 70

if bst.search(bst.root, key):
    print(f"Key {key} found in BST.")
else:
    print(f"Key {key} not found in BST.")

# Delete an element
key_to_delete = 40
bst.root = bst.delete(bst.root, key_to_delete)

print(f"\nBST after deleting {key_to_delete}:")
bst.inorder(bst.root)
print()
