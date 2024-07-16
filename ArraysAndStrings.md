# Arrays and Strings
1. Problem: is Urlify
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

```psy
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







