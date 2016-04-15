## CompSci Python 3 Class
* assignment means =
* data types
* function print and print()
* list
* dictionary
* control
* function definition
* function calling
* first program

### assignment means =
* number
    + state = 1
* boolean
    + human = True
* string
    + name = "Tom"
* list  ordered sequence of values
    + grades = [1,2,3,4,5,6,8,7]
* tuple immutable ordered sequence of values
    + planets = ("Mercury","Venus","Earth","Mars","Jupiter","Saturn","Uranus","Neptune")
* set  unordered bags of values
    + letters = {"s","h","e","l","a","h"}
* dictionary    unordered bags of key-value pairs
    + people = {"george":"washington", "barack":"obama"}

**common assignment errors:**

* "instrument" = "cello"   **BAD, variable names are letters only no quotes allowed, do this instead: instrument = "cello"**
* instrument = cello   **BAD, cello is not an existing value yet and cannot be assigned, do this instead: instrument = "cello"**
* instrument type = "cello"   **BAD, variable names are letters only, no spaces allowed, do this instead: instrumentType = "cello"**
* print = "Hello World"   **BAD, print is a variable name that is already in use, do this instead: print_variable = "hello world"**

### data types

* number
    + 1
    + 3.14159
    + -44
    + 0
    + 3/4 
* boolean 
    + True
    + False
* string
    + "good woman child"
    + "好女子"
* list
    + [1,2,3]
    + ["a","b","c"]
    + ["one", 2, True]
* tuple
    + ("alpha","omega")
* dictionary
    + {"a":1,"b":2}
    + {1:"a",2:"b"}
* set
    + {1,2,3}

### function print and print()

* print is a function
* print() is calling a function
```{python}
name="Tom"
print("hello world")
print(name)
```

### list
```{python}
grades = [1,2,3,4,5,6,8,7]
grades[0]
grades[1]
grades[7]
grades[7] = 8
grades[6] = 7
grades[7]
grades[1:3]
grades[:2]
grades[:2]
grades[2:]
len(grades)
grades.append(9)
len(grades)
# grades[9] = 10  **BAD no place at grades[9] to put value ~IndexError: list assignment index out of range~**
```
### dictionary
```{python}
people = {"george":"washington", "barack":"obama"}
people
people["ulysses"] = "grant" 
people["george"] = "bush"
#people["donald"]    **BAD, no such key in people dictionary ~KeyError: 'donald'~**
```
### control
* python code starts executing on the first line and continues line by line until last line and program ends
* control allows you to control program flow (skip lines, rerun lines)

* if, elif, else  (condition, colon, indentation)
```{python}
state=1
human=True
if(human==True):
    print("Hello")
else:
    print("Peace")
if(human==True):
    if(state==50):
         print("Howdy, you must be from Hawaii")
    elif(state==1):
         print("Hello, you must be from Delaware")
    else:
         print("Hello, are you Canadian?")
else:
    print("Peace")
```

* for 
```{python}
for planet in planets:
    print w, len(w)

grades = [1,2,3,4,5,6,8,7]
planets = ("Mercury","Venus","Earth","Mars","Jupiter","Saturn","Uranus","Neptune")
for item in range(len(grades)):
    print(grades[item])


people = {"george":"washington", "barack":"obama"}
for key in people.keys():
    print key, people[key]
```

* while
```{python}
i = 5
while(i>0):
    print i
    i=i-1    # what happens if we forget to decrement i?
print("blast off")
```
### function definition
```{python}
def fib(n):
     """Print a Fibonacci series up to n."""
     a, b = 0, 1
     while a < n:
         print a,
         a, b = b, a+b
```
### function calling
```{python}
fib(2000)
```

### first program
```{python}
SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],
            1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}

def approximate_size(size, a_kilobyte_is_1024_bytes=True):
    '''Convert a file size to human-readable form.

    Keyword arguments:
    size -- file size in bytes
    a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
                                if False, use multiples of 1000

    Returns: string

    '''
    if size < 0:
        raise ValueError('number must be non-negative')

    multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
    for suffix in SUFFIXES[multiple]:
        size /= multiple
        if size < multiple:
            return '{0:.1f} {1}'.format(size, suffix)

    raise ValueError('number too large')

if __name__ == '__main__':
    print(approximate_size(1000000000000, False))
    print(approximate_size(1000000000000))
```

