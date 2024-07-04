# kStatistics
### July 24, 2024

### Unbiased Estimators for Cumulant Products and Faa Di Bruno's Formula

### Description

kStatistics is a package producing estimates of (joint) cumulants and (joint) cumulant products
of a given dataset, using (multivariate) k-statistics and (multivariate) polykays, which are symmetric unbiased estimators. The procedures rely on a symbolic method arising from the classical
umbral calculus and described in the referred papers. In the package, a set of combinatorial tools
are given useful in the construction of these estimations such as integer partitions, set partitions,
multiset subdivisions or multi-index partitions, pairing and merging of multisets. In the package,
there are also functions to recover univariate and multivariate cumulants from a sequence of univariate and multivariate moments (and vice-versa), using Faa di Bruno’s formula. The function
producing Faa di Bruno’s formula returns coefficients of exponential power series compositions
such as $f[g(z)]$ with $f$ and $g$ both univariate, or $f[g(z1,...,zm)]$ with $f$ univariate and $g$ multivariate, or $f[g1(z1,...,zm),...,gn(z1,...,zm)]$ with $f$ and $g$ both multivariate. Let us recall
that Faa di Bruno’s formula might also be employed to recover iterated (partial) derivatives of all
these compositions. Lastly, using Faa di Bruno’s formula, some special families of polynomials are
also generated, such as Bell polynomials, generalized complete Bell polynomials, partition polynomials and generalized partition polynomials. Applications of these polynomials are described in
the referred papers.

### Presentation of the functions and their use

### countP

#### Description

The function computes the multiplicity of a multi-index partition. Note that a multi-index partition
corresponds to a subdivision of a multiset having the input multi-index as multiplicities.

#### Usage
```
countP( v=[1] )
```
#### Argument
A list 
#### Value
An integer
#### Examples
```
countP([2,1])
```
Returns 3 which is the multiplicity of [1,2], partition of the integer 3, or of [[a],[a,a]], subdivision of the multiset [a,a,a].
```
3
```
```
countP([4,2])
```
Return 15 which is the multiplicity of [4,2], partition of the integer 6, or of [[a,a,a,a],[a,a]], subdivision of the multiset [a,a,a,a,a,a].
```
15
```
```
countP( [[2,0], [1,0], [1,0], [0,1], [0,2]] )
```
Return 18 which is the multiplicity of [[2,0], [1,0], [1,0], [0,1], [0,2]], partition of the multi-index (4,3), or of [[b],[b,b],[a],[a],[a,a]], subdivision of the multiset [a,a,a,a,b,b,b].

### cum2mom

#### Description
The function computes a simple or a multivariate cumulant in terms of simple or multivariate moments.
#### Usage
```
cum2mom(n = 1)
```
#### Argument
n integer or vector of integers.
#### Value
String
#### Examples
```
cum2mom(5)
```
Returns the simple cumulant k[5] in terms of the simple moments m[1],..., m[5].
```
24m[1]^5 - 60m[1]^3m[2] + 30m[1]m[2]^2 + 20m[1]^2m[3] - 10m[2]m[3] - 5m[1]m[4] + m[5]
```
```
cum2mom([3,1])
```
Returns the multivariate cumulant k[3,1] in terms of the multivariate moments m[i,j] for i=0,1,2,3 and j=0,1.
```
- 6m[0,1]m[1,0]^3 + 6m[0,1]m[1,0]m[2,0] - m[0,1]m[3,0] + 6m[1,0]^2m[1,1] - 3m[1,0]m[2,1] - 3m[1,1]m[2,0] + m[3,1]
```
### eBellPol
#### Description
The function generates a complete or a partial exponential Bell polynomial.
#### Usage
```
eBellPol(n = 1, m = 0)
```
#### Argument
n integer, the degree of the polynomial

m integer, the fixed degree of each monomial in the polynomial
#### Value
String, the expression of the exponential Bell polynomial
#### Examples
```
eBellPol(5)
```
Returns the complete exponential Bell Polynomial for n=5, that is
```
(y1**5) + 10(y1**3)(y2) + 15(y1)(y2**2) + 10(y1**2)(y3) + 10(y2)(y3) + 5(y1)(y4) + (y5)
```
```
eBellPol(5,3)
```
Returns the partial exponential Bell Polynomial for n=5 and m=3, that is
```
15(y1)(y2**2) + 10(y1**2)(y3)
```
### e_eBellPol
#### Description
The function evaluates a complete or a partial exponential Bell polynomial (output of the eBellPol
function) when its variables are substituted with numerical values
#### Usage
```
e_eBellPol(n=1, m=0, v=None)
```
#### Argument
n integer, the degree of the polynomial

