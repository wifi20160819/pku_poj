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
const int maxn=2010;
const int maxv=110;
const int INF=1000000000;
const int sqrN=316;//sqrt(100001)£¬±íÊ¾¿éÄÚÔªËØµÄ¸öÊý 
typedef long long ll;
int N,M; 
struct Node{
       int id;
       int scores[4];
       }node[maxn];  
int flag=0; 
int ran[10000100][4]={0};   
char c[4]={'A','C','M','E'}; 
bool cmp(Node a,Node b){
     if(a.scores[flag]!=b.scores[flag])return a.scores[flag]>b.scores[flag];
     } 
           
int main(){
           scanf("%d%d",&N,&M);
           for(int i=0;i<N;i++){
                   scanf("%d%d%d%d",&node[i].id,&node[i].scores[1],&node[i].scores[2],&node[i].scores[3]);
                   node[i].scores[0]=node[i].scores[1]+node[i].scores[2]+node[i].scores[3];
                   }
           for(flag=0;flag<4;flag++){
                               sort(node,node+N,cmp);
                               ran[node[0].id][flag]=1;
                               for(int i=1;i<N;i++){
                                       if(node[i].scores[flag]==node[i-1].scores[flag]){
                                                                                          ran[node[i].id][flag]=ran[node[i-1].id][flag];                                      
                                                                                          }
                                       else{
                                            ran[node[i].id][flag]=i+1;
                                            }
                                       }
                               }
           for(int i=0;i<M;i++){
                   int g;
                   scanf("%d",&g);
                   if(ran[g][0]==0){
                                    printf("N/A\n");
                                    }
                   else{                       
                   int minRank=INF;
                   int idx=0;
                   for(int j=0;j<4;j++){
                           if(ran[g][j]<minRank){
                                         minRank=ran[g][j];
                                         idx=j;
                                         }
                           }                   
                   printf("%d %c\n",minRank,c[idx]);                                      
                        }
                   
                   }
           system("PAUSE");
           return 0;                                                                             
}
