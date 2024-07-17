# Arrays and Strings

# Rotate Matrix 90 degreess
- Rotate the matrix by 90 degress clock-wise
- For a 90∘90∘ clockwise rotation, the element at position (i,j)(i,j) in the original matrix will move to position (j,N−1−i)(j,N−1−i) in the rotated matrix, where N is the size of the matrix.
- Given a matrix element at (i,j)(i,j), the swaps can be broken down as follows:
- TC = O(N^2)
```py
Top: (i,j)(i,j)
Right: (j,N−1−i)(j,N−1−i)
Bottom: (N−1−i,N−1−j)(N−1−i,N−1−j)
Left: (N−1−j,i)(N−1−j,i)

    Save the top element (initial element at (i, j)):
        temp = A[i][j]
    Move left element to top:
        A[i][j] = A[N - 1 - j][i]
    Move bottom element to left:
        A[N - 1 - j][i] = A[N - 1 - i][N - 1 - j]
    Move right element to bottom:
        A[N - 1 - i][N - 1 - j] = A[j][N - 1 - i]
    Move saved top element to right:
        A[j][N - 1 - i] = temp
```
```py
def rotateMatrix(matrix):
  if len(matrix)==0 or len(matrix)!=len(matrix[0]):
    return "Not Square Matrix"
  N = len(matrix[0])
  for i in range(N//2):
    for j in range(i,N-i-1):
        #top
        top = matrix[i][j]
        #left
        matrix[i][j] = matrix[N-1-j][i]
        #bottom
        matrix[N-1-j][i] = matrix[N-1-i][N-1-j]
        #right
        matrix[N-1-i][N-1-j] = matrix[j][N-1-i]
        #top
        matrix[j][N-1-i] = top
  return matrix

def printMatrix(A):
    N = len(A[0])
    for i in range(N):
        print(A[i])

matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]]
printMatrix(matrix)
print()
matrix = rotateMatrix(matrix)
printMatrix(matrix)
```


# String Compression
- Compressing the string aaabbbcc to a3b3c2

```py
def strCompression(test):
  countConsecutives = 0
  N = len(test)
  compressed_str = ""
  for i in range(N):
    countConsecutives+=1
    if i+1>=N or test[i+1]!=test[i]:
      compressed_str += test[i]+str(countConsecutives)
      countConsecutives=0
  return test if len(compressed_str)<N else compressed_str

test = "aabbcc"
print(strCompression(test))
      

```


# OneWay Edit
- Operation on a given string can be delete/replace/add characters to the given string to make the match with other string.


```py

def OneWayEdit(s,t):
  Ns = len(s)
  Nt = len(t)
  if Ns == Nt+1:
    print("delete")
    if deleteS(s, t, Ns, Nt)==1:
      return True
    else:
      return False
  elif Ns== Nt-1:
    print("insert")
    if insert(s, t, Ns, Nt)==0:
      return True
    else:
      return False
  elif Ns==Nt:
    print("replace")
    if replace(s, t, Ns, Nt)==1:
      return True
    else:
      return False
def insert(s, t, Ns, Nt):
  counter = 0
  for i in range(Ns):
    if s[i]==t[i]:
      counter=0
    else:
      return 1

def replace(s,t,Ns,Nt):
  counter = 0
  for i in range(Ns):
    if s[i]==t[i]:
      counter=0
    else:
      return 1
def deleteS(s, t, Ns, Nt):
  counter = 0
  for i in range(Ns-1):
    if s[i]==t[i]:
      counter = 0
    else:
      counter=1
  if s[Ns-1]!=t[Nt-1]:
      counter+=1
  return counter
 
s = "pales"
t = "ples"
s = "pale"
t = "pale"
s = "pale"
t = "bale"
print(OneWayEdit(s,t))

```

# Palindrome Permutation 
- Given a String with even or odd length we need to check its permuation is a palidrome.
  - Solution 1: TC=O(N) SC=O(N)
     - Count the characters store in hashtable
     - if it is odd length string then only one character with odd count should exists.
     - if it is an even length string then all characters should be even count
  - Solution 2: use the odd character count tradeoff with even char count finally oddcount<=1 return
  - Solution 3:
     - Here we dont need to return the no of odd character count taking 2nd solution as reference.
     - we just toggle the bits that are not overrapping. If they do so then N&(N-1)==0 means not overlapping
     - If there is an overlapping then N&(N-1)!=0 the toggle the mask and & with bitvector.
     - Here bitvector is an integer of 8bit size.
  
```py
def getCharNumber(ch):
    if ch>='a' and ch<='z' or ch>='A' and ch<='Z':
      ch = ch.lower()
      return ord(ch) - ord('a')
    return -1
def isPalindromCheck(hashtable):
  odd_counter = 0
  even_counter = 0
  for k,v in hashtable.items():
    if v%2==0:
      even_counter+=v
    else:
      odd_counter+=v
  total_length = odd_counter+even_counter
  if total_length%2==0 and even_counter%2==0:
    return True
  elif total_length%2==1 and odd_counter%2==1 and even_counter%2==0:
    return True
  else:
    return False
def isPalimdromePermutation(test):
  hashtable = dict()
  for ch in test:
    if getCharNumber(ch)!=-1:
      ch = ch.lower()
      hashtable[ch]=hashtable.get(ch,0)+1
  print(hashtable)
  if isPalindromCheck(hashtable):
    return True
  return False
test = "Tact Coa"
test = "taco cat"
print(isPalimdromePermutation(test))
# return true
```

