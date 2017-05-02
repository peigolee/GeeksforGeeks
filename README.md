# GeeksforGeeks

Point *t1, *t2;   // No constructor call
t1 = new Point(10, 15);  // Normal constructor call
t2 = new Point(*t1);   // Copy constructor call 
Point t3 = *t1;  // Copy Constructor call
Point t4;   // Normal Constructor call
t4 = t3;   // Assignment operator call 


---------------------

#include <iostream>
using namespace std;
 
class Point
{
    int x, y;
public:
   Point(const Point &p) { x = p.x; y = p.y; }
   int getX() { return x; }
   int getY() { return y; }
};
 
int main()
{
    Point p1;
    Point p2 = p1;
    cout << "x = " << p2.getX() << " y = " << p2.getY();
    return 0;
}


There is compiler error in line "Point p1;". The class Point doesn't have a constructor without any parameter. If we write any constructor, then compiler doesn't create the default constructor. It is not true other way, i.e., if we write a default or parameterized constructor, then compiler creates a copy constructor. See the next question.

-----------------------

initializer_list
http://en.cppreference.com/w/cpp/utility/initializer_list


--------------------

#include<iostream>
#include<string.h>
using namespace std;

class String
{
    char *str;
public:
     String(const char *s);
     void change(int index, char c) { str[index] = c; }
     char *get() { return str; }
};

String::String(const char *s)
{
    int l = strlen(s);
    str = new char[l+1];
    strcpy(str, s);
}

int main()
{
   String s1("geeksQuiz");
   String s2 = s1;
   s1.change(0, 'G');
   cout << s1.get() << " ";
   cout << s2.get();
}

Question 11 Explanation: 
Since there is no copy constructor, the compiler creates a copy constructor. The compiler created copy constructor does shallow copy in line " String s2 = s1;" So str pointers of both s1 and s2 point to the same location. There must be a user defined copy constructor in classes with pointers ot dynamic memory allocation.

------------------

Objects must be passed by reference in copy constructors. Compiler checks for this and produces compiler error if not passed by reference. The following program compiles fine and produces output as 10.
#include <iostream >
using namespace std;
class Point {
    int x;
public:
    Point(int x) { this->x = x; }
    Point(const Point &p) { x = p.x;}
    int getX() { return x; }
};

int main()
{
   Point p1(10);
   Point p2 = p1;
   cout << p2.getX();
   return 0;
}
The reason is simple, if we don't pass by reference, then argument p1 will be copied to p. So there will be a copy constructor call to call the copy constructor, which is not possible.



#include<iostream>
using namespace std;
class Point {
    int x;
public:
    Point(int x) { this->x = x; }
    Point(const Point p) { x = p.x;}
    int getX() { return x; }
};

int main()
{
   Point p1(10);
   Point p2 = p1;
   cout << p2.getX();
   return 0;
}

Compiler Error: p must be passed by reference

--------------


http://www.geeksforgeeks.org/when-do-we-use-initializer-list-in-c/



---------------------------


If a class has a constructor which can be called with a single argument, then this constructor becomes conversion constructor because such a constructor allows automatic conversion to the class being constructed. A conversion constructor can be called anywhere when the type of single argument is assigned to the object. The output of the given program is

#include <iostream>
using namespace std;
class Test
{
private:
    int x;
public:
    Test(int i)
    {
        x = i;
        cout << "Called" << endl;
    }
};

int main()
{
    Test t(20);
    t = 30; // conversion constructor is called here.
    return 0;
}


Called
Called


-------------------

Why copy constructor argument should be const in C++?
http://www.geeksforgeeks.org/copy-constructor-argument-const/