m integer, the fixed degree of each monomial in the polynomial

v vector, the numerical values in place of the variables of the polynomial

#### Value
int, the value assumed by the polynomial.
#### Warnings
By default, the function returns the Stirling numbers of second kind.
#### Examples
```
e_eBellPol(5,3)
```
Returns S(5,3) = 25 (where S=Stirling number of second kind).
```
25
```
Or (same output)
```
e_eBellPol(5, 3, [1, 1, 1, 1, 1])
```
```
25
```
```
e_eBellPol(5)
```
Returns B5=52 (where B5 is the 5-th Bell number).
```
52
```
Or (same output)
```
e_eBellPol(5,0)
52
```
Or (same output)
```
e_eBellPol(5, 0, [1, 1, 1, 1, 1])
52
```
```
e_eBellPol(5,3,[1,-1,2,-6,24])
```
Return s(5,3) = 35 (where s=Stirling number of first kind).
```
35
```
### e_GCBellPol
#### Description
The function evaluates a generalized complete Bell polynomial (output of the GCBellPol function)
when its variables and/or its coefficients are substituted with numerical values.
#### Usage
```
e_GCBellPol(pv=[], pn=0, pyc=[], pc=[], b=False)
```
#### Argument
pv vector of integers, the subscript of the polynomial

pn integer, the number of variables

pyc vector, the numerical values into the variables [optional], or the string with the

direct assignment into the variables and/or the coefficients

pc vector, the numerical values into the coefficients, [optional if pyc is a string]

b boolean, if TRUE the function prints the list of all the assignments
#### Value
string or numerical, the evaluation of the polynomial
#### Warnings
The value of the first parameter is the same as the mkmSet function.
#### Examples
#####  Evaluation of the generalized complete Bell polynomial with subscript 2
The polynomial (y^2)g[1]^2 + (y^1)g[2], output of
```
GCBellPol( [2],1 )
```
when
g[1]=3 and g[2]=4
```
e_GCBellPol( [2], 1, [], [3,4] )
```
```
9(y^2) + 4(y)
```
OR (same output)
```
e_GCBellPol( [2], 1, "g[1]=3,g[2]=4" )
```
```
9(y^2) + 4(y)
```
Check the assignments setting the boolean parameter equals to True, that is g[1]=3
and g[2]=4
```
e_GCBellPol( [2], 1, [], [3,4], True )
```
```
y=, g[1]=3, g[2]=4
```
The numerical value of (y^2)g[1]^2 + (y^1)g[2], output of 
```
GCBellPol( c(2),1 )
```
when g[1]=3 and g[2]=4 and y=7, that is 469
```
e_GCBellPol( [2], 1, [7], [3,4] )
```
```
469
```
OR (same output)
```
e_GCBellPol( [2], 1, "y=7, g[1]=3,g[2]=4" )
```
Check the assignments setting the boolean parameter equals to True, that is g[1]=3
and g[2]=4 and y=7
```
e_GCBellPol( [2], 1, [7], [3,4], True )
```
```
y=7, g[1]=3, g[2]=4
```
##### Evaluation of the generalized complete Bell polynomial with subscript (2,1)
The polynomial 2(y^2)g[1,1]g[1,0] + (y^3)g[1,0]^2g[0,1] + (y)g[2,1] + (y^2)
g[2,0]g[0,1], output of
```
GCBellPol( [2,1], 1 )
```
 when g[0,1]=1, g[1,0]=2, g[1,1]=3,
