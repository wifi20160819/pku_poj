# pku_poj
#include<malloc.h> /* malloc()¦Ì¨¨ */
#include<stdio.h> /* EOF(=^Z?¨°F6),NULL */
#include<math.h> /* floor(),ceil(),abs() */

void Merge(int a[],int s,int m,int e,int temp[]){
	int pa=s;
	int i;
	int pb=m+1;
	int p1=0;
	while(pa<=m&&pb<=e){
		if(a[pa]>a[pb]){
			temp[p1++]=a[pa];pa++;
		}
			
		else{
			temp[p1++]=a[pb];pb++;			
		}			
	}
	while(pa<=m){
			temp[p1++]=a[pa];pa++;
	}
	while(pb<=e){
           temp[p1++]=a[pb];pb++;
	}
	for(i=0;i<p1;i++){
		a[s+i]=temp[i];
	}

}

void MergeSort(int a[],int s,int e,int temp[]){
	int m;
	if(e>s){
		m=s+(s-e)/2;
		MergeSort(a,s,m,temp);
    	MergeSort(a,m+1,e,temp);
		Merge(a,s,m,e,temp);
	}     


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
		
	MergeSort(a,0,k,b);
	for(i=0;i<k;i++){
		printf("%d\n",a[i]);
	}
		
	return 0;
}
