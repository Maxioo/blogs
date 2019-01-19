# The exercise of introduction to algorithms

## Chapter 1: Foundation

### 1.1 Algorithms

#### 1.1-1

- Sorting in real world : republish like dictionaries  
- Convex hull in real world : In the road,if some car crash together,we should find some way to surrender them.

#### 1.1-2

- The other efficient in real world other than speed:
- The time you spend per yuan(money), the efficiency.

#### 1.1-3

Array:

- Strengeh you can place the data in order,and can select and look easily.  
- Limitation if you want insert one,you may move a bunch of latter item.

#### 1.1-4

- Similar in the two problem,you must find the smallest cost.
- Differant in the t-s problem,the line of two adjacent dot have weight,and we must to consider.

#### 1.1-5

- Caculater the average
- The best way: sum up the all item,and divided.
- Approximately: select some of it,and sum up,then divided;

### 1.2 Algorithms as a technology

#### 1.2-1

- If we want diliver some advertising to customer,so we must well designed algorithm to met demand.  
- We can use deep learning or mechine learning to accomplish it.

#### 1.2-2

We let 8n equal 64 lgn ,solute it. the n equal 44.

#### 1.2-3

Same as 1.2-2 , the smallest n is 15.

------------------------------------------------------

## Chapter 2: Getting Started

### 2.1 Insertion sort

#### 2.1-1

> A = {31, 41, 59, 26, 41, 58}. illustrate the operation of INSERTION-SORT.
- Step1 Check if 31<41,the answer is true,so left as it is.
- Step2 same as step1,left as it is.
- Step3 Let 59 in position 3,41 in position 2,31 in position 1,26 in position 0.
- Step4 Let 59 in position 4,41 in position 3.
- Step5 Let 59 in position 5,58 in position 4.Down.

#### 2.1-2

> Rewrite the INSERTION-SORT to sort into nonincreasing order.

##### INSERTION-SORT(nonincresing)

    for j = 2 to A.length
        key = A[j]
        i = j - 1
        while i > 0 and A[i] < key
            A[i+1] = A[i]
            i = i - 1
        A[i+1] = key

#### 2.1-3

##### Liner-searching

    for i = 1 to A.length
        if A[i] == v
            return i
    return NIL

- **Initialization**  We start by showing that the loop invariant holds before the first loop iteration. if A[1]==v, so it will return 1, or return NIL, whitch shows that the loop invariant holds.
- **Maintenance** In each iteration,we can find that if the current A[i] equal v, it will return i, or return NIL, that loop invariant holds.
- **Termination** The condition causing the for loop to terminate is that i>A.length=n, when it terminate, it shows that we can't find the value, so it will return NIL. Hence, the algorithm is correct.

#### 2.1-4

> Adding two n-bit binary integers.

- **Input** Two sequence of n numbers A=<a1,a2,...,an> and B=<b1,b2,...,bn>
- **Output** Adding two sequence bianry integers to a sequence of C=<c1,c2,c3,...,c(n+1)>, and output the C.

##### Adding integers

    temp = 0
    for i = 0 to A.length
        c1 = (a1 + b1 + temp) % 2
        temp = (a1 + b1 + temp) / 2
    c(n+1) = (an + bn + temp) % 2
    return C

### 2.2 Analyzing algorithms

#### 2.2-1

O(n^3)

#### 2.2-2

    for i = 0 to A.length - 1
    temp = i
        for j = i to A.length
            if A[temp] > A[j]
                i = j
    exchange A[i] and A[temp]

- **Initialization**  when we start,there is only one element,because single element is always sorted.
- **Maintenance** In each iteration,we choose the smallest element,and we exchange it with the current one,so the maintenance holds.
- **Termination** The condition causing the for loop to terminate is that i>A.length=n, when it terminate,all the elements are sorted,so the loop invariant holds.

When the first n-1 elements sorted,the rest one is the biggest one in the array,so we do not have to care about it.

Best-run time: even the array are already sorted, we still have to compare all the elements,so the runtime is O(n^2)

Worest-runtime: same as Best-run time is O(n^2)

#### 2.2-3

On average,n/2 elements need to be checked on the average.

Worst-case: n elements need to be cheked.

average-case and worst-case running times of linear search are O(n)

#### 2.2-4

We just put a check statement to check whether the input is already maintain all the requirement.

### 2.3 Designing algorithms

#### 2.3-1

