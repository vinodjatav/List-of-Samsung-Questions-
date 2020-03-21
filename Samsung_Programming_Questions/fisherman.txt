#include<iostream>
using namespace std;

int n;
int a[100];
int gate1,p1;
int gate2,p2;
int gate3,p3;
int L=0,R=1;

int absdiff(int x,int y) {
	int xd=(x>y)?(x-y):(y-x);
	return xd;
}

void copyarr() {
	for(int i=0;i<n;i++) {
		a[i]=0;
	}
}

int cost(int pos,int pref) {
	int fp,sp;
	int f=INT_MAX,s=INT_MAX;
	if(pref==L) {
		for(int i=pos;i>=0;i--) {
			if(a[i]==0) {
				fp=i;
				f=(absdiff(pos,i)+1);
				break;
			}
		}
		for(int i=pos;i<n;i++) {
			if(a[i]==0) {
				sp=i;
				s=(absdiff(pos,i)+1);
				break;
			}
		}
		if(f<s) {
			a[fp]=1;
			return f;
		}
		else {
			a[sp]=1;
			return s;
		}
	}
	else {
		for(int i=pos;i<n;i++) {
			if(a[i]==0) {
				fp=i;
				f=absdiff(pos,i)+1;
				break;
			}
		}
		for(int i=pos;i>=0;i--) {
			if(a[i]==0) {
				sp=i;
				s=absdiff(pos,i)+1;
				break;
			}
		}
		if(f<s) {
			a[fp]=1;
			return f;
		}
		else {
			a[sp]=1;
			return s;
		}
	}
}
//LLL
int first(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=0,s=0,t=0;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//LLR
int second(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=0,s=0,t=1;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//LRL
int three(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=0,s=1,t=0;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//RLL
int four(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=1,s=0,t=0;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//LRR
int five(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=0,s=1,t=1;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//RLR
int six(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=1,s=0,t=1;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//RRL
int seven(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=1,s=1,t=0;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
//RRR
int eight(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int cst=0;
	int f=1,s=1,t=1;
	for(int i=0;i<p1;i++) {
		cst+=cost(gate1,f);
		f=!f;
	}
	for(int i=0;i<p2;i++) {
		cst+=cost(gate2,s);
		s=!s;
	}
	for(int i=0;i<p3;i++) {
		cst+=cost(gate3,t);
		t=!t;
	}
	return cst;
}
int f(int gate1,int gate2,int gate3,int p1,int p2,int p3) {
	int ans=INT_MAX;
	ans=min(ans,first(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,second(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,three(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,four(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,five(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,six(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,seven(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	ans=min(ans,eight(gate1,gate2,gate3,p1,p2,p3));
//	memset(a,0,sizeof(a));
	copyarr();
	
	return ans;
	
}
int main() {
	int t,index=1;
	cin>>t;
	while(t--) {
		cin>>n;
		cin>>gate1>>p1;
		cin>>gate2>>p2;
		cin>>gate3>>p3;
		int ans=INT_MAX;
		//memset(a,0,sizeof(a));
		copyarr();
		ans=min(ans,f(gate1,gate2,gate3,p1,p2,p3));
		ans=min(ans,f(gate1,gate3,gate2,p1,p3,p2));
		ans=min(ans,f(gate2,gate1,gate3,p2,p1,p3));
		ans=min(ans,f(gate2,gate3,gate1,p2,p3,p1));
		ans=min(ans,f(gate3,gate1,gate2,p3,p1,p2));
		ans=min(ans,f(gate3,gate2,gate1,p3,p2,p1));
		cout<<"#"<<index<<" "<<ans<<endl;
		index++;
	}
	return 0;
}
