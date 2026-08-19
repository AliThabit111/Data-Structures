// Objective: Implementation of a Binary Search Tree (BST) with CRUD operations, recursive/iterative search, traversals, and tree properties.
// Operations: insert, remove, deleteFromTree, search (iterative/recursive), inorder/preorder/postorder traversals, height, nodeCount, leavesCount, clearTree.
// Time Complexity: O(h) for search, insert, remove (where h is height: O(log n) average, O(n) worst-case) | O(n) for traversals, clear, counts
// Space Complexity: O(n) dynamic nodes (plus O(h) recursion stack)

#include <iostream>
#include <cassert>

using namespace std;

struct nodeType
{
	int info;
	nodeType *left;
	nodeType *right;
};

class binarySearchTreeType
{
public:
	binarySearchTreeType();
	~binarySearchTreeType();

	bool isEmpty();
	bool search(int item);
	bool searchRec(int item);
	void insert(int item);
	void remove(int item);
	void inorderTraversal();
	void preorderTraversal();
	void postorderTraversal();
	int treeHeight();
	int treeNodeCount();
	int treeLeavesCount();
	void clearTree();

private:
	nodeType *root;

	void clear(nodeType* &p);
	void inorder(nodeType *p);
	void preorder(nodeType *p);
	void postorder(nodeType *p);
	int height(nodeType *p);
	int max(int x, int y);
	int nodeCount(nodeType *p);
	int leavesCount(nodeType *p);
	void deleteFromTree(nodeType* &p);
	bool searchRecPriv(nodeType *p, int item);
};

// Constructor: Initialize empty BST
binarySearchTreeType::binarySearchTreeType()
{
	root = NULL;
}

// Check if tree is empty
bool binarySearchTreeType::isEmpty()
{
	return (root == NULL);
}

// Public Inorder Traversal (Left -> Root -> Right)
void binarySearchTreeType::inorderTraversal()
{
	inorder(root);
	cout << endl;
}

// Public Preorder Traversal (Root -> Left -> Right)
void binarySearchTreeType::preorderTraversal()
{
	preorder(root);
	cout << endl;
}

// Public Postorder Traversal (Left -> Right -> Root)
void binarySearchTreeType::postorderTraversal()
{
	postorder(root);
	cout << endl;
}

// Get height of the tree
int binarySearchTreeType::treeHeight()
{
	return height(root);
}

// Get total number of nodes
int binarySearchTreeType::treeNodeCount()
{
	return nodeCount(root);
}

// Get total number of leaf nodes (nodes with 0 children)
int binarySearchTreeType::treeLeavesCount()
{
	return leavesCount(root);
}

// Recursive Inorder: yields sorted values for BST
void binarySearchTreeType::inorder(nodeType *p)
{
	if (p != NULL)
	{
		inorder(p->left);
		cout << p->info << " ";
		inorder(p->right);
	}
}

// Recursive Preorder
void binarySearchTreeType::preorder(nodeType *p)
{
	if (p != NULL)
	{
		cout << p->info << " ";
		preorder(p->left);
		preorder(p->right);
	}
}

// Recursive Postorder
void binarySearchTreeType::postorder(nodeType *p)
{
	if (p != NULL)
	{
		postorder(p->left);
		postorder(p->right);
		cout << p->info << " ";
	}
}

// Recursive helper to deallocate all nodes
void binarySearchTreeType::clear(nodeType* &p)
{
	if (p != NULL)
	{
		clear(p->left);
		clear(p->right);
		delete p;
		p = NULL;
	}
}

// Public clear method
void binarySearchTreeType::clearTree()
{
	clear(root);
}

// Destructor: Clean up tree memory
binarySearchTreeType::~binarySearchTreeType()
{
	clear(root);
}

// Calculate height recursively
int binarySearchTreeType::height(nodeType *p)
{
	if (p == NULL)
		return 0;
	else
		return 1 + max(height(p->left), height(p->right));
}

// Helper to find max of two integers
int binarySearchTreeType::max(int x, int y)
{
	if (x >= y)
		return x;
	else
		return y;
}

// Count total nodes recursively
int binarySearchTreeType::nodeCount(nodeType *p)
{
	if (p == NULL)
		return 0;
	else
		return 1 + nodeCount(p->left) + nodeCount(p->right);
}

