# GENERATORS IN PYTHON

## What are Python Generators?
A generator is a function which can stop the code execution at any arbitrary point in its function body, can return a value back to the caller and later resume the code execution from the point it was stopped earlier.

<i>Note: Any function which has atleast one `yield` keyword becomes a generator.</i>

## What is yield keyword in python?
It is used to return from the function without destroying the state of local variable. However, a `return` keyword, returns the value and stops the further execution of the function body. 

## Why to use generators in python?
1. <b>Easy to implement</b> compared to making a iterator from scratch.
2. <b>Memory efficient</b> as generator doesn't create a sequence in memory all at once, instead it produced one output at a time.
3. <b>Infinite Sequence</b> can not be stored in memory all at once, that's where generators come into the picture.

### Generator as a function
Fetching the values of generator by treating it as a iterable function.

```
def your_generator():
	print('execution of first part')
	yield 1
	print('execution of second part')
	yield 2

#Now iterate it
for i in your_generator():
    print(i,", ")
```

Output - 
```
execution of first part
1 , 
execution of second part
2 , 
```

Explanation:
1. We implement a loop in this generator function which is iterable.
2. In the first iteration everything will run until the first yield keyword comes up. (yeild 1 in our case.)
3. Everything will be executed before yeild 1 and 1 will be returned. 
4. In the second iteration of the loop, the code execution continues from where it stopped i.e. exactly below yeild 1.
5. After returing yield 2, the iteration stops.

### Generator as an object
Generator function returns generator object. We can call next() function to iterate over it.

```
def your_generator():
	print('execution of first part')
	yield 1
	print('execution of second part')
	yield 2
	
gen_obj = your_generator()
print(gen_obj) 

#Calling next method on generator object
print(next(gen_obj))
print(next(gen_obj))
print(next(gen_obj))
```

Output -
```
<generator object your_generator at 0x7efc1238b580>
execution of first part
1
execution of second part
2
Traceback (most recent call last):
  File "<string>", line 16, in <module>
StopIteration
```

Explanation:
1. You can see, the return value of generator function is a generator object.
2. Now, we can call next() function and pass this object as argument to get the first yeild.
3. If there are no yield statements left, the iteration is stopped, in the upcoming next() call.

<i>NOTE: In earlier version of python next was called like `gen_obj.next()`. But, it has been throwing error in python3. So, we will use `next(gen_obj)` instead.</i>