g[2,0]=4, g[2,1]=5, that is 16(y^2) + 4(y^3) + 5(y)
```
import numpy as np

e_GCBellPol([2,1], 1, [], np.arange(1,6))
```
```
4(y^3) + 16.0(y^2) + 5(y)
```
Or (same output)
```
e_GCBellPol([2,1], 1, [], [1,2,3,4,5])
```
OR (same output)
```
e_GCBellPol( [2,1], 1, "g[0,1]=1, g[1,0]=2, g[1,1]=3, g[2,0]=4, g[2,1]=5" )
```
Check the assignments setting the boolean parameter equals to True, that is
g[0,1]=1, g[1,0]=2, g[1,1]=3, g[2,0]=4, g[2,1]=5
```
import numpy as np

e_GCBellPol( [2,1], 1, [], np.arange(1,6), True )
```
```
y=, g[0,1]=1, g[1,0]=2, g[1,1]=3, g[2,0]=4, g[2,1]=5
```
The numerical value of 2(y^2)g[1,1]g[1,0] + (y^3)g[1,0]^2g[0,1] + (y)g[2,1] + (y^2)
g[2,0]g[0,1], output of 
```
GCBellPol( [2,1], 1 )
```
when g[0,1]=1, g[1,0]=2,
g[1,1]=3, g[2,0]=4, g[2,1]=5 and y=7, that is 2191
```
import numpy as np

e_GCBellPol( [2,1], 1, [7], np.arange(1,6) )
```
```
2191
```
Or (same output)
```
e_GCBellPol( [2,1], 1, "y=7, g[0,1]=1, g[1,0]=2, g[1,1]=3, g[2,0]=4, g[2,1]=5" )
```
```
2191
```
Check the assignments setting the boolean parameter equals to True, that is
g[0,1]=1, g[1,0]=2, g[1,1]=3, g[2,0]=4, g[2,1]=5, y=7
```
import numpy as np

e_GCBellPol( [2,1], 1, [7], np.arange(1,6) )
```
```
y=7, g[0,1]=1, g[1,0]=2, g[1,1]=3, g[2,0]=4, g[2,1]=5
```
#####
Evaluation of the generalized complete Bell Polynomial with subscript (1,1)
The polynomial (y1)g1[1,1] + (y1^2)g1[1,0]g1[0,1] + (y2)g2[1,1] + (y2^2)g2[1,0]
g2[0,1] + (y1)(y2)g1[1,0]g2[0,1] + (y1)(y2)g1[0,1]g2[1,0], output of 
```
GCBellPol([1,1], 2)
```
when g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, g2[1,1]=6, that is
3(y1) + 2(y1^2) + 6(y2) + 20(y2^2) + 13(y1)(y2)
```
import numpy as np

e_GCBellPol( [1,1], 2, [], np.arange(1,7))
```
```
13.0(y1)(y2) + 2(y1^2) + 3(y1) + 20(y2^2) + 6(y2)
```
O (same output)
```
e_GCBellPol([1,1], 2, [], [1,2,3,4,5,6])
```
```
13.0(y1)(y2) + 2(y1^2) + 3(y1) + 20(y2^2) + 6(y2)
```
Or (same output)
```
e_GCBellPol( [1,1], 2, "g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, g2[1,1]=6" )
```
```
13.0(y1)(y2) + 2(y1^2) + 3(y1) + 20(y2^2) + 6(y2)
```
Check the assignments setting the boolean parameter equals to True, that is
g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, g2[1,1]=6
```
import numpy as np

e_GCBellPol( [1,1], 2, [], np.arange(1,7), True )
```
```
y1=, y2=, g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, g2[1,1]=6
```
The numerical value of (y1)g1[1,1] + (y1^2)g1[1,0]g1[0,1] + (y2)g2[1,1] + (y2^2)g2[1,0]
g2[0,1] + (y1)(y2)g1[1,0]g2[0,1] + (y1)(y2)g1[0,1]g2[1,0], output of
```
GCBellPol([1,1], 2)
```
when g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, y1=7 and y2=8, that is 2175
```
import numpy as np

e_GCBellPol( [1,1], 2, [7,8], np.arange(1,7))
```
```
2175
```
Or (same output)
```
cVal="y1=7, y2=8, g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5,g2[1,1]=6"
e_GCBellPol([1,1], 2, cVal)
```
```
2175
```
To recover which coefficients and variables are involved in the generalized complete
Bell polynomial, run the 
```
e_GCBellPol
```
function without any assignment.
```
e_GCBellPol([1, 1], 2)
```
The error message prints which coefficients and variables are involved, that is
```
ValueError: The third parameter must contain the 2 values of y: y1 y2.
 The fourth parameter must contain the 6 values of g: g1[0,1] g1[1,0] g1[1,1] g2[0,1] g2[1,0] g2[1,1]
```
To assign correctly the values to the coefficients and the variables:
1) run
```
e_GCBellPol(c(1, 1), 2)
```
and get the errors with the indication of the involved
coefficients and variables, that is
```
ValueError: The third parameter must contain the 2 values of y: y1 y2.
 The fourth parameter must contain the 6 values of g: g1[0,1] g1[1,0] g1[1,1] g2[0,1] g2[1,0] g2[1,1]
```
2) initialize g1[0,1] g1[1,0] g1[1,1] g2[0,1] g2[1,0] g2[1,1] with - for example - the
first 6 integer numbers and do the same for y1 and y2, that is
```
e_GCBellPol([1,1], 2, [1,2], [1,2,3,4,5,6], True)
```
3) trough the boolean value True, recover the string y1=1, y2=1, g1[0,1]=1, g1[1,0]=2,
g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, g2[1,1]=6
4) copy and past the string in place of "..." when run
```
e_GCBellPol(c(1,1),2,"...")
```
5) change the assignments if necessar
```
cVal="y1=10,y2=11,g1[0,1]=1.1,g1[1,0]=-2,g1[1,1]=3.2,g2[0,1]=-4,g2[1,0]=10,g2[1,1]=6"
e_GCBellPol([1,1], 2, cVal)
```
```
-2872.0
```
### e_MFB
#### Description
The function evaluates the Faa di Bruno’s formula, output of the MFB function, when the coefficients
of the exponential formal power series f and g1,...,gn in the composition f[g1(),...,gn()] are
substituted with numerical values.
#### Usage
```
e_MFB(pv=[], pn=0, pf=[], pg=[], b=False)
```
#### Argument
pv vector of integers, the subscript of Faa di Bruno’s formula

