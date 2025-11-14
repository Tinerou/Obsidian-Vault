#DataStructures 

### Assignment
![[HW4.pdf]]
### File: **dict.h**
```C++
#ifndef DICT_H
#define DICT_H
#include<iostream>

class Dict {
private:
  struct Node {
    std::string city;
    std::string country;
    int population;
    Node* left;
    Node* right;
    Node(std::string city, std::string country, int population, Node* left=NULL, Node* right=NULL) {
      this->city = city;
      this->country = country;
      this->population = population;
      this->left = left;
      this->right = right;
    }
  };

  int count;
  Node* root;

  int topk_helper(Node* p, int index, int a, int b, std::string city_list[], std::string country_list[], int k) const;
  int bottomk_helper(Node* p, int index, int a, int b, std::string city_list[], std::string country_list[], int k) const;


public:
  Dict();
  ~Dict();
  unsigned int size() const;
  bool empty() const;
  bool insert(const std::string& city, const std::string& country, int population);
  bool remove(const std::string& city, const std::string& country);
  int get_population(const std::string& city, const std::string& country) const;
  int topk(int a, int b, std::string city_list[], std::string country_list[], int k) const;
  int bottomk(int a, int b, std::string city_list[], std::string country_list[], int k) const;
  bool next(const std::string& name, std::string& next_city, std::string& next_country, int& next_population) const;
};

#endif
```

### File: **dict.cpp**
```C++
#include"dict.h"
#include<iostream>

Dict::Dict() {
  count = 0;
  root = NULL;
}

Dict::~Dict() {
	while (!empty()) {
		std::string r = "";
	    std::string next_city = "";
	    std::string next_country = "";
	    int next_population = -1;
	    next(r, next_city, next_country, next_population);
	    remove(next_city, next_country);
	}
}

unsigned int Dict::size() const {
  return count;
}

bool Dict::empty() const {
  return !count;
}

bool Dict::insert(const std::string& city, const std::string& country, int population) {
  Node* curr = root;
  Node* parent = NULL;
  while (curr && (curr->city != city || curr->country != country)) {
    parent = curr;
    // case 1: same city name
    if (city == curr->city) {
      (country < curr->country) ? curr = curr->left
        : curr = curr->right;
    }
    else {
    (city < curr->city) ? curr = curr->left 
      : curr = curr->right;
    }
  }
  // case 2: same city and country
  if (curr) {
    std::cout << "This location already exists." << '\n';
    return false;
  }
  Node* newNode = new Node(city, country, population);
  // newNode->left and right both default NULL
  // case 3: root is empty
  if (!parent) root = newNode;
  // Same idea as case 1 here:
  else if (city == parent->city) {
     (country < parent->country) ? parent->left = newNode
       : parent->right = newNode;
  }
  else {
    (city < parent->city) ? parent->left = newNode
      : parent->right = newNode;
  }
  count++;
  return true;
}

bool Dict::remove(const std::string& city, const std::string& country) {
  Node* curr = root; 
  Node* parent = NULL;
  while (curr && (curr->city != city || curr->country != country)) {
    parent = curr;
    if (city == curr->city) {
      (country < curr->country) ? curr = curr->left
        : curr = curr->right;
    }
    else {
      (city < curr->city) ? curr = curr->left
        : curr = curr->right;
    }
  }
  if (!curr) return false; // if not found
  // case: two children
  if (curr->left && curr->right) {
    parent = curr;
    Node* succ = curr->right;
    while (succ->left) {
      parent = succ;
      succ = succ->left;
    }
    curr->city = succ->city;
    curr->country = succ->country;
    curr = succ;
  }
  // case: curr has 1 child 
  // subtree replaces curr
  Node* subtree = (curr->left ? curr->left : curr->right);
  // if curr is root
  if (!parent)
    root = subtree;
  else { 
    if (parent->left == curr)
      parent->left = subtree;
    else parent->right = subtree;
  }
  delete curr;
  count--;
  return true;
}

int Dict::get_population(const std::string& city, const std::string& country) const{
  Node* curr = root;
  while (curr && (curr->city != city || curr->country != country)) {
    if (city == curr->city) {
      (country < curr->country) ? curr = curr->left : curr = curr->right;
    }
    else {
      (city < curr->city) ? curr = curr->left : curr = curr->right;
    }
  }
  if (!curr) return -1; // if (city, country) dne
  return curr->population;
}

int Dict::topk(int a, int b, std::string city_list[], std::string country_list[], int k) const {
  Node* p = root;
  int index = 0;
  return topk_helper(p, index, a, b, city_list, country_list, k);
}

int Dict::topk_helper(Node* p, int index, int a, int b, std::string city_list[], std::string country_list[], int k) const{
  if (index >= k || !p) return index;
  int currIndex = topk_helper(p->left, index, a, b, city_list, country_list, k);
  if(currIndex < k && p->population >= a && p->population <= b) {
    city_list[currIndex] = p->city;
    country_list[currIndex] = p->country;
    currIndex++;
  }
  return topk_helper(p->right, currIndex, a, b, city_list, country_list, k);
}

int Dict::bottomk(int a, int b, std::string city_list[], std::string country_list[], int k) const {
  Node* p = root;
  int index = 0;
  return bottomk_helper(p, index, a, b, city_list, country_list, k);
}

// Helper class for bottomk()
int Dict::bottomk_helper(Node* p, int index, int a, int b, std::string city_list[], std::string country_list[], int k) const {
  if (index >= k || !p) return index;
  int currIndex = bottomk_helper(p->right, index, a, b, city_list, country_list, k);
  if (currIndex < k && p->population > a && p->population < b) {
    city_list[currIndex] = p->city;
    country_list[currIndex] = p->country;
    currIndex++;
  }
  return bottomk_helper(p->left, currIndex, a, b, city_list, country_list, k);
}

// finds successor of given name within the Dict
bool Dict::next(const std::string& name, std::string& next_city, std::string& next_country, int& next_population) const {
  if (root) {
    Node* curr = root;
    bool found = false;
    while (curr && curr->city != name) {
      if (name < curr->city) {
        next_city = curr->city;
        next_country = curr->country;
        next_population = curr->population;
        found = true;
        curr = curr->left;
      }
      else curr = curr->right;
    } 
    // case where name exists on tree and curr->right exists
    if (curr && curr->right) {
      curr = curr->right;
      // Find leftmost node on right subtree
      while (curr->left)
        curr = curr->left;
      // update variables
      next_country = curr->country;
      next_population = curr->population;
      found = true;
    }
    return found;
  }
  // In the case where the tree is empty
  return false;
}
```

