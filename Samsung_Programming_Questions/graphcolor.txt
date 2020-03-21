#include<iostream>
using namespace std;
int a[201][201];
int color[201];
bool issafe(int source,int colour,int v) {
	for(int i=0;i<v;i++) {
		if(a[source][i]==1) {
			if(color[i]==colour) {
				return false;
			}
		}
	}
	return true;
}
bool graphcolor(int source,int v) {
	if(source==v) {
		return true;
	}
	for(int c=1;c<=2;c++) {
		if(issafe(source,c,v)==true) {
			color[source]=c;
			if(graphcolor(source+1,v)==true) {
				return true;
			}
			color[source]=0;
		}
	}
	return false;
}
int main() {
	int t;
	cin>>t;
	while(t--) {
		int v,e;
		cin>>v>>e;
		
		for(int i=0;i<v;i++) {
			for(int j=0;j<v;j++) {
				a[i][j]=0;
			}
		}
		int x,y;
		for(int i=0;i<e;i++) {
			cin>>x>>y;
			a[x][y]=1;
			a[y][x]=1;
		}
		
		for(int i=0;i<v;i++) {
			color[i]=0;
		}
		if(graphcolor(0,v)==true) {
			cout<<"Bipartite";
		}
		else {
			cout<<"Not Bipartite";
		}
		cout<<endl;
	}
	return 0;
}