The first level: 3 9 26 38 41 49 52 57
The second level: 3 26 41 52 || 9 38 49 57
The third level: 3 41 || 26 52 || 38 57 || 9 49
The forth level: 3 || 41 || 52 || 26 || 38 || 57 || 9 || 49

#### 2.3-2

    Merge(A,p,q,r)
    n1 = q-p-1
    n2 = r-q
    let L[1..n1] and R[1..n2] be new arrays
    for i = 1 to n1
        L[i] = A[p+i-1]
    for j = 1 to n2
        R[j] = A[q+j]
    if n1 > n2
        min = n2
    else
        min = n1
    i1 = 1
    i2 = 1
    for i = 1 to min
        if L[i1] < R[i2]
            A[p+i-1] = L[i1]
            i1++
        else
            A[p+i-1] = R[i2]
            i2++
    if i1 = n1
        for j = i2 to n2
            A[p+j-1] = R[i2]
            i2++
    else
        for j = i1 to n1
            A[p+j-1] = L[i1]
            i1++

#### 2.3-3

When n is an exact power of 2.
First: When n equal 2,T(2) = 2 = 2*lg2 = 2,so the prove to be established.
Second: We suppose T(n/2) = 2T(n/4) + n/2 = (n/2)lg(n/2) establish.
Final: T(n) = 2T(n/2) + n = (n/2)lg(n/2) + n = nlgn
so this equation establishment.

#### 2.3-4

T(n) = O(1)                 if n = 1
       T(n-1) + an + b      if n > 1

#### 2.3-5

    Search_iterative(A,p,r,d)
    flag = 0
    while p != r
        mid = (p + r)/2
        if A[mid] < d
            p = mid
        else if A[mid] > d
            r = mid
        else
            return mid
    if A[p] != d
        return 0

Fistly,we assume that n is an exact power of 2.each time of iteration we cut half of number.
The worst time is when there is only one number,whatever it is the number we want,we cut
lgn times,and every cut operation consume constant time.
so the worst-case time running time of binary search is O(lgn).

#### 2.3-6

Yes,we can

#### 2.3-7

    twoNumSum(S,x)
    Sort S
    for i = 1 to S.length()
        temp = x/S[i]
        if Search_iterative(temp) == 0
            continue
        else
            return true
    return false

### Problems

#### 2-1

Problem a:When we want use insertion sort to sort n/k sublists.
so the worest time is O(n/k * k *k) = O(nk)

Problem b:We cut the sublists into two sublists,and we merge the left and right sublists.
we merge two sublist into one sublist,the worst-case time is O(k+k),
the first layer we need O(n),and there is lg(n/k) layer

Problem c:The biggest num is lgn

Problem d:we can count the running time when we choose k from 1 to lgn.
and deside the best one.

#### 2-2

Problem a:We need prove that A' consists of the original elements in A,although in different order.

Problem b and c:We need Initialization ,Manintnance and Termination.

 **Initialization** First,when i equal 1,so from A.length to 2,we choose the smallest one to sit in A[1].
 So the A[1] <= A[2]

 **Maintenance** When A[1] <= A[2] <= ... <= A[c-1] ,When i equal c-1, we continue choose the smallest one,
 and A[c-1] <=  A[c]

 **Termination** When i equal A.length -1 ,we find A[A.length-1] <= A[A.length],so A[1] <= A[2] <= ... <= A[n]

Problem d: The worst-cast running time is O(n^2),and the bubblesort will show slower than insertion sort,because bubblesort apply assignment more than insertion sort.

#### 2-3

Problem a: O(n)

Problem b: 

    y = 0
    for i = 0 to n
        temp = 1
        for j = 0 to i
            temp *= x
        y += ai*temp

This running-time is O(n^2) ,it slower than Horner's rule.

Problem c:

 **Initialization** First,y = 0,so with no terms as equaling 0.

 **Maintenance** y = a(i+1)+a(i+2)*x+...+an*x^(n-i-1),when i = n, y = an,and when i subtract 1,all elements will plus x,and add ai,so the loop invariant holds.
 at the end of iteration of i.we get y = (n-i)sum(k=0)a(k+i)x^k.

 **Termination** When the loop end ,i equal 1 so at the termination y = nsum(k=0)akx^k.

Problem d: It should be fairly obvious.

#### 2-4

Problem a:{1,5} {2,5} {3,4} {3,5} {4,5}

Problem b:The reversive list {n,n-1,...,1},
it equal n + n-1 + ... + 1 = n(n-1)/2