pn integer, the number of the inner formal power series "g"

pf vector, the numerical values in place of the coefficients of the outer formal power
series "f" or the string with the direct assignments in place of the coefficients
of both "f" and "g"

pg vector, the numerical values in place of the coefficients of the inner formal power
series "g" [Optional if pf is a string]

b boolean

#### Value
numerical, the evaluation of Faa di Bruno’s formula
#### Warnings
The value of the first parameter is the same as the mkmSet function.
#### Examples
The numerical value of f[1]g[1,1] + f[2]g[1,0]g[0,1], that is the coefficient of z1z2 in
$f(g1(z1,z2),g2(z1,z2)))$, output of 
```
MFB(c(1,1),1)
```
when
f[1] = 5 and f[2] = 10,
g[0,1]=3, g[1,0]=6, g[1,1]=9
```
e_MFB([1,1], 1, [5,10], [3,6,9])
```
```
225
```
Same as the previous example, with a string of assignments as third input parameter
```
e_MFB([1,1], 1, "f[1]=5, f[2]=10, g[0,1]=3, g[1,0]=6, g[1,1]=9")
```
```
225
```
Use the boolean parameter to verify the assignments to the coefficients of "f" and "g",
that is f[1]=5, f[2]=10, g[0,1]=3, g[1,0]=6, g[1,1]=9
```
e_MFB([1,1], 1, [5,10], [3,6,9], True)
```
```
f[1]=5, f[2]=10, g[0,1]=3, g[1,0]=6, g[1,1]=9
```
To recover which coefficients are involved, run the function without any assignment.
The error message recalls which coefficients are necessary, that is
```
e_MFB([1,1], 1)
```
```
ValueError: The third parameter must contain the 2 values of f: f[1] f[2]. The fourth parameter must contain the 3 values of g: g[0,1] g[1,0] g[1,1]
```
To assign correctly the values to the coefficients of "f" and "g" when the functions
become more complex:
1) run
```
e_MFB([1,1], 2)
```
and get the errors with the indication of the involved coefficients
of "f" and "g", that is
```
ValueError: The third parameter must contain the 5 values of f: f[0,1] f[0,2] f[1,0] f[2,0] f[1,1]. The fourth parameter must contain the 6 values of g: g1[0,1] g2[1,0] g1[1,0] g2[0,1] g1[1,1] g2[1,1]
```
2) initialize f[0,1] f[0,2] f[1,0] f[1,1] f[2,0] with - for example - the first 5 integer
numbers and do the same for g1[0,1] g1[1,0] g1[1,1] g2[0,1] g2[1,0] g2[1,1], that is
```
import numpy as np

e_MFB([1,1], 2, np.arange(1,6), np.arange(1,7), True)
```
```
f[0,1]=1, f[0,2]=2, f[1,0]=3, f[2,0]=4, f[1,1]=5, g1[0,1]=1, g2[1,0]=2, g1[1,0]=3, g2[0,1]=4, g1[1,1]=5, g2[1,1]=6
```
3) trough the boolean value True, recover the string f[0,1]=1, f[0,2]=2, f[1,0]=3, f[1,1]=4,
f[2,0]=5, g1[0,1]=1, g1[1,0]=2, g1[1,1]=3, g2[0,1]=4, g2[1,0]=5, g2[1,1]=6
4) copy and past the string in place of " ... " when run
```
e_MFB([1,1], 1, " ... ")
```
5) change the assignments if necessary
```
cfVal = "f[0,1]=2, f[0,2]=5, f[1,0]=13, f[1,1]=-4, f[2,0]=0"


cgVal = "g1[0,1]=-2.1, g1[1,0]=2, g1[1,1]=3.1, g2[0,1]=5, g2[1,0]=0, g2[1,1]=6.1"


cVal = cfVal + "," + cgVal


result = e_MFB((1, 1), 2, cVal)
print(result)
```
```
12.500000000000004
```
### ff
#### Description
The function computes the descending (falling) factorial of a positive integer n with respect to a
positive integer k less or equal to n.
#### Usage
```
ff( n=1, k )
```
#### Argument
n integer

