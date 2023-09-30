# Dynamic array in C++

Usage example:

```cpp
template<class T>
static void out(const Array<T>& arr){
	for (int32_t index = 0; 
		index < arr.length();
		++index){
		std::cout << arr[index];
		if (index != (arr.length() - 1))
			std::cout << ", ";
	}
	std::cout << "];" << std::endl;
}

template<class T>
static void out_itr(const Array<T>& arr){
	for (auto begin = arr.begin(), end = arr.end();
		begin != end;
		++begin){
		std::cout << *begin;
		if (begin != (end - 1))
			std::cout << ", ";
	}
	std::cout << "];" << std::endl;
}

template<class T>
static void populate(Array<T>& out_arr, size_t count){
	for (int32_t index = 0;
		index < count;
		++index){
		out_arr.push_back(index);
	}
}

#define OutItr(arr) \
{\
std::cout << #arr ": ["; \
out_itr(arr);\
}

#define Out(arr) \
{\
std::cout << #arr ": [";\
out(arr);\
}

#include "dynamic_array.h"
#include <iostream>

int main(int argc, char **argv)
{
	Array<int32_t> arr;
	int32_t element = 78;
	arr.push_back(element);
	std::cout << "Element: " << arr[0] << std::endl;
	std::cout << "Last element: " << arr.back() << std::endl;
	arr.pop_back();
	std::cout << "Length: " << arr.length() << std::endl;
	for (int32_t index = 0; 
		index < 3; 
		++index)
	{
		arr.push_back(index);
	}
	Out(arr);
	arr.clear();
	std::cout << "After arr.clear()" << std::endl;
	Out(arr);
	assert(arr.empty());
	arr.push_back(1);
	arr.push_back(24);
	arr.push_back(56);
	arr.push_back(78);
	Out(arr);
	OutItr(arr);
	Array<int32_t> arr1 = arr;
	OutItr(arr1);
	Array<int32_t> arr2;
	populate(arr2, 6);
	arr1 = arr2;
	OutItr(arr1);
	
	arr1 = std::move(arr);
	OutItr(arr1);
	OutItr(arr);
	Array<int32_t> arr3 = std::move(arr2);
	OutItr(arr3);
	OutItr(arr2);

	Array<int32_t> arr4{ 109, 1234, 78, 99, 104 };
	std::cout << "Before erasing: " << std::endl;
	OutItr(arr4);
	std::cout << "After erasing: " << std::endl;
	arr4.erase(arr4.begin() + 2);
	OutItr(arr4);
	std::cout << "Erasing the first element..." << std::endl;
	arr4.erase(arr4.begin());
	OutItr(arr4);
	std::cout << "Removing the last element..." << std::endl;
	arr4.erase(arr4.end() - 1);
	OutItr(arr4);
	populate(arr4, 5);
	OutItr(arr4);
	std::cout << "Erasing a range: " << std::endl;
	arr4.erase_range(arr4.begin() + 1, arr4.begin() + 5);
	OutItr(arr4);
	std::cout << "Size: " << arr4.length() << std::endl;
	arr4.push_back(34545);
	std::cout << "Size: " << arr4.capacity() << std::endl;
	arr4.clear();
	std::cout << "Size: " << arr4.length() << std::endl;

	return 0;
}
```
