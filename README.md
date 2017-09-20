# Assignment 3

1. Github Account has been created.  My username is bart3251.
2. Code in C++ for finding a fixed point iteration using hardcoded functions and params.

```C++
#include <iostream>
#include <cmath>
using namespace std;

double f(double x) {
	//return x + 1;	//basic test for error
	//return x - 1;	//basic test for root
	//return 3*x*sin(10*x);	//test a
	return x*exp(-x);	//test b
}
double fpiter(double a, double b, double tol, int maxiter) {
	double error = 10 * tol;
	double fa = f(a);
	double fb = f(b);
	double c = 0; 
	double fc = 0;
	if (fa*fb > 0) {
		cout << "Error" << endl;
		return(NULL);
	}
	int cnt = 0;
	while (error > tol && cnt < maxiter) {
		c = 0.5*(a + b);
		fc = f(c);
		if (fc == 0) {
			return c;
		}
		if (fa*fc < 0) {
			b = c;
			fb = fc;
		}else {
			a = c;
			fa = fc;
		}
		error = b - a;
		cnt++;
	}
	return c;
}
int main() {
	double a = -1;
	double b = 10;
	int resolution = 8;
	double tol = pow(10,resolution);
	double maxiter = pow(10,resolution+2);
	cout<<fpiter(a,b,tol,maxiter)<<endl;

	return 0;
}
```
3. Tested values for the functions resulted in the following:
For f(x) = 3xsin(10x)and initial params a=0, b=7, the function outputted 5.02654, which is indeed a root.
For f(x) = xe(-x), and initial params a=-9.9, b=10, the function outputted 2.14577e-06, which is also a root.
4.  Software manual saved under project assn3 as "manual.md", and is copied below:

# fpiter(double a, double b, double tol, int maxiters)
Currently, the function fpiter is at the disadvantage that it must have a hardcoded function, f, in order to function.  Future edits may resolve this problem.  The function itself is a implementation of the fixed point numerical operation to finding a root of a function.  It takes as inputs: a,b,f (as a hardcoded function aforementioned), tol, and matiters.  It then gives the output c.

a is the lower bound of the function stored as a double

b is the upper bound of the function stored as a double

f is an exterior routine that is hardcoded as a mathematical operation, and must be able to take in a double and return a double modified by the function.

tol is the tolerance of our fixed point iteration, stored as a double, and is preferably small with respect to the size of the function.

maxiters is the maximum number of iterations the function will run before it will automatically terminate.

c is the double that is returned, which is an x-intercept of the function f.

The function first stores a double "error" as ten times the tolerance.  It then checks to ensure that there is f(a) and f(b) are not of the same signs, thus we would be guaranteed an answer via the mean value theorem.  Then the function begins the process of iterating through different a's and b's to narrow down a 0 until such time that the value of the error has been reduced below the tolerance or when it has exceeded the maximum number of iterations. Finally the function returns the value of c, the estimated 0 of the function.