k integer
#### Value
int, the descending factorial
#### Examples
```
ff(6,3)
```
```
120
```
### GCBellPol
#### Description
The function generates a generalized complete Bell polynomial, that is a coefficient of the composition 

exp(y[1] g1(z1,...,zm) + ... + y[n] gn(z1,...,zm)),

where y[1],...,y[n] are variables. The input vector of integers identifies the subscript of the polynomial.

#### Usage
```
GCBellPol(nv=[], m=1, b=False)
```
#### Argument
nv vector of integers, the subscript of the polynomial, corresponding to the powers
of the product among z1, z2, ..., zm

m integer, the number of z’s variables

b boolean, TRUE if the inner formal power series "g" are all equal
#### Value
str, the expression of the polynomial
#### Warnings
The value of the first parameter is the same as the mkmSet function
#### Examples
Returns the generalized complete Bell Polynomial for n=1, m=1 and g1=g,
that is (y^2)g[1]^2 + (y)g[2]
```
GCBellPol( [2], 1 )
```
```
(y**2)g[1]^2 + (y)g[2]
```
Returns the generalized complete Bell Polynomial for n=1, m=2 and g1=g,
2(y^2)g[1,0]g[1,1] + (y^3)g[0,1]g[1,0]^2 + (y)g[2,1] + (y^2)g[0,1]g[2,0]
```
GCBellPol( [2,1], 1 )
```
```
(y**3)g[0,1]g[1,0]^2 + (y**2)g[0,1]g[2,0] + 2(y**2)g[1,0]g[1,1] + (y)g[2,1]
```
Returns the generalized complete Bell Polynomial for n=2, m=2 and g1=g2=g,
(y1)g[1,1] + (y1^2)g[0,1]g[1,0] + (y2)g[1,1] + (y2^2)g[0,1]g[1,0] + 2(y1)(y2)g[0,1]g[1,0]
```
GCBellPol( [1,1], 2, True )
```
```
2(y1)(y2)g[0,1]g[1,0] + (y1**2)g[0,1]g[1,0] + (y1)g[1,1] + (y2**2)g[0,1]g[1,0] + (y2)g[1,1]
```
Returns the generalized complete Bell Polynomial for n=2, m=2 and g1 different from g2,
that is (y1)g1[1,1] + (y1^2)g1[1,0]g1[0,1] + (y2)g2[1,1] + (y2^2)g2[1,0]g2[0,1] +
(y1)(y2)g1[1,0]g2[0,1] + (y1)(y2)g1[0,1]g2[1,0]
```
GCBellPol( [1,1], 2 )
```
```
(y1)(y2)g1[0,1]g2[1,0] + (y1)(y2)g1[1,0]g2[0,1] + (y1**2)g1[0,1]g1[1,0] + (y1)g1[1,1] + (y2**2)g2[0,1]g2[1,0] + (y2)g2[1,1]
```
### gpPart 
#### Description
The function returns a general partition polynomial.
#### Usage
```
gpPart(n = 0)
```
#### Argument
n integer
#### Value
str, the expression of the polynomial 
#### Warnings
The value of the first parameter is the same as the MFB function in the univariate with univariate
composition.
#### Examples
Return the general partition polynomial G[a1,a2; y1,y2], that is a2(y1^2) + a1(y2)
```
gpPart(2)
```
```
a2(y1**2) + a1(y2)
```
Return the general partition polynomial G[a1,a2,a3,a4,a5; y1,y2,y3,y4,y5], that is
a5(y1^5) + 10a4(y1^3)(y2) + 15a3(y1)(y2^2) + 10a3(y1^2)(y3) + 10a2(y2)(y3) + 5a2(y1)(y4)
+ a1(y5)
```
gpPart(5)
```
```
a5(y1**5) + 10a4(y1**3)(y2) + 15a3(y1)(y2**2) + 10a3(y1**2)(y3) + 10a2(y2)(y3) + 5a2(y1)(y4) + a1(y5)
```
### intPart 
#### Description
The function generates all possible (unique) decomposition of a positive integer n in the sum of
positive integers less or equal to n.
#### Usage
```
intPart(n=0 ,vOutput = FALSE)
```
#### Argument
n : integer

