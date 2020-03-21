#include<iostream>
using namespace std;

int a[10000],b[10000];

unsigned int countsetbits(int n) {
	unsigned int count=0;
	while(n) {
		n&=(n-1);
		count++;
	}
	return count;
}
int main() {
	int t,index=1;
	cin>>t;
	while(t--) {
		int comps,mines;
		cin>>comps>>mines;
		int i,j;
		int ans=999999;
		for(i=0;i<mines;i++) {
			cin>>a[i];
		}
		for(i=0;i<(1<<mines);i++) {
			if(countsetbits(i)<comps || countsetbits(i)>comps)
				continue;
			for(j=0;j<mines;j++) {
				b[j]=0;
			}
			for(j=0;j<mines;j++) {
				if(i & (1<<j)) {
					b[j]=1;
				}
			}
			int maximum=-999999;
			int minimum=999999;
			int frsum=0,lastsum=0,sum=0;
			for(j=0;j<mines;) {
				if(b[j]==1) {
					sum+=a[j++];
					while(j<mines && b[j]==0) {
						sum+=a[j++];
					}
					if(j==mines) {
						lastsum=sum;
						break;
					}
					else {
						maximum=max(maximum,sum);
						minimum=min(minimum,sum);
					}
					sum=0;
				}
				else {
					frsum+=a[j++];
				}
			}
			sum=frsum+lastsum;
			maximum=max(maximum,sum);
			minimum=min(minimum,sum);
			ans=min(ans,maximum-minimum);
			
		}
		cout<<"#"<<index<<" "<<ans<<endl;
		index++;
	}
	return 0;
}
