#include<iostream>
using namespace std;
int main() {
	int t,index=1;
	cin>>t;
	while(t--) {
		int row,col,laser;
		cin>>row>>col>>laser;
		int ans=0;
		int amp[201][21];
		for(int i=0;i<row;i++) {
			for(int j=0;j<col;j++) {
				cin>>amp[i][j];
			}
		}
		
		for(int i=0;i<row;i++) {
			int similarrows=0;
			for(int j=0;j<row;j++) {
				bool flag=true;
				for(int k=0;k<col;k++) {
					if(amp[i][k]!=amp[j][k]) {
						flag=false;
						break;
					}
				}
				if(flag==true) {
					similarrows++;
				}
			}
			int zeros=0;
			for(int k=0;k<col;k++) {
				if(amp[i][k]==0) {
					zeros++;
				}
			}
			if(zeros<=laser && (laser-zeros)%2==0){
				ans=max(ans,similarrows);
			}
		}
		cout<<"#"<<index<<" "<<ans<<endl;
		index++;
	}
	return 0;
}