vOutput : optional boolean parameter, if equal to TRUE the function produces a compact
output that is easy to read.
#### Value
list, all the partitions of n
#### Examples
Return the partition of the integer 3, that is
[1,1,1],[1,2],[3]
```
intPart(3)
```
```
[[1, 1, 1], [1, 2], [3]]
```
Return the partition of the integer 4, that is
[1,1,1,1],[1,1,2],[1,3],[2,2],[4]
```
intPart(4)
```
```
[[1, 1, 1, 1], [1, 1, 2], [2, 2], [1, 3], [4]]
```
Or (same output)
```
intPart(4, False)
```
```
[[1, 1, 1, 1], [1, 1, 2], [2, 2], [1, 3], [4]]
```
Return the same output as the previous example but in a compact expression
```
intPart(4, TRUE)
```
```
[1, 1, 1, 1]
[1, 1, 2]
[2, 2]
[1, 3]
[4]
None
```
### list2m 

#### Description
The function returns the multiset representation of a vector or a list, in increasing order
#### Usage
```
list2m(v=[0])
```
#### Argument
v : single vector or list of vectors
#### Value
multiset, the list of multisets
#### Examples
Returns the list of multisets [[1],3], [[2],1] from the input vector (1,2,1,1)
```
list2m([1,2,1,1])
```
```
[[[1], 3], [[2], 1]]
```
Returns the list of multisets [[1,2],2], [[2,3],1] from the input [[1,2], [2,3], [1,2]]
```
list2m([[1,2], [2,3], [1,2]])
```
```
[[[1, 2], 2], [[2, 3], 1]]
```
### list2Set
#### Description
Given a list, the function deletes the instances of an element in the list, leaving the order inalterated.
#### Usage
```
list2Set(v=[0])
```
#### Argument
v : single vector or list of vectors
#### Value
set, the sequence of distinct elements
#### Examples
Returns the vector [1,2,3,5,6]
```
list2Set([1,2,3,1,2,5,6])
```
```
[1, 2, 3, 5, 6]
```
Returns the list [[1,2], [10,11], [7,8]]
```
list2Set([[1,2], [1,2], [10,11], [1,2], [7,8]])
```
```
[[1, 2], [10, 11], [7, 8]]
```
### m2Set
#### Description
The function returns the vectors (only counted once) of all the multi-index partitions output of the
mkmSet function. These vectors correspond also to the blocks of the subdivisions of the multiset
having the given multi-index as multeplicites.
#### Usage
```
m2Set(v=[0])
```
#### Argument
v : sequence of type [[e1,e2,...], m1], [[f1,f2,...], m2],... with m1, m2,...
multiplicities
#### Value
set, the sequence with distinct elements
#### Examples
M1 = mkmSet([2,1])
M1 is
[
    [ [[0, 1], [1, 0], [1, 0]], 1 ],
    [ [[0, 1], [2, 0]], 1 ],
    [ [[1, 0], [1, 1]], 2 ],
    [ [[2, 1]], 1 ]
]
To print all the partitions of the multi-index (2,1) run 
```
mkmSet([2,1], True)
```
```
[( 0 1 )( 1 0 )( 1 0 ), 1 ]
[( 0 1 )( 2 0 ), 1 ]
[( 1 0 )( 1 1 ), 2 ]
[( 2 1 ), 1 ]
```
Then m2Set(M1) returns the following set: [[0,1],[1,0],[2,0],[1,1],[2,1]]
```
m2Set( M1 )
```
```
[[0, 1], [1, 0], [2, 0], [1, 1], [2, 1]]
```
### mCoeff
#### Description
Given a list containing vectors paired with numbers, the function returns the number paired with
the vector matching the one passed in input.
#### Usage
```
mCoeff(v=None, L=None)
```
#### Argument
v : vector to be searched in the list

