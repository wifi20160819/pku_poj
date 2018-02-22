# pku_poj#include <cstdlib>
#include <iostream>//
#include <cstring>
#include<cstdio>
#include<cmath>
#include<algorithm>
#include<vector>
#include<queue>
#include<stack>
#include<map>
#include<set>
#include<stack>
using namespace std;
const int maxn=1010;
const int maxv=110;
const int INF=1000000000;
const int sqrN=316;//sqrt(100001)£¬±íÊ¾¿éÄÚÔªËØµÄ¸öÊý 
typedef long long ll;
int N,M,K;
int mon[15];
  
struct Node{
       char name[25];
       int month,dd,hh,mm;
       bool status;
       }node[maxn];
            
bool cmp(Node a,Node b){
     if(strcmp(a.name,b.name)!=0){
                                  return strcmp(a.name,b.name)<0;
                                  } 
     if(a.month!=b.month)return a.month<b.month; 
     if(a.dd!=b.dd)return a.dd<b.dd; 
     if(a.hh!=b.hh)return a.hh<b.hh;
     if(a.mm!=b.mm)return a.mm<b.mm;    
     }

void counting(int& time,int& money,int a,int b){
     Node temp=node[a];
     while(temp.dd<node[b].dd||temp.hh<node[b].hh||temp.mm<node[b].mm){
     time++;
     money+=mon[temp.mm];
     temp.mm++;
     if(temp.mm==60){
                     temp.hh++;
                     temp.mm=0;
                     }
      if(temp.hh==24){
                     temp.dd++;
                     temp.hh=0;
                     }                                                                 
                              }
     
     }    
     
int main(){
           for(int i=0;i<24;i++){
                   scanf("%d",&mon[i]);
                   }
           scanf("%d",&N);
           for(int i=0;i<N;i++){
                   scanf("%s %d:%d:%d:%d",node[i].name,&node[i].month,&node[i].dd,&node[i].hh,&node[i].mm);
                   char c[10];
                   scanf("%s",c);
                   if(strcmp(c,"on-line")){
                                           node[i].status=true;
                                           }
                   else{
                        node[i].status=false;
                        }
                   }
           sort(node,node+N,cmp);
           int on=0;
           while(on<N){
                       int next=on;
                       int flag=0;
                       while(strcmp(node[on].name,node[next].name)==0&&next<N){
                               if(flag==0&&node[next].status==true){
                                                                    flag=1;
                                                                    }
                                else if(flag==1&&node[next].status==false){
                                                                     flag=2;
                                                                     }
                               next++;
                               }
                       if(flag!=2){
                                   on=next;
                                   continue;
                                   }
                       else{
                            printf("%s %02d\n",node[on].name,node[on].month);
                            int miding=on;
                            int totalAmount=0;
                            while(miding<next){
                                           if(strcmp(node[miding].name,node[miding+1].name)==0&&
                                           node[miding].status==true&&node[miding+1].status==false){
                                           printf("%02d:%02d:%02d ",node[miding].dd,node[miding].hh,node[miding].mm);
                                           printf("%02d:%02d:%02d ",node[miding+1].dd,node[miding+1].hh,node[miding+1].mm);
                                           int totalTime=0;
                                           int money=0;
                                           counting(totalTime,money,miding,miding+1);
                                           totalAmount+=money;
                                           printf("%d ",totalTime);
                                           printf("$%.2f\n",money/100.0);
                                                                       }                                                        
                                           miding++;
                                           } 
                            printf("Total amount: $%.2f\n",totalAmount/100.0);   
                            on=next;                                     
                            }
                       }        
           system("PAUSE");
           return 0;                                                                             
}