### Recursive (insert/remove/get_population)

**dict.h** (focused)
```C++
private:
	bool insert_helper(Node*& curr, const std::string& city, const std::string& country, const int& population);
	int get_population(const std::string& city, const std::string& country) const;
private:
	bool insert(const std::string& city, const std::string& country, const int& population);
	int get_population_helper(Node* curr, const std::string& city, const std::string& country) const;
```


**dict.cpp** (focused)
```C++
// since we are modifying the tree we need Node*& here
bool Dict::insert_helper(Node*& curr, const std::string& city, const std::string& country, const int& population) {
	// base cases
	if (!curr) {
		Node newNode = new Node(city, country, population);
		curr = newNode;
		// we will increment count in insert()
		return true;
	}
	if (curr->city == city && curr->country == country)
		return false; // key already exists
	
	// recursive function
	if (curr->city == city) {
		if (country < curr->country)
			return insert_helper(curr->left, city, country, population);
		else
			return insert_helper(curr->right, city, country, population);
	}
	else {
		if (city < curr->city)
			return insert_helper(curr->left, city, country, population);
		else
			return insert_helper(curr->right, city, country, population);
	}
}

bool Dict::insert(const std::string& city, const std::string& country, const int& population) {
	found = insert_helper(root, city, country, population);
	if (found) count++;
	return found;
}

int Dict::get_population_helper(Node* curr, const std::string& city, const std::string& country) const {
	// base cases
	if (!curr) return -1; // key DNE
	if (city == curr->city && country == curr->country)
		return curr->population;
	// recursive function
	if (city == curr->city)
		if (country < curr->country)
			return get_population_helper(curr->left, city, country);
		else
			return get_population_helper(curr->right, city, country);
	else
		if (city < curr->city)
			return get_population_helper(curr->left, city, country);
		else
			return get_population_helper(curr->right, city, country);
}

int Dict::get_population(const std::string& city, const std::string& country) const {
	return get_population_helper(root, city, country);
}

bool Dict::remove_helper(Node*& curr, const std::string& city, const std::string& country) {
	if (!curr) return false;
	if (curr->city == city && curr->country == country) {
		// case 1: No children
		if (!(curr->left) && !(curr->right)) {
			delete curr;
			curr = NULL;
		}
		// case 2: 1 child
		else if (curr->left && !(curr->right)) {
			Node* temp = curr;
			curr = curr->left;
			delete temp;
		}
		else if (!(curr->left) && curr->right) {
			Node* temp = curr;
			curr = curr->right;
			delete temp;
		}
		// case 3: 2 children
		else {
			Node* temp = curr->right;
			while (temp->left)
				temp = temp->left;
			curr->city = temp->city;
			curr->country = temp->country;
			curr->population = temp->population;
			// now from right subtree remove(old succ)
			return remove_helper(curr->right, temp->city, temp->country);
		}
		return true;
	}
	if (city == curr->city) {
		if (country < curr->country)
			return remove_helper(curr->left, city, country);
		else
			return remove_helper(curr->right, city, country);
	}
	else {
		if (city < curr->city)
			return remove_helper(curr->left, city, country);
		else
			return remove_helper(curr->right, city, country);
	}
}
```