```py
#Optimized checking the max one odd  count char
# EVEN + EVEN = EVEN
# ODD + EVEN = ODD
# here to form a permutation we can allow only one odd count char.
def getCharNumber(ch):
    if ch>='a' and ch<='z' or ch>='A' and ch<='Z':
      ch = ch.lower()
      return ord(ch) - ord('a')
    return -1
def isPalindromCheck(hashtable):
  oddflag = False
  for k,v in hashtable.items():
    if v%2==1:
      if oddflag==True:
        return False
      oddflag=True
  return True
def isPalimdromePermutation(test):
  hashtable = dict()
  for ch in test:
    if getCharNumber(ch)!=-1:
      ch = ch.lower()
      hashtable[ch]=hashtable.get(ch,0)+1
  print(hashtable)
  if isPalindromCheck(hashtable):
    return True
  return False
test = "Tact Coa"
test = "aabbb"
print(isPalimdromePermutation(test))
```

```py
# More optimized removing extra isPalindromCheck for max one odd character count
# we are doing tradeoff on OddCount value to stabilize with even count and make it <=1
def getCharNumber(ch):
    if ch>='a' and ch<='z':
      return ord(ch) - ord('a')
    return -1
def isPalimdromePermutation(test):
  hashtable = dict()
  odd_counter = 0
  even_counter = 0
  for ch in test:
    ch = ch.lower()
    if getCharNumber(ch)!=-1:
      hashtable[ch]=hashtable.get(ch,0)+1
      if hashtable[ch]%2==1:
        odd_counter+=1
      else:
        odd_counter-=1
  print(hashtable)
  return odd_counter<=1

test = "Tact Coa"
test = "aabbb"
print(isPalimdromePermutation(test))
```
```py
# it more brain eating solution. Working with bits and toggling the bits which are not overlapping.
def isPalindrom(test):
  bitVector = createBitVector(test)
  print(bitVector==0)
  result = bitVector&(bitVector-1)
  if(bitVector==0 or result==0)==True:
    return True
  else:
    return False

def createBitVector(test):
  bitVector = 0
  for ch in test:
    if ch==" ":
      continue
    ch = ch.lower()
    val_index = ord(ch) - ord('a')
    bitVector = toggle(bitVector, val_index)
  return bitVector

def toggle(bitVector, index):
  if index<0:
    return bitVector # no need of operations
  mask = 1<<index
  if bitVector&(mask)==0:
    bitVector = bitVector|mask
  else:
    bitVector = ~mask & bitVector

  return bitVector

test = "Tact Coa"
test = "aabbb"
print(isPalindrom(test))
```





# is Urlify
- Description: Implement an algorithm to determine if a string has all unique characters. What if there is no additional datastructures?
- Solution:
  - Confirm the string is a set of ASCII chars or UniCodes
  - Solution 01: In case of ascii code the take an array of 128 size to store for each character at index i in array for character at index i.
  - Solution 02: implementation using the bit magic.By taking a bitVector integer with 8bit size checking placing the set bits if they are repeats.

```py
def IsUrilify(test):
  hashtable = [0]*128
  for i in range(len(test)):
    value = ord(test[i])-ord('a')
    if(hashtable[value]==1):
      return False
    hashtable[value]=1
  return True

test = "aba"
print(IsUrilify(test))
```

```py
# O(N) TC
# O(c) SC
def IsUrilify(test):
  bitVector = 0
  result = 0
  value = 0
  for i in range(len(test)):
    value = ord(test[i]) - ord('a')
    result = bitVector & (1<<value)
    if(result > 0):
      return False
    bitVector = bitVector| (1<<value)
  return True
test = "aba"
print(IsUrilify(test))
```

```py
# O(N^2) TC
def IsUrilify(test):
  for i in range(len(test)-1):
    for j in range(i+1,len(test)):
      if test[i]==test[j]:
        return False
  return True
test = "aba"
print(IsUrilify(test))
```
```py
# O(N) + O(NlogN) TC
# linearly checking neighbours if they are same then return True
test = "".join(sorted(test))
```
# Checking Permutation of two strings
- We have multiple solutions
    1. Sort the two strings and compare linearly before this the length should be same for both strings.
    2. Checking the two strings have identical characters count before this the length should be same for both strings.
```py
# solution 1
def permutation(s, t):
  if len(s)!=len(t):
    return False
  new_s = "".join(sorted(s))
  new_t = "".join(sorted(t))
  for i in range(len(new_s)):
    if new_s[i]!=new_t[i]:
      return False
  return True
  
test1 = "aba"
test2 = "baa"
print(permutation(test1,test2))
```

```py
# Solution 2
def permutation(s, t):
  if len(s)!=len(t):
    return False
  counter = [0]*128
  for i in range(len(s)):
    value = ord(s[i]) - ord('a')
    counter[value]+=1
  for j in range(len(t)):
    value = ord(t[j]) - ord('a')
    if counter[value]<=0:
      return False
    else:
      counter[value]-=1
  return True
```

# Urilify
- Replace space with %20 in the string
  - Count spaces and make the newstring index= 2*spaces + truelength. Assume the string has enough spaces at the end
  - replace the space with the %20 chars and actual if not space char from backward traversing.
  - TC = O(N)
  - SC = O(N)

```py
def Urilify(tests, truelength):
  count_spaces = 0
  test = list(tests)
  for i in range(truelength):
    if test[i]==" ":
      count_spaces+=1
  index = count_spaces*2 + truelength
  if(truelength<len(tests)):
    test[truelength-1]="\0"
  for i in range(truelength-1,-1,-1):
    if test[i]==" ":
      test[index-1]="%"
      test[index-2]="0"
      test[index-3]="2"
      index-=3
    else:
      test[index-1]=test[i]
      index-=1
  return "".join(test)

tests = "Mr John Smith    "
print(Urilify(tests,13))
# output: Mr20%John20%Smit
```
















