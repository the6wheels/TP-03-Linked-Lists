#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct elem{
	
	int data;
	struct elem *next;
	
}elem;


elem * find(int x,elem * head);
elem * sortlist(elem * head);
elem * newlist(int n);
void name(void);
void printlist(elem * head);
void fstelem(elem * head);
void lastelem(elem * head);
void suiv(elem * head);
void cont(elem * head);
int lang(elem * head);
elem * supfst(elem * head);
void suplast(elem * head);
void supsuiv(elem * head);
void ajotapre(elem * head);
elem * ajotavant(elem *head);
void split(elem *head, elem **first, elem **last);
elem * merge(elem *first, elem *last);
void fuse(elem **head);
void panachi(elem *start);
void swap(elem *a, elem *b);

int main (){
	
	int n;
	int a;
	int l;
	elem * head = NULL;
	name();
	printf("\nplease give the size of the list = ");
	scanf("%d",&n);
	head = newlist(n);
//	printlist(head);
	here:
	printf("\n\nActions available : \n1: Premier element.\t2: Dernier element.\n3: Suivant element. \t4: Contenu element.\n5: Taille de liste.\t6: Suprimer premier.\n7: Suprimer dernier.\t8: Suprimer suivent.\n9: Ajouter apres.\t10: Ajouter avant.\n11: Tri fusion.\t\t12: Tri Bulle.\n13: Show the list.\t0: exit the program.\n");
	printf("\n\nplease select action = ");
	scanf("%d",&a);
	
	switch (a){
		
		case 0:
			break;
		case 1:
			fstelem(head);
			goto here;
		case 2:
			lastelem(head);
			goto here;
		case 3:
			suiv(head);
			goto here;
		case 4:
			cont(head);
			goto here;
		case 5:
			l=lang(head);
			printf("\nsize of list = %d",l);
			goto here;
		case 6:
			head=supfst(head);
			goto here;
		case 7:
			suplast(head);
			goto here;
		case 8:
			supsuiv(head);
			goto here;
		case 9:
			ajotapre(head);
			goto here;
		case 10:
			head=ajotavant(head);
			goto here;
		case 11:
			fuse(&head);
			goto here;
		case 12:
			panachi(head);
			goto here;
		case 13:
			printlist(head);
			goto here;
			
		default :
			goto here;
	}
	
	
	
	return 0;
}


void printlist(elem * head){
	int n=0;
	elem *p=head;
	while (p != NULL){
		n+=1;
		printf("\nelemant %d : %d",n,(p->data));
		p=p->next;
	}
}
	
elem * newlist(int n){
	
	elem *head = NULL;
	elem *temp = NULL;
	elem *p = NULL;
	
	int i =0;
	for(i=0; i<n;i++){
		
		temp = (elem*)malloc(sizeof(elem));
		printf("\nplease enter the element # %d data : ",i+1);
		scanf("%d",&(temp->data));
		temp->next = NULL;
		
		if(head == NULL){
		head=temp;
		}
		else{
		p=head;
		while(p->next != NULL){
		p=p->next;
		}
		p->next = temp;
		}
		
	
	}
	
	return head;
	
	
}	


elem * find(int x,elem * head){
	
	elem *p=NULL;
	p=head;
	while(p != NULL){
		if (p->data == x)
		return p;
		else
		p=p->next;
	}
	return 0;
}






void fstelem(elem * head){
	elem *p=NULL;
	p=head;
	if (p == NULL)
	printf ("\nlist est vide.");
	else
	printf ("\nelement 1 : %d",(p->data));
	
}


void lastelem(elem * head){

	elem *p=NULL;
	p=head;
	int a = 1;
	while (p->next != NULL){
	a+=1;
	p=p->next;
	}
	printf("\nlast element is element %d = %d",a,(p->data));
}


void suiv(elem * head){
	elem *p=NULL;
	elem *q=NULL;
	p=head;
	q=p->next;
	int a,b=1;
	printf("\nplease give location of element : ");
	scanf("%d",&a);
while (q != NULL){	
	if (a == b){
	printf("\nnext element is %d : %d",b+1,(q->data));
	break;
}
	else
	b+=1;
	p=p->next;
	q=p->next;
	
}
if (q == NULL)
printf("\nnon element");
}




void cont(elem * head){
	elem *p=NULL;
	p=head;
	int a,b=1;
	
	
	printf("\n\nplease give the location of element : ");
	scanf("%d",&a);
	while(p != NULL){
		if (a==b){
			printf("\nelement %d data : %d",a,(p->data));
			break;
		}
		b+=1;
		p=p->next;
		
	}
	if (a<=0 || a>b)
	printf ("\nno element");
	
}


int lang(elem * head){
	
	elem *p=head;
	int a=1;
	p=head;
	if(p==NULL){
	return(0);
}
	else{
	
	while (p->next!=NULL){
		a+=1;
		p=p->next;
	}
	
	return(a);
}
}



elem * supfst(elem * head){
	
	elem *p = NULL;
	elem *q = NULL;
	p=head;
	q=head;
	head=p->next;
	free(q);
	printf("\njob done =P");
	return(head);
		
}



void suplast(elem * head){
	elem *p = NULL;
	elem *q = NULL;
	p=head;
	q=p->next;
	
	while(q->next != NULL){
		p=p->next;
		q=p->next;
	}
	p->next=NULL;
	free(q);
	
		printf("\njob done =P");
}


