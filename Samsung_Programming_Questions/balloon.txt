#include<bits/stdc++.h>
using namespace std;
int n,a[50],visited[50],max_ans;
void fun(int shot,int ans) {
	if(shot==n) {
		if(ans>max_ans) {
			max_ans=ans;
		}
		return;
	}
	int cr_ans=ans;
	for(int i=0;i<n;i++) {
		if(visited[i]==0) {
			visited[i]=1;
			int lf=0,rf=0,lv=1,rv=1;
			for(int j=i-1;j>=0;j--) {
				if(visited[j]==0) {
					lf=1;
					lv=a[j];
					break;
				}
			}
			for(int j=i+1;j<n;j++) {
				if(visited[j]==0) {
					rf=1;
					rv=a[j];
					break;
				}
			}
			if(rf==1 && lf==1) {
				ans=ans+lv*rv;
			}
			else if(lf==1 && rf==0) {
				ans=ans+lv;
			}
			else if(lf==0 && rf==1) {
				ans=ans+rv;
			}
			else {
				ans=ans+a[i];
			}
			fun(shot+1,ans);
			visited[i]=0;
			ans=cr_ans;
		}
	}
}
int main() {
	int t,index=1;
	cin>>t;
	while(t--) {
		cin>>n;
		for(int i=0;i<n;i++) {
			cin>>a[i];
			visited[i]=0;
		}
		max_ans=-99;
		fun(0,0);
		cout<<"#"<<index<<" "<<max_ans<<endl;
		indedx++;
	}
	return 0;
}
