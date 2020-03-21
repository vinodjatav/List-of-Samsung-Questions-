#include<bits/stdc++.h>
using namespace std;
int n,max_jewels;
int maze[100][100],a[100][100];
int sol[100][100];

void fun(int x,int y,int jewels) {
	
	if(maze[x][y]==3 || maze[x][y]==1) {
		return;
	}
	
	if(a[x][y]==2) {
		jewels+=1;
	}
	maze[x][y]=3;
	
	if(x==n-1 && y==n-1) {
		if(jewels>max_jewels) {
			max_jewels=jewels;
			
			for(int i=0;i<n;i++) {
				for(int j=0;j<n;j++) {
					sol[i][j]=maze[i][j];
				}
			}
		}
		
		if(a[x][y]==2) {
			maze[x][y]=2;
		}
		else {
			maze[x][y]=0;
		}
	}
	
	if((x-1)>=0) {
		fun(x-1,y,jewels);
	}
	if((x+1)<n) {
		fun(x+1,y,jewels);
	}
	if((y-1)>=0) {
		fun(x,y-1,jewels);
	}
	if((y+1)<n) {
		fun(x,y+1,jewels);
	}
	
	if(a[x][y]==2) {
		maze[x][y]=2;
	}
	else {
		maze[x][y]=0;
	}
	
}
int main() {
	int t,index=1;
	cin>>t;
	while(t--) {
		cin>>n;
	//	memset(a,-1,sizeof(a));
	//	memset(maze,-1,sizeof(maze));
	//	memset(sol,-1,sizeof(sol));
		for(int i=0;i<n;i++) {
			for(int j=0;j<n;j++) {
				a[i][j]=-1;
				maze[i][j]=-1;
				maze[i][j]=-1;
			}
		}
		for(int i=0;i<n;i++) {
			for(int j=0;j<n;j++) {
				cin>>maze[i][j];
				a[i][j]=maze[i][j];
			}
		}
		max_jewels=-1;
		fun(0,0,0);
		cout<<"Case #"<<index<<endl;
		cout<<endl;
		for(int i=0;i<n;i++) {
			for(int j=0;j<n;j++) {
				cout<<sol[i][j]<<" ";
			}
			cout<<endl;
		}
		cout<<max_jewels<<endl;
		index++;
	}
	return 0;
}
