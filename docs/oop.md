# Object Oriented Programming 

# Classes and Objects

```
#include <iostream>
using namespace std;
 
class Pacman {
 
	private:
	  int x;
	  int y;
	public:
	Pacman(int x, int y);
	void show();
};
 
Pacman::Pacman(int x, int y){
	this->x = x;
	this->y = y;
}
 
void Pacman::show(){
	std::cout << "(" << this->x << ", " << this->y << ")";
}
 
int main() {
	// your code goes here
	Pacman p = Pacman(2, 3);
	p.show();
	return 0;
}
```

# Template

**Function Template**

```cpp
#include <iostream>
#include <string>

using namespace std;

template <typename T>

T Max(T a, T b)
{
	return a < b ? b : a;
}

int main()
{

	int i = 39;
	int j = 20;
	cout << Max(i, j) << endl;

	double f1 = 13.5;
	double f2 = 20.7;
	cout << Max(f1, f2) << endl;

	string s1 = "Hello";
	string s2 = "World";
	cout << Max(s1, s2) << endl;

	double n1 = 20.3;
	float n2 = 20.4;
	// it will show an error
	// Error: no instance of function template "Max" matches the argument list
	//        arguments types are: (double, float)
	cout << Max(n1, n2) << endl;
	return 0;
}
```

