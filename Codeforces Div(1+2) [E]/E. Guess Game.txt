//https://codeforces.com/contest/1864/problem/E
//this below is 32*n^2 code , will update soon for the 32*nlogn optimization
/*You don't get to choose if you get hurt in this world...but you do have some say in who hurts you. I like my choices.*/

#pragma GCC optimize("Ofast")
#pragma GCC target("avx,avx2,fma")
#include <bits/stdc++.h>
// #define int             long long
#define all(a)          a.begin(),a.end()
#define endl            "\n"
#define fill(a,b) memset(a, b, sizeof(a))
#define rep(i, begin, end) for (__typeof(end) i = (begin) - ((begin) > (end)); i != (end) - ((begin) > (end)); i += 1 - 2 * ((begin) > (end)))
using namespace std;
int MOD=998244353;
const int MAXL=64;
int lcm(int a, int b){
    int g=__gcd(a, b);
    return a/g*b;
}
int power(int a, int b, int p){
    if(a==0)
    return 0;
    int res=1;
    a%=p;
    while(b>0)
    {
        if(b&1)
        res=(1ll*res*a)%p;
        b>>=1;
        a=(1ll*a*a)%p;
    }
    return res;
}
int modInverse(int n,int p)
{
	return power(n, p - 2, p);
}               
signed main (){
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    int t=1;
    cin>>t;
while(t--){
    int i,j,x=0,y=0,p=0,n,q=-1,u=0,v=0,k,c=0,m=998244353;
    cin>>n;
    int a[n];
    for(i=0;i<n;i++) {
        cin>>a[i];
    }
    // int ans=(21*modInverse(9,m))%m;
    // cout<<ans<<endl;
    c=0;
    int ans=0;
    for(i=0;i<n;i++){
        for(j=0;j<n;j++){
            c=0;
            if(a[i]==0){
                c+=1;
                ans+=c;
                ans%=m;
                continue;
            }
            if(a[j]==0){
                c+=2;
                ans+=c;
                ans%=m;
                continue;
            }
            x=a[i];
            // if((a[i]&(a[i]-1))==0){
            //     c+=2;
            //     continue;
            // }
            p=0;
            q=0;
            for(k=30;k>=0;k--){
                y=1<<k;
                if((a[i]&y)>0&&(a[j]&y)>0){
                    q++;
                    c++;
                    p=0;
                    continue;
                }
                else if((a[i]&y)>0){
                    if(c%2==1) c+=2;
                    else c+=1;
                    // c+=2;
                    p=1;
                    break;
                }
                else if((a[j]&y)>0){
                    if(c%2==0) c+=2;
                    else c+=1;
                    // c+=1;
                    p=2;
                    break;
                }
            }
            if(p==0) c++;
            ans+=c;
            ans%=m;
        }
    }
    c=ans;
    int n1=(1ll*n*n)%m;
    ans=(1ll*c*modInverse(n1,m))%m;
    cout<<ans<<endl;


    }
}