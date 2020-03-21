#include<iostream>
using namespace std;

int n,m,x,y,l;
int ar[100][100],rs[100][100],ans[100][100];
void dfs(int,int,int);
bool issafe(int a,int b) {
	return (a>=0 && a<n && b>=0 && b<m && rs[a][b]==0);
}
void up(int a,int b,int l) {
	if(issafe(a-1,b)) {
		if(ar[a-1][b]==1 || ar[a-1][b]==2 || ar[a-1][b]==5 || ar[a-1][b]==6) {
			dfs(a-1,b,l-1);
		}
	}
}
void down(int a,int b,int l) {
	if(issafe(a+1,b)) {
		if(ar[a+1][b]==1 || ar[a+1][b]==2 || ar[a+1][b]==4 || ar[a+1][b]==7) {
			dfs(a+1,b,l-1);
		}
	}
}
void left(int a,int b,int l) {
	if(issafe(a,b-1)) {
		if(ar[a][b-1]==1 || ar[a][b-1]==3 || ar[a][b-1]==4 || ar[a][b-1]==5) {
			dfs(a,b-1,l-1);
		}
	}
}
void right(int a,int b,int l) {
	if(issafe(a,b+1)) {
		if(ar[a][b+1]==1 || ar[a][b+1]==3 || ar[a][b+1]==6 || ar[a][b+1]==7) {
			dfs(a,b+1,l-1);
		}
	}
}
void dfs(int a,int b,int l) {
	if(l==0) {
		return;
	}
	ans[a][b]=1;
	rs[a][b]=1;
	switch(ar[a][b]) {
		case 1:
			up(a,b,l);
			down(a,b,l);
			left(a,b,l);
			right(a,b,l);
			break;
		case 2:
			up(a,b,l);
			down(a,b,l);
			break;
		case 3:
			left(a,b,l);
			right(a,b,l);
			break;
		case 4:
			up(a,b,l);
			right(a,b,l);
			break;
		case 5:
			down(a,b,l);
			right(a,b,l);
			break;
		case 6:
			down(a,b,l);
			left(a,b,l);
			break;
		case 7:
			up(a,b,l);
			left(a,b,l);
			break;
		default:
			break;
	}
	rs[a][b]=0;
}
int main() {
	int t,index=1;
	cin>>t;
	while(t--) {
		cin>>n>>m>>x>>y>>l;
	//	memset(ans,0,sizeof(ans));
	//	memset(rs,0,sizeof(rs));
		for(int i=0;i<n;i++) {
			for(int j=0;j<m;j++) {
				ans[i][j]=0;
				rs[i][j]=0;
			}
		}
		for(int i=0;i<n;i++) {
			for(int j=0;j<m;j++) {
				cin>>ar[i][j];
			}
		}
		if(ar[x][y]) {
			dfs(x,y,l);
		}
		int result=0;
		for(int i=0;i<n;i++) {
			for(int j=0;j<m;j++) {
				result+=ans[i][j];
			}
		}
		cout<<"#"<<index<<" "<<result<<endl;
		index++;
	}
	return 0;
}
