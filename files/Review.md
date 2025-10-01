copy constructor
- Time const(Time& t);
- When constructing we use copy constructor:
	- Time t3 = t1;
	- rather than
	- t2 = t3 // This uses assignment operator bc t2 already exists
overloading operator==
- When using pointers by default they compare addresses not values.
