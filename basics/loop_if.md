### for
```
#include <iostream>
using namespace std;
#include <vector>
int main() {
    for(int i=0,j=0; i<4, j<5; i++, j++) {
        cout<<"i="<<i<<"j="<<j<<endl;
    }
    return 0;
}
```
输出结果为：
```
i=0j=0
i=1j=1
i=2j=2
i=3j=3
i=4j=4
```
```

#include <iostream>
using namespace std;

int main() {
    string s="5as";
    for (char& c : s) {
        cout<<c<<'\t';
    }
	return 0;
}
```
gives `5	a	s	`.
```
#include <iostream>
using namespace std;

int main() {
    string a[] = {"Jan", "Feb", "Mar"};
    for(auto tmp:a) {
        cout<<tmp<<'\t';
    }
	return 0;
}
```
gives `Jan	Feb	Mar	`.
### while
```
#include <iostream>
using namespace std;
int main()
{
    int i=0;
    while(i<3) {
        cout<<i<<endl;
        i++;
    }
}
```
### if
```
#include <iostream>
using namespace std;

int main() {
	int a=2;
	if(a==0) {
	    cout<<"a=1"<<endl;
	}
	else if(a==1) {
	    cout<<"a=1"<<endl;
	}
	else if(a==2) {
	    cout<<"a=2"<<endl;
	}
	else {
	    cout<<"a=3"<<endl;
	}
}
```
### switch
```
#include <iostream>
using namespace std;

int main() {
    char a = 'X';
	switch (a) {
	    case 'J':
	    case 'M': cout<<31<<endl; break;
	    default: cout<<28<<endl;
	}
	return 0;
}
```