L : two-dimensional list: in the first there is a vector and in the second a number
#### Value
float, the number paired with the input vector
#### Examples
Run
```
mkmSet([3])
```
to get the list
```
L1 = [[[1,1,1],1], [[1,2],3], [[3],1]]
```
```
L1 = mkmSet([3])
```
Returns the number 3, which is the number paired with [1,2] in L1
```
mCoeff( [1,2], L1)
```
```
3
```
### MFB
#### Description
The function returns the coefficient indexed by the integers i1,i2,... of an exponential formal
power series composition through the univariate or multivariate Faa di Bruno’s formula.
#### Usage
```
MFB(v=[], n=0)
```
#### Argument
v : vector of integers, the subscript of the coefficient

n : integer, the number of inner functions g’s
#### Value
str,  the expression of Faa di Bruno’s formula
#### Warnings
The value of the first parameter is the same as the mkmSet function
#### Examples
##### Univariate f with Univariate g
The coefficient of z^2 in f[g(z)], that is f[2]g[1]^2 + f[1]g[2], where

f[1] is the coefficient of x in f(x) with x=g(z)

f[2] is the coefficient of x^2 in f(x) with x=g(z)

g[1] is the coefficient of z in g(z)

g[2] is the coefficient of z^2 in g(z)
```
MFB( [2], 1 )
```
```
f[2]g[1]^2 + f[1]g[2]
```
The coefficient of z^3 in f[g(z)], that is f[3]g[1]^3 + 3f[2]g[1]g[2] + f[1]g[3]
```
MFB( [3], 1 )
```
```
f[3]g[1]^3 + 3f[2]g[1]g[2] + f[1]g[3]
```
##### Univariate f with Multivariate g
The coefficient of z1 z2 in f[g(z1,z2)], that is f[1]g[1,1] + f[2]g[1,0]g[0,1]
where

f[1] is the coefficient of x in f(x) with x=g(z1,z2)

f[2] is the coefficient of x^2 in f(x) with x=g(z1,z2)

g[1,0] is the coefficient of z1 in g(z1,z2)

g[0,1] is the coefficient of z2 in g(z1,z2)

g[1,1] is the coefficient of z1 z2 in g(z1,z2)
```
MFB( [1,1], 1 )
```
```
f[2]g[0,1]g[1,0] + f[1]g[1,1]
```
The coefficient of z1^2 z2 in f[g(z1,z2)]
```
MFB( [2,1], 1 )
```
```
f[3]g[0,1]g[1,0]^2 + f[2]g[0,1]g[2,0] + 2f[2]g[1,0]g[1,1] + f[1]g[2,1]
```
The coefficient of z1 z2 z3 in f[g(z1,z2,z3)]
```
MFB( [1,1,1], 1 )
```
```
f[3]g[0,0,1]g[0,1,0]g[1,0,0] + f[2]g[0,0,1]g[1,1,0] + f[2]g[0,1,0]g[1,0,1] + f[2]g[0,1,1]g[1,0,0] + f[1]g[1,1,1]
```
#####  Multivariate f with Univariate/Multivariate g1, g2, ..., gn
The coefficient of z in f[g1(z),g2(z)], that is f[1,0]g1[1] + f[0,1]g2[1] where

f[1,0] is the coefficient of x1 in f(x1,x2) with x1=g1(z) and x2=g2(z)

