---
layout:     post
title:      "Python Tutorial"
category:   Python
tags:       Python
---
* content
{:toc}

Python Tutorial

Python is a very simple language, and has a very straightforward syntax. Python uses indentation for blocks, instead of curly braces. Both tabs and spaces are supported, but the standard indentation requires standard Python code to use four spaces.

## Basic Syntax

```python
# multiple lines, use \ 
total = item_one + \
		item_two 
# if the sentence includes {}, (), [], don't need the \		
days = ['Monday', 'Tuesday', 'Wednesday',
        'Thursday', 'Friday']
```
## Python Quotation, '', "", """ (means multiple lines words)
```python
word = 'word'
sentence = "This is a sentence."
paragraph = """This is a paragraph.
With multiple lines"""
```
## Comments
```python
# this is a comment
'''
There are multiple comments 
here
'''
"""
Multiple comments
"""
```
## Python Variables. 

You do not need to declare variables before using them, or declare their type. 
```python
# numbers
var1 = 10
myfloat = 1.0
# string, using "" is easy to include '
mystring = 'hello'
mystring = "hello"
mystring = "Don't worry about apostrophes"
mystring = mystring + " " + mystring
# muitlple assignments
a, b = 3, 4
# we will go to details about each variable
```

## Operator
```python
# Arithmetic Operator
a = 21
b = 10
c = a + b
c = a - b
c = a * b
c = a / b
c = a % b
c = a ** b   # power(a, b)
c = a // b   # get the int part

# Comparation Operator
# <  >  ==  !=  >=  <=

# Assignment Operator
# =  +=  -=  *=  /=  %=  **=  //=
# Bit operator
a = 0011 1100
b = 0000 1101
-----------------
a&b = 0000 1100
a|b = 0011 1101
a^b = 0011 0001
~a  = 1100 0011

# Logic Operator
# and or not 

# Member Operator
a = 1
list = [1, 2, 3, 4, 5]
if ( a in list)
	print ("a is in the list")

# Identity Operator
a = 20
b = 20
if ( a is b )
	print ("a and b have the same identity.")
```

## Condition
The "and" and "or" , "yes", "not" boolean operators allow building complex boolean expressions. 
The "in" operator could be used to check if a specified object exists within an iterable object container.
```python
num = 5
if num == 3:
	print ('shan')
elif num == 2:
	print ('cici')
else:
	print ('error')

if num < 0 or num > 10:
	print ('yeah')

if num in [1, 3, 4]
	print ('yes')	
```
## Loop
```python
count = 3
while ( count >0 ):
	print ('The count is ', count)
	count -= 1

# while .. else, when while loop finished, go to the else sentence
while count < 5:
	print (count, " is  less than 5")
	count = count + 1
else:
	print (count, " is not less than 5")	

# For
for letter in 'Python':     
	print ('Current Letter is :', letter)

# for .. else
for letter in 'Python':     
	print ('Current Letter is :', letter)
else:
	print ('It is the end')

# break and continue
count = 0
while True:
    print count
    count += 1
    if count >= 5:
        break

for x in xrange(10):
    # Check if x is even
    if x % 2 == 0:
        continue
    print x
```
* Pass: pass in python is a blank sentence, does not do anything
## Number
```python
var = 1
del var
str(x)	# transfer x to string
eval(str)	# calculate the valid expression in the string str
tuple(s)	#transfer x to tuple
list(s)		#transfer x to list
chr(s)		#transfer x to char
unichr(s)	#transfer x to unicode
hex(x)
oct(x)
# math function in python
abs(x)
ceil(x)		# ceil(4.1) return 5
floor(x)	# floor(4.1)	return 4
exp(x)
cmp(x, y)	# compare x and y
log(x)
max(x1, x2)
min(x1, x2)
power(x, y)
round(x, [, n])
sqrt(x)
```
## String
```python
var = 'hello world'
print (var[1])
print (var[1:4])

a = "hello"
b = "python"
a + b
a * 2 # copy
a[2]
a[1:4]
"h" in a # Return True

print "My name is %s and weight is %d kg!" % ('Zara', 21) 

# string functions
str.capitalize()	# Capitalize the first letter
str.count(s, begin=0, end=len(str))	# return how many times s occur in str
str.find(s, beg=0, end=len(str))
str.index(s, beg=0, end=len(str))
str.isalnum()
str.isalpha()
str.isdigit()
str.islower()
str.isspace()
max(str)	
min(str)
str.lstrip()	# delete the spaces in the left of str
str.rstrip()	# delete the spaces in the right of str
str.replace(str1, str2, num==str.count(str1))
string.split(str="", num=string.count(str))
```
## List
```python
list1 = ['physics', 'chemistry', 1997, 2000];
list2 = [1, 2, 3, 4, 5, 6, 7 ];
print "list1[0]: ", list1[-2]
print "list2[1:5]: ", list2[1:5]
```
* List Operations
```python
# update:
list1[2] = 2000
# delete:
del list1[2]
# length:
len([1, 2, 3])
# append
[1, 2, 3] + [4, 5, 6]
# copy
['Hi']*4
for x in [1, 2, 3]: 
	print x
```

* List Functions
```python
cmp(list1, list2)
list.append(obj)
list.count(obj)
list.index(obj)
list.insert(index, obj)
list.pop()#delete the last one
list.remove(obj) #remove the first object matched
list.reverse()
list.sort(func)
```
## Tuple

the only difference with list is that the elements can not be modified
```python
tup1 = ('physics', 'chemistry', 1997, 2000)
when the number of the tuple is only one, you need add ,
tup1 = (50,)
# tuple operations
print "tup2[1:5]: ", tup2[1:5]
# append two tuples
tup1 = (12, 34.56)
tup2 = ('abc', 'xyz')
tup3 = tup1 + tup2
# delete the whole tuple
del tup
len(tup)
('Hi')*4
3 in (1, 2, 3)
```
## Dictionary

```python
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
print "dict['Name']: ", dict['Name'];
# update, delete, same as the list operations
print "dict['Name']: ", dict['Name']
```

## Date and Time
```python
# import time;
ticks = time.time()
localtime = time.localtime(time.time())
print "本地时间为 :", localtime
# default time
localtime = time.asctime( time.localtime(time.time()) )
time.strftime(format[, t])
# 2016-03-20 11:45:39 format
print time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) 
# Sat Mar 28 22:24:24 2016 format
print time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) 
a = "Sat Mar 28 22:24:24 2016"
print time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y"))
# calinder
Get the calinder
import calendar
cal = calendar.month(2016, 1)
print cal;
```

## Input and Output
```python
print 'hello, world'
print '100+200 = ', 100+200
str = raw_input("Inuput:")
fo = open("foo.txt", "wb")
print "File name: ", fo.name
print "If closed : ", fo.closed
print "Mode : ", fo.mode
print "If add the space in the end : ", fo.softspace
fo.write( "www.runoob.com!\nVery good site!\n");
```

## Functions: all parameters are all references
```python
def printme( str ):
   "Print all the strings"
   print str;
   return;

printme("I am calling the function!");
```