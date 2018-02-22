# pku_poj
#include <cstdlib>
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
//const int INF=1000000000;
const int sqrN=316;//sqrt(100001)£¬±íÊ¾¿éÄÚÔªËØµÄ¸öÊý 
typedef long long ll;
char a[110],b[110];
ll INF=(1LL<<63-1);
ll index1,index2;
ll hashTable[maxn];
void init(){
     int num=0;
     for(char c='0';c<='9';c++){
              hashTable[c]=num++;
              }
     for(char c='a';c<='z';c++){
              hashTable[c]=num++;
              }
     }

ll convertNum10(char a[],ll index,ll inf){
                              int len=strlen(a);
                              ll ans=0;
                              for(int i=0;i<len;i++){
                                      ans=ans*index+hashTable[a[i]];
                                      if(ans<0||ans>inf)return -1;
                                      }
                              return ans;
                              }

ll findLow(char a[]){
                ll manNum=-1;
                int len=strlen(a);
                for(int i=0;i<len;i++){
                        manNum=max(manNum,hashTable[a[i]]);
                        }
                return manNum+1;
                }
int cmp(char a[],ll miding,ll ans){
    int aa;
    ll cos=convertNum10(a,miding,ans);  
    if(cos<0){
              aa=-1;
              }
    else if(cos<ans){
         aa=1;
         }  
    else if(cos>ans){
         aa=-1;
         }
    else aa=0;
    return aa;
    }

ll binarySearch(char a[],ll low,ll high,ll ans){
                     ll l=low,r=high;
                     while(l<=r){
                                 ll miding=(l+r)/2;
                                 int flag=cmp(a,miding,ans);
                                 if(flag==0)return miding;
                                 else if(flag=-1){
                                      r=miding-1;
                                      }
                                 else{
                                      l=miding+1;
                                      }
                                 }
                     return -1;
                     }
                     
int main(){
           scanf("%s %s %lld%lld",a,b,&index1,&index2);
           if(index1==2){
                         char temp[110];
                         strcpy(temp,a);
                         strcpy(a,b);
                         strcpy(b,temp);
                         }
           init();
           //printf("%lld\n",hashTable['b']);
           ll figer=convertNum10(a,index2,INF);
           ll low=findLow(b);
           ll high=max(low,figer)+1;
           ll ans=binarySearch(b,low,high,figer);
           if(ans==-1){
                       printf("Impossible\n");
                       }
           else{
                printf("%lld\n",ans);
                }
           system("PAUSE");
           return 0;                                                                             
}
