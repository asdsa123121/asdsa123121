#include<bits/stdc++.h>
using namespace std;

struct canh{
	int x,y,z;
};

int n,m,w;
vector<pair<int,int>> adj[1000];
bool visited[1000];
int const inf=1e9;
int parent[1000];

void prim(int u){
	vector<canh> MST;  // vector luu canh
	vector<int> d(n+1,inf);// khoi tao gia tri cac do dai cay khung la vo cung
	priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> q; // hang doi uu tien min heap
	d[u]=0;
	q.push({0,u}); // day dinh dau tien vao hang doi
	int res=0; // gia tri nho nhat cua cay khung
	while(!q.empty()){ // duyet toi khi hang doi rong
		pair<int,int> top=q.top();q.pop(); // lay va xoa phan tu dau hang doi
		int kc=top.first;   // khoang cach
		int v=top.second;   // dinh
		if(visited[v]==true) continue; // neu dinh da duoc duyet thi bo qua
		res+=kc; 
		visited[v]=true; // danh dau dinh do da duoc tham
		if(v!=u){ 
			MST.push_back({v,parent[v],kc}); // day cac canh vao vector mst
		}
		for(auto x:adj[v]){
			int y=x.first,w=x.second;  // cac dinh va trong so ke voi dinh v
			if(!visited[y]&&w<d[y]){   // neu dinh do chua duoc tham thi tham
				d[y]=w;         // cap nhap do dai
				q.push({w,y});   // day vao hang doi
				parent[y]=v;
			}
		}
	}
	cout<<"do dai cay khung nho nhat la: "<<res<<endl; // xuat do dai cay khung
	cout<<"cac canh cua cay khung la:"<<endl;
	for(canh it:MST){
		cout<<it.x<<" "<<it.y<<" "<<it.z<<endl; // xuat canh vs trong so cay khung
	}
}


int main(){
	cin>>n>>m>>w;
	for(int i=1;i<=m;i++){
		int x,y,z;
		cin>>x>>y>>z;
		adj[x].push_back({y,z}); // chuyen danh sach canh sang danh sach ke
		adj[y].push_back({x,z});
	}
	cout<<endl;
	memset(visited,false,sizeof(visited));
	prim(w);
}
