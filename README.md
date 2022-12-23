# binary
//Code in C for binary search tree
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>

struct node
{
    struct node *lchild;
    int info;
    struct node *rchild;
};

struct node *insert(struct node *ptr, int key);
struct node *search(struct node *ptr, int key);
void inorder(struct node *ptr);
void preorder(struct node *ptr);
void postorder(struct node *ptr);
void display(struct node *ptr, int level);


int main()
{
    struct node *root = NULL, *ptr;
    int choice, k;
    while (1)
    {
        printf("\n0:Quit \n1:Create \n2:Inorder \n3:Preorder \n4:Postorder \n5:Search");
        printf("\n Enter your choice:");
        scanf("%d", &choice);

        switch (choice)
        {
        case 1:
            printf("\nEnter the key to be inserted: ");
            scanf("%d", &k);
            root = insert(root, k);
            break;

        case 2:
            inorder(root);
            break;

        case 3:
            preorder(root);
            break;
            
        case 4:
            postorder(root);
            break;
            
        case 5:
            printf("\nEnter the key to be search: ");
            scanf("%d", &k);
            ptr = search(root, k);

            if (ptr == NULL)
            {
                printf("\n Key not present");
            }
            else
            {
                printf("\n Key present");
            }

            break;



        case 0:
            exit(0);
        }
    }

    return 0;
}

struct node *insert(struct node *ptr, int key)
{
    if (ptr == NULL)
    {
        ptr = (struct node *)malloc(sizeof(struct node));
        ptr->info = key;
        ptr->lchild = NULL;
        ptr->rchild = NULL;
    }

    else if (key < ptr->info) /*Insertion in left subtree*/
    {
        ptr->lchild = insert(ptr->lchild, key);
    }

    else if (key > ptr->info) /*Insertion in right subtree */
    {
        ptr->rchild = insert(ptr->rchild, key);
    }

    else
        printf("\n Duplicate key");

    return ptr;
} /*End of insert( )*/
struct node *search(struct node *ptr, int key)
{

    if (ptr == NULL)
    {
        printf("\n Key not found");
        return NULL;
    }

    else if (key < ptr->info) /*search in left subtree*/
        return search(ptr->lchild, key);

    else if (key > ptr->info) /*search in right subtree*/
        return search(ptr->rchild, key);

    else /*key found*/
        return ptr;
} /*End of search()*/

void inorder(struct node *ptr)
{
    if (ptr == NULL)
        return;

    inorder(ptr->lchild);
    printf("%d ", ptr->info);
    inorder(ptr->rchild);
}

void preorder(struct node *ptr)
{
    if (ptr == NULL)
        return;

    printf("%d ", ptr->info);
    preorder(ptr->lchild);
    preorder(ptr->rchild);
}

void postorder(struct node *ptr)
{
    if (ptr == NULL)
        return;

    postorder(ptr->lchild);
    postorder(ptr->rchild);
    printf("%d ", ptr->info);
}

void display(struct node *ptr, int level)
{
    int i;
    if (ptr == NULL) /*Base Case*/
        return;
    else
    {
        display(ptr->rchild, level + 1);
        printf("\n");
        for (i = 0; i < level; i++)
            printf(" ");
        printf("%d ", ptr->info);
        display(ptr->lchild, level + 1);
    }
} /*End of display()*/