f[0,1] is the coefficient of x2 in f(x1,x2) with x1=g1(z) and x2=g2(z)

g1[1] is the coefficient of z of g1(z)

g2[1] is the coefficient of z of g2(z)
```
MFB( [1], 2 )
```
```
f[1,0]g1[1] + f[0,1]g2[1]
```
The coefficient of z1 z2 in f[g1(z1,z2),g2(z1,z2)], that is

f[1,0]g1[1,1] + f[2,0]g1[1,0]g1[0,1] + f[0,1]g2[1,1] + f[0,2]g2[1,0]g2[0,1] +
f[1,1]g1[1,0]g2[0,1] + f[1,1]g1[0,1]g2[1,0]

where

f[1,0] is the coefficient of x1 in f(x1,x2) with x1=g1(z1,z2) and x2=g2(z1,z2)

f[0,1] is the coefficient of x2 in f(x1,x2) with x1=g1(z1,z2) and x2=g2(z1,z2)

g1[1,1] is the coefficient of z1z2 in g1(z1,z2)

g1[1,0] is the coefficient of z1 in g1(z1,z2)

g1[0,1] is the coefficient of z2 in g1(z1,z2)

g2[1,1] is the coefficient of z1 z2 in g2(z1,z2)

g2[1,0] is the coefficient of z1 in g2(z1,z2)

g2[0,1] is the coefficient of z2 in g1(z1,z2)
```
MFB( [1,1], 2 )
```
```
f[1,1]g1[0,1]g2[1,0] + f[1,1]g1[1,0]g2[0,1] + f[2,0]g1[0,1]g1[1,0] + f[1,0]g1[1,1] + f[0,2]g2[0,1]g2[1,0] + f[0,1]g2[1,1]
```
The coefficient of z1 in f[g1(z1,z2),g2(z1,z2),g3(z1,z2)]
```
MFB( [1,0], 3 )
```
```
f[0,1,0]g2[1,0] + f[1,0,0]g1[1,0] + f[0,0,1]g3[1,0]
```
The coefficient of z1 z2 in f[g1(z1,z2),g2(z1,z2),g3(z1,z2)]
```
MFB( [1,1], 3 )
```
```
f[0,1,1]g2[0,1]g3[1,0] + f[1,0,1]g1[0,1]g3[1,0] + f[1,1,0]g1[0,1]g2[1,0] + f[0,1,1]g2[1,0]g3[0,1] + f[1,0,1]g1[1,0]g3[0,1] + f[1,1,0]g1[1,0]g2[0,1] + f[0,2,0]g2[0,1]g2[1,0] + f[0,1,0]g2[1,1] + f[2,0,0]g1[0,1]g1[1,0] + f[1,0,0]g1[1,1] + f[0,0,2]g3[0,1]g3[1,0] + f[0,0,1]g3[1,1]
```
The coefficient of z1^2 z2 in f[g1(z1,z2),g2(z1,z2)]
```
MFB( [2,1], 2 )
```
```
f[1,2]g1[0,1]g2[1,0]^2 + f[1,1]g1[0,1]g2[2,0] + f[2,1]g1[1,0]^2g2[0,1] + f[1,1]g1[2,0]g2[0,1] + 2f[1,2]g1[1,0]g2[0,1]g2[1,0] + 2f[1,1]g1[1,0]g2[1,1] + 2f[2,1]g1[0,1]g1[1,0]g2[1,0] + 2f[1,1]g1[1,1]g2[1,0] + f[3,0]g1[0,1]g1[1,0]^2 + f[2,0]g1[0,1]g1[2,0] + 2f[2,0]g1[1,0]g1[1,1] + f[1,0]g1[2,1] + f[0,3]g2[0,1]g2[1,0]^2 + f[0,2]g2[0,1]g2[2,0] + 2f[0,2]g2[1,0]g2[1,1] + f[0,1]g2[2,1]
```
The coefficient of z1^2 z2 in f[g1(z1,z2),g2(z1,z2),g3(z1,z2)]
```
MFB( [2,1], 3 )
```
```
Not displayed for readibility reasons
```
The coefficient of z1 z2 z3 in f[g1(z1,z2,z3),g2(z1,z2,z3),g3(z1,z2,z3)]
```
MFB( [1,1,1], 3 )
```

#### Description
#### Usage
#### Argument
#### Value
#### Warnings
#### Examples