void supsuiv(elem * head){
	
	elem *p = NULL;
	elem *q = NULL;
	p=head;
	q=p->next;
	int a, b=1;
	printf("\nplease give the location of element : ");
	scanf("%d",&a);
	if(a<1 || a > lang(head))
	printf("\nERROR");
	else if (a==1){
		p->next=q->next;
		q=NULL;
			printf("\njob done =P");
	}
	else{
		while (q != NULL){
			if(a==b){
				p->next=q->next;
				q=NULL;
			}
			b+=1;
			p=p->next;
			q=p->next;
		}
		printf("\njob done =P");
	}
	
	
}



void ajotapre(elem * head){
	int a,b;
	elem *x=NULL;
	elem *p=NULL;
	elem *s=NULL;
	s=(elem*)malloc(sizeof(elem));
	p=head;
	printf("\nplease give data you want to enter after : ");
	scanf("%d",&a);
	x=find(a,p);
	if(x==NULL){
		printf("\nERROR couldn't find %d",a);
	}	
	else{
	printf("\nplease give new data : ");
	scanf("%d",&b);
	p=x;
	x=x->next;
	s->data=b;
	s->next=x;
	p->next=s;
		printf("\njob done =P");
	}

}


elem * ajotavant(elem *head){
	int a,b;
	elem *x=NULL;
	elem *p=NULL;
	elem *s=NULL;
	s=(elem*)malloc(sizeof(elem));
	p=head;
	printf("\nplease give data you want to enter before : ");
	scanf("%d",&a);
	x=find(a,p);
	if(x==NULL){
		printf("\nERROR couldn't find %d",a);
	}	
	else{
	printf("\nplease give new data : ");
	scanf("%d",&b);
	s->data=b;
	if(x == p){
		s->next=p;
		p=s;
		head=s;
		
	}
	else if(p->next==x){
		s->next=x;
		p->next=s;
	}
	else{
		while(p->next != x){
			p=p->next;
		}
		s->next=x;
		p->next=s;
	}
}
return(head);	
}

void fuse(elem **head){
	
	if (*head == NULL || (*head)->next == NULL)
	return;
	
	elem * p;
	elem * q;
	
	split(*head,&p,&q);
	
	fuse(&p);
	fuse(&q);
	
	*head=merge(p,q);
}

void split(elem *head, elem **first, elem **last){
	
	if (head == NULL || head->next == NULL){
		*first = head;
		*last = NULL;
		return;
	}
	
	elem *p = head;
	elem *q = head->next;
	
	while (q != NULL){
		q=q->next;
		if(q != NULL){
			p=p->next;
			q=q->next;
		}
	}
	
	*first = head;
	*last = p->next;
	p->next = NULL;
}


elem * merge(elem *first, elem *last){
	if (first == NULL)
	return last;
	
	else if (last == NULL)
	return first;
	
	elem *r=NULL;
	if(first->data <= last->data){
		r=first;
		r->next=merge(first->next, last);
	}
	else{
		r=last;
		r->next = merge(first, last->next);
	}
	return r;
}

elem * sortlist(elem * head){
	
	elem *p=NULL;
	elem *q=NULL;
	elem *s=NULL;
	
	p=head;
	q=p->next;
	
	if (p->data > q->data){
	
	p->next=q->next;
	q->next=p;
	head=q;
}
	s=head;
	p=s->next;
	q=p->next;	
	while (q->next != NULL){
		if (p->data > q->data){
			s->next=q;
			p->next=q->next;
			q->next=p;
		}
		s=s->next;
		p=s->next;
		q=p->next;
	}
	
	if(q->next == NULL && p->data > q->data){
		
		s->next=q;
		q->next=p;
		p->next=NULL;
		
	}
	
	return head;
	
}	



void name(void)
{
    int x = 0,y = 0;
    unsigned int size = 0;
    char name[35] = {0};
    unsigned int len = 0;
    size=25;
	fflush(stdin);
    strcpy(name, "  HADJAZI HISHAM  TP_3  ");
	len = strlen(name);
    for(x=(size/2); x<=size; x+=2)
    {
        for(y=1; y<(size-x); y+=2)
        {
            printf(" ");
        }
        for(y=1; y<=x; ++y)
        {
            printf("*");
        }
        for(y=1; y<=(size-x); ++y)
        {
            printf(" ");
        }
        for(y=1; y<=x; ++y)
        {
            printf("*");
        }
        printf("\n");
    }
    for(x=size; x>=1; --x)
    {
        for(y=x; y<size; ++y)
        {
            printf(" ");
        }
        if(x == size)
        {
            for(y=1; y<=((size * 2)-len)/2; ++y)
            {
                printf("*");
            }
            fputs(name,stdout);
            for(y=((size * 2)-len)/2; y< size; ++y)
            {
                printf("*");
            }
        }
        else
        {
            for(y=1; y<=(x*2)-1; ++y)
            {
                printf("*");
            }
        }
        printf("\n");
    }
}

void panachi(elem *start) 
{ 
    int s; 
    elem *p; 
    elem *q = NULL; 

    if (start == NULL) 
        return; 
  
    do
    { 
        s = 0; 
        p = start; 
  
        while (p->next != q) 
        { 
            if (p->data > p->next->data) 
            {  
                swap(p, p->next); 
                s = 1; 
            } 
            p = p->next; 
        } 
        q = p; 
    } 
    while (s); 
} 
  
void swap(elem *a, elem *b) 
{ 
    int temp = a->data; 
    a->data = b->data; 
    b->data = temp; 
} 
