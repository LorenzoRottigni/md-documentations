# Machine Learning Udemy Bootcamp 01 - Python basics

## String format
```
x = 'hello'
y = 'world'

print('{} is {}'.format(x, y))
print('{a} is {b}'.format(a=x, b=y))
# Python3
print(f'{x} is {b}')
```

## Slice notation
```
x = 'abdefghijk'

# takes everything after index 0
print(s[0:]) => abdefghijk
# takes everything before index 3
print(s[3:]) => abc
# take range 0 to 3
print[s[0:3]] => abc
print(s[3:6]) => def
```

## Lists
```
list = ['a', 'b', 'c']
list.append('d')
list[0] => 'a'
list[1:3] => ['b', 'c']
```

## Dictionaries
```
d = { 'key1': 'value', 'key2': [1,2,3] }
d['key1'] => 'value'
d['key1'][1] => 2
```

## Tuples
```
t = (1,2,3)
t[0] => 1
```
!! isn't possible to reassign tuples

## Sets
Collection of unique elements
set([1,1,1,1,1,2,2,2,2,6,6,6,6]) => {1, 2, 6}

s = {1, 2, 3}
s.add(5) => {1, 2, 3, 5}

## Utilities

### range
```
r = range(0, 5)
# by default starts from 0
r2 = range(10)

list(r) => [0, 1, 2, 3, 4]
list(r2) => [0, 1, 2, 4, 5, 6, 7, 8, 9]

for i in r:
  print(i)
```

### map
```
# normal function
def doublize(n): return n * 2
# callback function
t = lambda n: n * 2
seq = [1,2,3,4,5]
list(map(t, seq))
```

### filter
```
# filter odd numbers
list(filter(lambda n: n%2, seq))
```

### Short-hands
#### List for-loop generation
```
out = []

for num in x:
  out.append(num**2)

# is writable as
out = [num**2 for num in x]
```