// Count leaf nodes recursively
int binarySearchTreeType::leavesCount(nodeType *p)
{
	if (p == NULL)
		return 0;
	else if ((p->left == NULL) && (p->right == NULL))
		return 1;
	else
		return leavesCount(p->left) + leavesCount(p->right);
}

// Iterative search for an element
bool binarySearchTreeType::search(int item)
{
	nodeType *current = root;

	while (current != NULL)
	{
		if (current->info == item)
			return true;
		else if (current->info > item)
			current = current->left;
		else
			current = current->right;
	}

	return false;
}

// Public recursive search interface
bool binarySearchTreeType::searchRec(int item)
{
	return searchRecPriv(root, item);
}

// Private recursive search helper
bool binarySearchTreeType::searchRecPriv(nodeType *p, int item)
{
	if (p == NULL)
		return false;
	else if (p->info == item)
		return true;
	else if (p->info > item)
		return searchRecPriv(p->left, item);
	else
		return searchRecPriv(p->right, item);
}

// Insert new item into BST (no duplicates allowed)
void binarySearchTreeType::insert(int item)
{
	nodeType *current;
	nodeType *trailCurrent;
	nodeType *newNode;

	newNode = new nodeType;
	assert(newNode != NULL);
	newNode->info = item;
	newNode->left = NULL;
	newNode->right = NULL;

	if (root == NULL)
		root = newNode;
	else
	{
		current = root;

		while (current != NULL)
		{
			trailCurrent = current;

			if (current->info == item)
			{
				cout << "The insert item is already in the list -- duplicates are not allowed.\n";
				delete newNode;
				return;
			}
			else if (current->info > item)
				current = current->left;
			else
				current = current->right;
		}

		if (trailCurrent->info > item)
			trailCurrent->left = newNode;
		else
			trailCurrent->right = newNode;
	}
}

// Find node to be deleted then invoke deleteFromTree
void binarySearchTreeType::remove(int item)
{
	nodeType *current;
	nodeType *trailCurrent;

	if (root == NULL)
	{
		cout << "Cannot delete from the empty tree.\n";
		return;
	}
	if (root->info == item)
	{
		deleteFromTree(root);
		return;
	}

	trailCurrent = root;

	if (root->info > item)
		current = root->left;
	else
		current = root->right;

	// Search for target node
	while (current != NULL)
	{
		if (current->info == item)
			break;
		else
		{
			trailCurrent = current;
			if (current->info > item)
				current = current->left;
			else
				current = current->right;
		}
	}

	if (current == NULL)
		cout << "The delete item is not in the tree.\n";
	else if (trailCurrent->info > item)
		deleteFromTree(trailCurrent->left);
	else
		deleteFromTree(trailCurrent->right);
}

// Handles node deletion across 3 cases (leaf node, single child, two children)
void binarySearchTreeType::deleteFromTree(nodeType* &p)
{
	nodeType *current;
	nodeType *trailCurrent;
	nodeType *temp;

	// Case 1: Leaf node (0 children)
	if (p->left == NULL && p->right == NULL)
	{
		delete p;
		p = NULL;
	}
	// Case 2a: Only right child exists
	else if (p->left == NULL)
	{
		temp = p;
		p = p->right;
		delete temp;
	}
	// Case 2b: Only left child exists
	else if (p->right == NULL)
	{
		temp = p;
		p = p->left;
		delete temp;
	}
	// Case 3: Node has two children (find inorder predecessor)
	else
	{
		current = p->left;
		trailCurrent = NULL;

		while (current->right != NULL)
		{
			trailCurrent = current;
			current = current->right;
		}

		p->info = current->info; // Copy predecessor value

		if (trailCurrent == NULL)
			p->left = current->left;
		else
			trailCurrent->right = current->left;

		delete current;
	}
}

int main()
{
	binarySearchTreeType b;
	b.insert(10);
	b.insert(20);
	b.insert(5);
	b.insert(15);
	b.insert(30);

	cout << "Inorder Traversal: ";
	b.inorderTraversal();

	cout << "Removing 10...\n";
	b.remove(10);

	cout << "Inorder after remove: ";
	b.inorderTraversal();

	return 0;
}
