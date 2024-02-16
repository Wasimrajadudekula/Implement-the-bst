# Implement-the-bst

// IMPLEMENT THE BST WITH THE FOLLOWING INDIVIDUAL FUNCTIONS

#include <stdio.h>
#include <stdlib.h>

struct TreeNode
{
    struct TreeNode *left;
    int val;
    struct TreeNode *right;
};

struct TreeNode *createNode(int data)
{
    struct TreeNode *newNode = (struct TreeNode *)malloc(sizeof(struct TreeNode));
    if (newNode == NULL)
    {
        printf("Memory Error");
        return NULL;
    }

    newNode->val = data;
    newNode->left = NULL;
    newNode->right = NULL;

    return newNode;
}

struct TreeNode *insert(struct TreeNode *root, int k)
{
    if (root == NULL)
        return createNode(k);

    if (k < root->val)
        root->left = insert(root->left, k);

    if (k > root->val)
        root->right = insert(root->right, k);

    return root;
}

void inorderTraversal(struct TreeNode *root)
{
    if (root != NULL)
    {
        inorderTraversal(root->left);
        printf("%d ", root->val);
        inorderTraversal(root->right);
    }
}

struct TreeNode *search(struct TreeNode *root, int k)
{
    if (root == NULL || root->val == k)
        return root;

    if (k < root->val)
        return search(root->left, k);

    return search(root->right, k);
}

int findSmallestElement(struct TreeNode *root)
{
    if (root == NULL)
    {
        printf("The tree is empty.\n");
        return -1;
    }

    while (root->left != NULL)
    {
        root = root->left;
    }

    return root->val;
}

int findLargestElement(struct TreeNode *root)
{
    if (root == NULL)
    {
        printf("The tree is empty.\n");
        return -1;
    }

    while (root->right != NULL)
    {
        root = root->right;
    }

    return root->val;
}

int findHeight(struct TreeNode *root)
{
    if (root == NULL)
    {
        return 0;
    }
    else
    {

        int leftHeight = findHeight(root->left);
        int rightHeight = findHeight(root->right);

        return (leftHeight > rightHeight) ? (leftHeight + 1) : (rightHeight + 1);
    }
}

void displayTree(struct TreeNode *root)
{
    if (root != NULL)
    {

        displayTree(root->left);

        printf("%d ", root->val);

        displayTree(root->right);
    }
}

int main()
{
    struct TreeNode *root = NULL;

    root = insert(root, 50);
    root = insert(root, 10);
    root = insert(root, 30);
    root = insert(root, 6);
    root = insert(root, 8);
    root = insert(root, 60);
    root = insert(root, 20);

    int height = findHeight(root);
    printf("The height of the BST is: %d\n", height);

    displayTree(root);
    printf("\n");
    
    free(root->left->left);
    free(root->left);
    free(root->right);
    free(root);

    return 0;
}
