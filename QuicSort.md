# pku_poj
#include<malloc.h> /* malloc()¦Ì¨¨ */
#include<stdio.h> /* EOF(=^Z?¨°F6),NULL */
#include<math.h> /* floor(),ceil(),abs() */

void Swamp(int *a,int *b){
		int m=0;
		m=*a;
		*a=*b;
		*b=m;
}



void QuicSort(int *a[],int s,int e){
	
		int i=s;
		int j=e;
		int k=a[s];
		if(s>=e)
			return ;
		while(i!=j){
			while(i<j&&a[j]>k)
				j--;
			 Swamp(&a[i],&a[j]);
			while(i<j&&a[i]<k)
				i++;
           Swamp(&a[i],&a[j]);
		}

		QuicSort(a,s,i-1);
		QuicSort(a,i+1,e);
}

int main(){
	int n,k;
	int a[100000],b[100000];
	int i=0,j=0;
	scanf("%d",&n);
	for(i=0;i<n;i++){
		scanf("%d",&a[i]);
	}

	do{
		scanf("%d",&k);
	}while(k>=n);
		
	QuicSort(&a,0,k);
	for(i=0;i<k;i++){
		printf("%d\n",a[i]);
	}


		
	return 0;
}