Problem c:When we at the ith iteration,we know the A'[1..i] are sorted,and all the element are come from the original A[1..i],so if A[i+1] and former i elements have m inversions,we need to push the sublist m times.so the running time of insertion sort is O(n+m).

Problem d:

  MERGE-SORT(A, p, r):
  if p < r
      inversions = 0
      q = (p + r) / 2
      inversions += merge_sort(A, p, q)
      inversions += merge_sort(A, q + 1, r)
      inversions += merge(A, p, q, r)
      return inversions
  else
      return 0

MERGE(A, p, q, r)
  n1 = q - p + 1
  n2 = r - q
  let L[1..n₁] and R[1..n₂] be new arrays
  for i = 1 to n₁
      L[i] = A[p + i - 1]
  for j = 1 to n₂
      R[j] = A[q + j]
  i = 1
  j = 1
  for k = p to r
      if i > n₁
          A[k] = R[j]
          j = j + 1
      else if j > n₂
          A[k] = L[i]
          i = i + 1
      else if L[i] ≤ R[j]
          A[k] = L[i]
          i = i + 1
      else
          A[k] = R[j]
          j = j + 1
          inversions += n₁ - i
  return inversions

### 3.1 Asymptotic notation

#### 3.1-1

Because f(n) and g(n) be asymptotically nonnegative.when n > 1,we let c1 = 0.5 and c2 = 2
so c1(f(n)+g(n)) < max(f(n),g(n)) < c2(f(n)+g(n))
so it proved.

#### 3.1-2

We can let the c1 = 1,and c2 = 2^b and when n > a,we know n^b < (n+a)^b < (2n)^b

#### 3.1-3

Because O(n^2) is a upper bound,but at least represent a lower bound.

#### 3.1-4

First 2^(n+1) equal 2*2^n,obviously 2^(n+1) equal O(2^n). Second 2^2n = 4^n if we let 4^n = c2 2^n,so c2 equal 2^n,2^2n not equal O(2^n).

#### 3.1-5

From f(n) = Θ(g(n)),so 0<=c1g(n)<=f(n)<=c2g(n),for n>n0
obviously the definitions of O and Ω to show taht both hold.

From f(n) = Ω(g(n)) and f(n) = O(g(n)):
0<=c3g(n)<=f(n) for all n>=n1  
0<=f(n)<=c4g(n) for all n>=n2 .we let n3 = max(n1,n2)  
0<=c3g(n)<=f(n)<=c4g(n) for all n>n3.Which is the definition of  Θ.

#### 3.1-6

If Tw is the worst-case running time and Tb is the best-case running time, we know that:

0≤c1g(n)≤Tb(n)for n>nb0≤Tw(n)≤c2g(n)for n>nw

Combining them we get:

0≤c1g(n)≤Tb(n)≤Tw(n)≤c2g(n)for n>max(nb,nw)

Since the running time is bound between Tb and Tw and the above is the definition of the Θ-notation, we have our proof.

#### 3.1-7

we suppose f(n) is a member of o(g(n)),h(n) is a member of w(g(n)),we can know,for all c1>0, 0<=f(n) < c1g(n).
0<=c1g(n) < h(n).
so f(n) < clg(n) < h(n),so we can know,there are no same items belong to o(n) and w(n).

#### 3.1-8

Ω(g(n,m)) = {f(n,m):there exist positive constants c,n0,and m0 such that 0<=cg(n,m)<=f(n,m) for all n>=n0 or m>=m0}  
O(g(n,m)) = {f(n,m):there exist positive constants c,n0,and m0 such that 0<=f(n,m)<=cg(n,m) for all n>=n0 or m>=m0}

### Standard notation and common functions

#### 3.2-1

if f(n) and g(n) are monotonically increasing,we let m <= n,so f(m)<=f(n),g(m)<=g(n).  
so f(m) + g(m) <= f(n) + g(n) ,and f(g(m)) <= f(g(n)),and if f(n) and g(n) are in addition nonnegative,then f(m)*g(m) <= f(n)*g(n).

#### 3.2-2

a^(logb c) = a^(loga b/loga b) so we can get c^(loga b)

#### 3.2-3

lg(n!) = 1/2lg(2pin) + nlg(n/e) + anlge

so lg(n!) = 0(nlgn)
n! = n*(n-1)*(n-2)*...*2*1 >= 2^n
n! = n*(n-1)*(n-2)*...*2*1 <= n^n

#### 3.3-4(not solved)

