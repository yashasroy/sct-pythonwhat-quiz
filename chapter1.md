---
title       : SCT quiz
description : Quiz time y'all
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


--- type:NormalExercise lang:python xp:100 skills:1 key:03eebf7448
## Simple tests (1)

#### pass 1

```python
import numpy

x = numpy.array([1,2,3])

print(x)
```

#### pass 2

```python
import numpy as npp

x = y = npp.array([1,2,3])

print(y)
```

#### fail 1 - "Did you import numpy?"

```python
import pandas as pd

x = pd.np.array([1,2,3])

print(x)
```

#### fail 2 - "Your value of x is incorrect"

```python
import numpy as np

x = [1,2,3]

print(x)
```

#### fail 3 - "x is undefined"

```python
import numpy as np
```

#### fail 4 - "Expected [1,2,3] in your output"

```python
import numpy

x = numpy.array([1,2,3])
```

*** =sample_code
```{python}
import numpy as np

x = np.array([1,2,3])

print(x)
```

*** =solution
```{python}
import numpy as np

x = np.array([1,2,3])

print(x)
```

*** =sct
```{python}

```

--- type:NormalExercise lang:python xp:100 skills:2 key:d71dfcb25c
## Simple tests (2)

#### pass 1

```
f("blue")
```

#### pass 2

```
 f( "b" )
```

#### pass 3

```
f('b')
```

#### pass 4
```
(f("b"))
```

#### fail 1 -

```
f("blueberry")
```

#### fail 2 -

```
pf("blue")
```

*** =pre_exercise_code
```{python}
def f(a): return a*2

def pf(a): return a*2

```

*** =sample_code
```{python}
f("b")
```

*** =solution
```{python}
f("b")
```

*** =sct
```{python}
# NOTE: use a single test_student_typed statement
#       see https://docs.python.org/3.5/library/re.html

```

--- type:NormalExercise lang:python xp:100 skills:2 key:746620aaa8
## Part Checks (1)

#### fail 1 - "No inline if expression"

```
if True: ["yes" for ii in range(3) if ii > 2]
elif False: pass
else: pass
```

#### fail 2 - "No if filter in list comp"

```
if True: ["yes" for ii in range(3)]
elif False: pass
else: pass
```

#### fail 3 - "No else statement"

```
if True: ["yes" for ii in range(3) if ii > 2]
elif False: pass
```

*** =sample_code
```{python}
if True: ["yes" if True else False for ii in range(3)]
```

*** =solution
```{python}
if True: ["yes" if True else False for ii in range(3)]
```

*** =sct
```{python}

```

--- type:NormalExercise lang:python xp:100 skills:2 key:23e667966f
## Part checks (2)

#### pass 1 -

```
with open('test.txt') as f:
    map(print, f)
```

#### pass 2 - 

```
with open('test.txt') as f:
    for ii in f.readlines(): print(ii)
```

#### fail 1 - "No with block"

```
f = open('test.txt')
for ii in f: print(ii)
```

#### fail 2 - "Incorrect output"

```
with open('test.txt') as f:
    for ii in f: print('no')
```

*** =pre_exercise_code
```{python}
open('test.txt', 'w').write('a\nb\nc\n')
```

*** =sample_code
```{python}
with open('test.txt') as f:
    for ii in f:
        print(ii)
```

*** =solution
```{python}
with open('test.txt') as f:
    for ii in f:
        print(ii)
```

*** =sct
```{python}
```

--- type:NormalExercise lang:python xp:100 skills:2 key:1b865f62b7
## Expression tests (1)

#### fail 1 - "wrong if test"

```
def callback():
    if select1.value == 'WRONGVAL':
        select2.value = 1
    else:
        select2.value = 2
```

#### fail 2 - "wrong select2 value in if"

```
def callback():
    if select1.value == 'a':
        select2.value = 'WRONGVAL'
    else:
        select2.value = 2
```

#### fail 3 - "wrong select2 value in else"

```
def callback():
    if select1.value == 'a':
        select2.value = 1
    else:
        select2.value = 'WRONGVAL'
```

#### fail 4 - "select2 unused in if"

```
def callback():
    if select1.value == 'a':
        pass
    else:
        select2.value = 'WRONGVAL'
```



*** =pre_exercise_code
```{python}
class Select:
    """Calls self.callback whenever self.value is set"""
    
    def __init__(self, value):
        self.callback = None
        self.value = value
        
    def on_change(cb):
        self.callback = cb
    
    @property
    def value(self): return self._value
    
    @value.setter
    def _(self, x):
        self._value = x
        if self.callback: self.callback()

```

*** =sample_code
```{python}
select1 = Select(value='a')
select2 = Select(value=0)

# ONLY MODIFY HERE
def callback():
    if ____ == ____:
        select2.value = ____
    else:
        select2.value = ____
#

select1.on_change(callback)
```

*** =solution
```{python}
select1 = Select(value='a')
select2 = Select(value=1)

# ONLY MODIFY HERE
def callback():
    if select1.value == 'a':
        select2.value = 1
    else:
        select2.value = 2
#

select1.on_change(callback)
```

*** =sct
```{python}
# DO NOT MODIFY
for name in ['select1', 'select2']:
    Ex().check_object(name).has_equal_value("%s unequal"%name)
# Put SCTs below here ----

```
