# dijkstra Algorithm

* 求最短路徑

## 原理

## 實作(2d array version)

* [題目](https://vjudge.net/contest/276600#problem/A)

想法：其實跟bfs很像，只是在bfs的基礎上要加上權重的判斷

AC Code：

```cpp
#pragma GCC optimize("Ofast,fast-math,unroll-loops,no-stack-protector")
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define shixia ios_base::sync_with_stdio(0),cin.tie(0),cout.tie(0)

const int Mxn = 1005;

struct tii
{
    int x,y,dis;
    bool operator>(const tii &rhs)const{
        return dis>rhs.dis;
    }
};

int t,n,m,cost[Mxn][Mxn],vis[Mxn][Mxn],ans[Mxn][Mxn];
int dx[] = {0,0,-1,1},dy[] = {1,-1,0,0};
priority_queue<tii,vector<tii>,greater<tii> > pq;

bool isr(int x,int y,int n,int m){
    if(x>0&&x<=n&&y>0&&y<=m) return true;
    return false;
}

signed main(){
    shixia;
    cin>>t;
    while(t--){
        memset(cost,-1,sizeof(cost));
        memset(vis,-1,sizeof(vis));
        memset(ans,-1,sizeof(ans));
        cin>>n>>m;
        for(int i=1;i<=n;i++)
        for(int j=1;j<=m;j++){
            cin>>cost[i][j];
            ans[i][j] = 1e18;
        }
        ans[1][1] = cost[1][1];
        pq.push({1,1,cost[1][1]});
        while(pq.size()){
            tii cur = pq.top(); pq.pop();
            int x = cur.x,y = cur.y,dis = cur.dis;
            if(vis[x][y]==1) continue;
            vis[x][y]=1;
            for(int i=0;i<4;i++){
                int rx = x + dx[i],ry = y + dy[i];
                if(isr(rx,ry,n,m))
                if(ans[rx][ry]>dis+cost[rx][ry]){
                    ans[rx][ry]=dis+cost[rx][ry];
                    pq.push({rx, ry, ans[rx][ry]});
                }
            }
        }
        cout<<ans[n][m]<<"\n";
    }
    return 0;
}
```