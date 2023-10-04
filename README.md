# CAASTECHLINKLIST
#include<stdio.h>
#include<malloc.h>
typedef struct Node
{
	int info;
	struct Node *next;
}NODE;
NODE * createList(NODE *s)
{
	NODE *node;
	char ch;
	do{
	if(s==NULL)
	{
		s=(NODE *)malloc(sizeof(NODE));
		printf("Enter value for new Node: ");
		scanf("%d",&s->info);
		s->next=NULL;
		node=s;
	}
	else
	{
		node->next=(NODE *)malloc(sizeof(NODE));
		node=node->next;
		printf("Enter value for new Node: ");
		scanf("%d",&node->info);
		node->next=NULL;
	}
	printf("Do you want to create more node: ");
	fflush(stdin);
	scanf("%c",&ch);
	}while(ch=='Y' || ch=='y');
	return s;
}
void traverse(NODE *s)
{
	if(s==NULL)
	{
		printf("List is empty");
		return;
	}
	while(s!=NULL)
	{
		if(s->next==NULL)
			printf("%d",s->info);
		else
			printf("%d->",s->info);
		s=s->next;
	}
}
NODE * insert_first(NODE *s)
{
	NODE *new1;
	new1=(NODE *)malloc(sizeof(NODE));
	printf("\nEnter value for new node: ");
	scanf("%d",&new1->info);
	new1->next=s;
	s=new1;
	return s;
}
NODE * insert_last(NODE *s)
{
	NODE *new1,*node=s;
	while(node->next!=NULL)
		node=node->next;
	new1=(NODE *)malloc(sizeof(NODE));
	printf("\nEnter value for new node: ");
	scanf("%d",&new1->info);
	new1->next=NULL;
	node->next=new1;
	return s;
}
void insert_aftervalue(NODE *s)
{
	NODE *new1,*node=s;
	int value;
	printf("\nEnter the value after which to insert: ");
	scanf("%d",&value);
	while(node!=NULL && node->info!=value)
		node=node->next;
	if(node==NULL)
	{
		printf("%d does not exist",value);
		return;
	}
	new1=(NODE *)malloc(sizeof(NODE));
	printf("\nEnter value for new node: ");
	scanf("%d",&new1->info);
	new1->next=node->next;
	node->next=new1;
}
NODE * delete_first(NODE *s)
{
	NODE *node=s;
	if(node==NULL)
	{
		printf("List is empty");
		return;
	}
	s=node->next;
	free(node);
	return s;
}
NODE * delete_last(NODE *s)
{
	NODE *node=s;
	NODE *temp;
	if(node==NULL)
	{
		printf("List is empty");
		return;
	}
	while(node->next->next!=NULL)
		node=node->next;
	temp=node->next;
	free(temp);
	node->next=NULL;
	return s;
}
NODE * delete_nodenumber(NODE *s)
{
	NODE *p,*q;
	p=q=s;
	int n,i;
	printf("\nEnter node number to delete: ");
	scanf("%d",&n);
	if(n==1)
	{
		s=delete_first(s);
		return s;
	}
	for(i=1;i<=n-1;i++)
	{
		q=p;
		p=p->next;
		if(p==NULL)
		{
			printf("\nWrong node number");
			return s;
		}
	}
	q->next=p->next;
	free(p);
	return s;
}
NODE * delete_value(NODE *s)
{
	NODE *p,*q;
	p=q=s;
	int n,i;
	printf("\nEnter value to delete: ");
	scanf("%d",&n);
	if(p->info==n)
	{
		s=delete_first(s);
		return s;
	}
	while(p->info!=n)
	{
		q=p;
		p=p->next;
		if(p==NULL)
		{
			printf("\nvalue does not exist");
			return s;
		}
	}
	q->next=p->next;
	free(p);
	return s;
}
int countnodes(NODE *s)
{
	int c=0;
	while(s!=NULL)
	{
		c++;
		s=s->next;
	}
	return c;
}
NODE * reverse_list(NODE *s)
{
	NODE *p,*q,*r;
	p=s;
	q=r=NULL;
	while(p!=NULL)
	{	
		q=p->next;
		p->next=r;
		r=p;
		p=q;
	}
	return r;
}
void pairwise_swap(NODE *node)
{
	int temp;
	while(node!=NULL && node->next!=NULL)
	{
		temp=node->info;
		node->info=node->next->info;
		node->next->info=temp;
		node=node->next->next;
	}
}
void display_middle(NODE *s)
{
	NODE *p,*q;
	p=q=s;
	while(q->next!=NULL)
	{
		p=p->next;
		q=q->next->next;
		if(q==NULL)
		{
			printf("Enter odd no of element");
			return;
		}
	}
	printf("\n%d",p->info);
}
void nthnode_end(NODE *s)
{
	NODE *node=s;
	int len=0,i;
	int n;
	printf("Enter value of n : ");
	scanf("%d",&n);
	len=countnodes(s);
	node=s;
	if(len<n)
	{
		printf("Invalid node number");
		return;
	}
	for(i=1;i<=len-n;i++)
		node=node->next;
	printf("\n%d",node->info);
}
void detect_loop(NODE *s)
{
	NODE *p,*q;
	p=q=s;
	while(p!=NULL && q!=NULL && p->next!=NULL)
	{
		q=q->next;
		p=p->next->next;
		if(p==q)
		{
			printf("Loop detected");
			return;
		}
	}
	printf("No Loop");
}
int main()
{
	NODE *start=NULL;
	int ch;
	do
	{
		printf("\n****** MENU ******");
		printf("\n1. Create List");
		printf("\n2. Traverse");
		printf("\n3. Insert as First Node");
		printf("\n4. Insert as Last Node");
		printf("\n5. Insert After a Value");
		printf("\n6. Insert When Node Number Given");
		printf("\n7. Delete First Node");
		printf("\n8. Delete Last Node");
		printf("\n9. Delete a value");
		printf("\n10. Delete Node Number");
		printf("\n11. Count Nodes");
		printf("\n12. Reverse List");
		printf("\n13. Pairwise Swap");
		printf("\n14. Middle of Linked List");
		printf("\n15. nth node from end");
		printf("\n20. Exit");
		printf("\n Enter your choice: ");
		scanf("%d",&ch);
		switch(ch)
		{
			case 1: start=createList(start);
					break;
			case 2: traverse(start);
					break;
			case 3: start=insert_first(start);
					break;
			case 4: start=insert_last(start);
					break;
			case 5: insert_aftervalue(start);
					break;
			/*case 6: insert_nodenumber(start);
					break;*/
			case 7: start=delete_first(start);
					break;
			case 8: start=delete_last(start);
					break;
			case 9: start=delete_value(start);
					break;
			case 10: start=delete_nodenumber(start);
					break;
			case 11: printf("\nNo of nodes: %d",countnodes(start));
					break;
			case 12:start=reverse_list(start);
					break;
			case 13:pairwise_swap(start);
					break;
			case 14: display_middle(start);
					break;
			case 15:nthnode_end(start);
					break;
			case 20: printf("\nExiting from program");
					break;
			default: printf("\nWrong choice...");		
		}
		getch();
	}while(ch!=20);
	
	
}
