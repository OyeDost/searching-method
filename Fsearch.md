#include "stdafx.h"
#include <iostream>
using namespace std;

class Data
{
private:
	int i, n, *ary;
	int f1, f2, fibm;
public:
	void read_data();
	int Fsearch_data(int);
	int min(int,int);
};

void Data::read_data()
{
	cout << "\n Enter the aryay size : ";
	cin >> n;

	ary = new int[n];
	cout << "\n Enter " << n << " Elements : ";
	for (i = 0; i<n; i++)
		cin >> ary[i];
}

int Data::Fsearch_data(int x)
{
	 int f1 = 0, f2 = 1; 
    int fibM = f1 + f2;  // m'th Fibonacci
 
    while (fibM < n)
    {
        f1 = f2;
        f2 = fibM;
        fibM  = f1 + f2;
    }
 
    int offset = -1;
 
    while (fibM > 1)
    {
        int i = min(offset+f1, n-1);
        if (ary[i] < x)
        {
            fibM  = f2;
            f2 = f1;
            f1 = fibM - f2;
            offset = i;
        }
        else if (ary[i] > x)
        {
            fibM  = f1;
            f2 = f2 - f1;
            f1 = fibM - f2;
        }
     else 
		 return i;
    }
 
    if(f2 && ary[offset+1]==x) return offset+1;
    return -1;
}
int Data::min(int x, int y) { 
	return (x <= y) ? x : y; 
}
int main()
{
	Data obj;
	int key, p;
	//clrscr();

	obj.read_data();

	cout << "\n Enter the element to search  : ";
	cin >> key;
	p = obj.Fsearch_data(key);

	if (p == -1)
		cout << "\n Element not found \n";
	else
		cout << "\n Element found at position " << p <<endl;
}
