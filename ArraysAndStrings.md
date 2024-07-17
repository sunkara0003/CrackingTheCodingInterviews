# Arrays and Strings

# Palindrome Permutation 
- Given a String with even or odd length we need to check its permuation is a palidrome.
  - Solution 1: TC=O(N) SC=O(N)
     - Count the characters store in hashtable
     - if it is odd length string then only one character with odd count should exists.
     - if it is an even length string then all characters should be even count
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
