[lgn]! upper bound <= lgn^lgn so it is not polynomially bounded.and [lglgn]! is not polynomially bounded.
polylogarithmic functions grow slower than polynomial functions.

#### 3.3-5

lg*n = min{i>=0: lg^(i)n<=1}
suppose lg*n compare 2^lg*(lgn)
suppose lg*n equal t,so t compare 2^(t-1) when n become sufficent large,we know the right bigger than left

#### 3.3-6

we substituting the two number ,we know the equation holds.

#### 3.3-7

We can let F(i+2) = F(i+1) + Fi.so we put all thing in it.so the equation holds.

#### 3.3-8(not solved)

From the symmetry of Θ:

klnk=Θ(n)⇒n=Θ(klnk)

Lets find lnn:

lnn=Θ(ln(klnk))=Θ(lnk+lnlnk)=Θ(lnk)

Let's divide the two:

nlnn=Θ(klnk)Θ(lnk)=Θklnklnk=Θ(k)

### Problems 3

#### 3-1(not solved)

#### 3-2

a:yes ; yes ; no ; no ; no
b:yes ; yes ; no ; no ; no
c:no  ; no  ; no ; no ; no
d:no  ; no  ; yes; yes; no
e:yes ; no  ; yes; no ; yes
f:yes ; no  ; yes; no ; yes     (no solved)

#### 3-3

a:2^2^(n+1) ; 2^(2^n) ;  (n+1)! ; n! ; (lgn)! ; e^n ; n*2^n ; 2^n 4^lgn ; (lgn)^lgn n^lglgn ; (3/2)^n ; n^3 ; n^2 ; lg(n!)  nlgn; n 2^lgn ; (sqrt2)^lgn ; 2^(sqrt(2lgn)) ; lg^2n ; lnn ; sqrt(lgn) ; lnlnn ; 2^lg*n ; lg*n ; lg(lg*n) ; 1 n^(1/lgn)

b:2^sinx

#### 3-4

a: n = O(n^2) but n^2 not equal O(n).
b: f(n)+g(n) not equal O(min(f(n),g(n))).
c: if f(n) = O(g(n)),we can know there exist c > 0,n>n0,let 0<= f(n) <= cg(n),we can get lg(f(n)) <= lg(cg(n)) = lgc + lg(g(n)).
we must prove lg(f(n)) <= c1 lg(g(n))
so d = (lgc + lgg(n))/lg(g(n)) <= lgc+1 because lg(g(n)) >= 1.
d:because 2n = O(n),but 2^2n = 4^n not equal O(2^n)
e:incorrect : f(n) = 1/n
f:correct
g:incorrect : f(n) = 2^n
h:correct

#### 3-5

a: n = Omega-Infinity(n^nsinn) but n not equal Omega(n^nsin).
b: some times,when n become so large,it also come to leap more higher or smaller,but most of time it like Omega(g(n))
c:So we can only use Theta to indicate O',but we can not reverse.
d:Just like anwer,Soft-Omega like cg(n)*lg^-k n <= f(n)

#### 3-6

a: Θ(n)
b: Θ(lg*n)
c: Θ(lgn)
d: Θ(lgn)
e: Θ(lglgn)
f: can not converge
g: Θ(log3lgn)
h: ω(lglgn),o(lgn)  becasue n^(1/2) <= n/lgn <= n/2

### 4-1 The maximum-subarray problem

#### 4.1-1

It will return biggest negative number index and value.

#### 4.1-2

    FIND-MAX-SUBARRAY-BRUTE-FORCE(A)
    sumFin = -INF;
    sum = 0;
    maxi = 0;
    maxj = 0;
    for i = 1 to A.length
        for j = i to A.length
            sum += A[i];
            if sumFin < sum
                sumFin = sum;
                maxi = i;
                maxj = j;
    return (maxi,maxj,sum);

#### 4.1-3

when the input number larger than 660, the brute way will cost more time.And when we use brute way in smaller number in divide ways, the divide way will always quicker or equal than brute way.

#### 4.1-4

We need to modify the base case,when A[low] is negative,we return a empty array.
when the maxsum is negative ,we return a empty array.

#### 4.1-5

    FIND-MAX-SUBARRAY-LINER(A)
    sumE = -INF
    sum = 0
    maxl = 1
    maxr = 1
    for i = 1 to A.length
        sum += A[i]
        if sum < 0
            sum = 0
            tempi = i + 1
        if sumE < sum
            sumE = sum
            maxl = tempi
            maxr = i
    return (maxl,maxr,sumE) 
