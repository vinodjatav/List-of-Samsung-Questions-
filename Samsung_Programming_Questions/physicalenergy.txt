#include<bits/stdc++.h>
using namespace std;
#define ll long long

ll solve(ll h,ll d,ll vf[],ll vs[]){
	ll ans = LONG_LONG_MAX;
	for(int i1=0;i1<=d;i1++){
		for(int i2=0;i2<=(d-i1);i2++){
			for(int i3=0;i3<=(d-i1-i2);i3++){
				for(int i4=0;i4<=(d-i1-i2-i3);i4++){
					if(i1+i2+i3+i4<=d){
						int i5 = (d-i1-i2-i3-i4);
						ll nd = i1*vs[0]+i2*vs[1]+i3*vs[2]+i4*vs[3]+i5*vs[4];
					//	ll nd = i1*v[0].second+i2*v[1].second+i3*v[2].second+i4*v[3].second+i5*v[4].second;
						ll nans = i1*vf[0]+i2*vf[1]+i3*vf[2]+i4*vf[3]+i5*vf[4];
					//	ll nans = i1*v[0].first+i2*v[1].first+i3*v[2].first+i4*v[3].first+i5*v[4].first;
						if(nd<=h)
							ans = min(ans,nans);
					}
				}
			}
		}
	}
	return ans;
}



int main(){
	int t,index=1;
	cin >> t;
	while(t--) {
		ll h,d;
		cin >> h >> d;
		ll vf[6],vs[6];
		ll m,s,item;
		for(int i=0;i<5;i++){
			cin >> m >> s >> item;
			vf[i]=m*60+s;
			vs[i]=item;
		//	v.push_back(make_pair(m*60+s,item));
		}
		ll sec = solve(h,d,vf,vs);
		ll min = sec/60;
		ll seconds = sec%60;
		cout << "#" << index << " " << min << " " << seconds << endl;
		index++;
	}
	return 0;
}
