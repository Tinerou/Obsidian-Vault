### **Static Array:** list.h
``` C++
#ifndef _LIST_H  
#define _LIST_H  
#include <ostream>  
const int SIZE = 1000;  
typedef int ElementType;  
class List {  
private:  
	ElementType arr[SIZE];  
	int count;  
public:  
	List();  
	~List();  
	bool empty();  
	bool insert(ElementType x, int pos);  
	// - Input validation (check if pos is valid)
	// - Make rooom for new elements (shift elements if needed)
	// - sort (array[pos] = x)
	// - update count
	bool erase(int pos);  
	void display(std::ostream& out) const;  
};  
	std::ostream& operator<<(std::ostream& out, const List& list);  
#endif
```