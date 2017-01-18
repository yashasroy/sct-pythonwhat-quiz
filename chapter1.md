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


#### fail 2 - "x is not an ndarray"

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

Ex().test_import("numpy", same_as=False)

Ex().test_object('x', undefined_msg = 'x is undefined')

#Ex().test_output_contains("[1 2 3]", pattern = False, no_output_msg = "Expected [1,2,3] in your output")

Ex().test_function('numpy.array', not_called_msg = "x is not an ndarray")

Ex().test_function('print', not_called_msg = 'Expected [1,2,3] in your output')

```

--- type:NormalExercise lang:python xp:100 skills:2 key:d71dfcb25c
## Simple tests (2)

NOTE: Skipping due to time constraints

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

NOTE: I have a handle on this, but had to move on due to time

#### fail 1 - "No inline if expression"

```
if True: ["yes" for ii in range(3) if ii > 2]
elif False: pass
else: pass
```

#### fail 2 - "No if filter in list comp"

```
if True: ["yes" if True else False for ii in range(3)]
elif False: pass
else: pass
```


*** =sample_code
```{python}
if True: ["yes" if True else False for ii in range(3) if ii > 2]
elif False: pass
else: pass

```

*** =solution
```{python}
#if True: ["yes" if True else False for ii in range(3) if ii > 2]
#elif False: pass
#else: pass

["yes" if True else False for ii in range(3) if ii > 2]
```

*** =sct
```{python}
#first_if_test = Ex().check_if_else(0).check_test().check_body()

#list_comp = first_if_test.check_list_comp(0)

#list_comp = check_list_comp(0)

#list_comp.check_body().

#check_if_exp(0).has_equal_value()

#list_comp.check_iter().has_equal_value()

#list_comp.check_ifs(0).multi([has_equal_value(context_vals=[ii]) for ii in range(0,3)])




```

--- type:NormalExercise lang:python xp:100 skills:2 key:23e667966f
## Part checks (2)

NOTE: First example is failing because my SCT tests the for loop. Need to spend more time on this. Also, spec2 has 'incorrect_msg', but is there an option such as 'undefined_msg' or 'not_called_msg'?

#### pass 1 -

```
with open('test.txt') as f:
    print(f.read().replace('\n','\n\n'))
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
with_open = Ex().check_with(0).check_context(0).check_function('open', index=0).check_args(0).has_equal_value()
with_body = Ex().check_with(0).check_body().test_function('print')
for_body = with_body.check_for_loop(0).check_body()
for_body.test_function('print', incorrect_msg = 'Incorrect output')

```

--- type:NormalExercise lang:python xp:100 skills:2 key:1b865f62b7
## Expression tests (1)

NOTE: Ended up using spec1 due to time constraints.

#### fail 1 - "wrong if test"

```
def callback():
    if select1.value == 'WRONGVAL':
        select2.value = 1
    else:
        select2.value = 2
```

#### fail 2 - "need assign select2 value in if"

```
def callback():
    if select1.value == 'a':
        pass
    else:
        select2.value = 2
```

#### fail 3 - "wrong select2 value in if"

```
def callback():
    if select1.value == 'a':
        select2.value = 'WRONGVAL'
    else:
        select2.value = 2
```

#### fail 4 - "wrong select2 value in else"

```
def callback():
    if select1.value == 'a':
        select2.value = 1
    else:
        select2.value = 'WRONGVAL'
```



*** =pre_exercise_code
```{python}
class Select:
    """Calls self.callback whenever self.value is set"""
    
    def __init__(self, value):
        self.callback = None
        self._value = value
        
    def on_change(self, cb):
        self.callback = cb
    
    @property
    def value(self): return self._value
    
    @value.setter
    def value(self, x):
        self._value = x
        if self.callback: self.callback()

```

*** =sample_code
```{python}
select1 = Select(value='a')
select2 = Select(value=1)

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
    Ex().has_equal_value(expr_code = name+'.value')
# Put SCTs below here ----
#fn_body = Ex().check_function_def('callback').check_body()
#fn_body.check_if_else(0).has_equal_ast()

#Spec1

pre_code = """
select1 = Select(value="a")
select2 = Select(value=1)
"""

def inner_test():
    test_if_else(
            test = test_expression_result(context_vals=["a"], incorrect_msg = 'wrong if test'),
            body = test_object_after_expression('select2', undefined_msg = 'need assign select2 value in if', incorrect_msg = "wrong select2 value in if"),
            orelse = test_object_after_expression('select2', pre_code = pre_code, incorrect_msg = "wrong select2 value in else")
            )

test_function_definition("callback", body=inner_test)

```

--- type:NormalExercise lang:python xp:100 skills:2 key:82a04869ae
## Expression tests (2)

#### pass

```
def f(c, b=1, *args, **kwargs):
    if c > 1: return c + b
```

NOTE: I need to spend more time on the `if` statement. `has_equal_ast` does not accept anything other than `a`.

#### pass

```
def f(c, b=1, *args, **kwargs):
    print(args)
    if c > 1: return c + b
```

#### fail 1 - "b should be kw arg"

```
def f(a, b, *args, **kwargs): 
    if a > 1: return a + b
```

#### fail 2 - "incorrect if test"

```
def f(a, b=1, *args, **kwargs):
    if a == 1: return a + b
```


*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
def f(a, b=1, *args, **kwargs): 
    if a > 1: return a + b
```

*** =solution
```{python}
def f(a, b=1, *args, **kwargs):
    if a > 1: return a + b
```

*** =sct
```{python}

fn_def = Ex().check_function_def('f').multi(check_args(0), check_args('b').has_equal_value(), check_args(2), check_args(3))

fn_body = fn_def.check_body()

fn_body.check_if_else(0).check_test().has_equal_ast()

```

--- type:NormalExercise lang:python xp:100 skills:2 key:40d94c3753
## Logic tests (1)

#### pass

```
import pandas as pd

x = pd.np.array([1,2,3])
```

#### fail 1 - "numpy array w/wrong values"

```
import numpy as np

x = np.array([1,2])
```

#### fail 2 - "x not numpy array"

```
import numpy as np

x = [1,2,3]
```

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
import numpy as np

x = np.array([1,2,3])
```

*** =solution
```{python}
import numpy as np

x = np.array([1,2,3])
```

*** =sct
```{python}
# NOTE: write 2 SCTs below that would, on their own, pass all cases
# SCT using test_correct

test_correct(test_function('numpy.array', incorrect_msg = 'numpy array w/wrong values', not_called_msg = 'x not numpy array'),
             test_object('x', incorrect_msg = 'numpy array w/wrong values'))
 
# SCT using test_or
#test_or(test_function('numpy.array', incorrect_msg = 'numpy array w/wrong values', not_called_msg = 'x not numpy array'),
#        test_object('x', incorrect_msg = 'numpy array w/wrong values'))
        

```
--- type:NormalExercise lang:python xp:100 skills:2 key:e29e74e2f3
## Processes

NOTE: Didn't get to this in time.

Only need to make solution work!


*** =instructions

*** =hint

*** =pre_exercise_code
```{python}
from bokeh.plotting import figure
p = figure(x_axis_label='fertility (children per woman)', 
           y_axis_label='female_literacy (% population)')

class A:
    def __init__(self, value): 
        self.value = value
        self.pickle_poison = p
```

*** =sample_code
```{python}
a = A(value=1)
```

*** =solution
```{python}
a = A(value=1)
```

*** =sct
```{python}
Ex().check_object('a').has_equal_value()
```

--- type:NormalExercise lang:python xp:100 skills:2 key:d874e260cb
## Function Signatures

NOTE: I don't know how to test optional kwargs. Ended up using `test_function`, commented out my attempts with `check_function` and `test_function_v2`.

#### pass -

```
plot([1,2], [3,4], color='b')
```

#### fail 1 - "forgot a pos arg"

```
plot([1,2], color='b', shape='.')
```

#### fail 2 - "check first arg"

```
plot([1], [3,4], color='b', shape='.')
```

#### fail 3 - "forgot color"

```
plot([1,2], [3,4], shape='.')
```

#### fail 3 - "check color arg"

```
plot([1,2], [3,4], color='red', shape='.')
```


*** =pre_exercise_code
```{python}
def plot(*args, **kwargs):
    """
    args is positional arguments x, y
    kwargs may include color or shape
    """
    pass
```

*** =sample_code
```{python}
plot([1,2], [3,4], color='b', shape='.')
```

*** =solution
```{python}
plot([1,2], [3,4], color='b', shape='.')
```

*** =sct
```{python}
test_function("plot", args=[0,1], keywords=['color', 'shape'])

#Ex().check_function('plot', 0).multi(check_args(0).has_equal_value("check first arg"), check_args(1).has_equal_value("check second arg"), #check_args('color').has_equal_value("check color arg"), check_args('shape').has_equal_value("check shape arg"))


#sig = sig_from_params(param("x", param.POSITIONAL_OR_KEYWORD),
#                      param("y", param.POSITIONAL_OR_KEYWORD),
#                      param("color", param.POSITIONAL_OR_KEYWORD),
#                      param("shape", param.POSITIONAL_OR_KEYWORD))
#test_function_v2("plot", params=["x"], signature=sig, index=1, incorrect_msg = 'check first arg', not_called_msg='forgot a pos arg')
#test_function_v2("plot", params=["y"], signature=sig, index=1, incorrect_msg = 'check second arg', not_called_msg='forgot a pos arg')
#test_function_v2("plot", params=["color"], signature=sig, index=1, incorrect_msg='check color arg', not_called_msg = 'forgot color')
#test_function_v2("plot", params=["shape"], signature=sig, index=1)

```

--- type:NormalExercise lang:python xp:100 skills:2 key:20c3c210c6
## More Functions

NOTE: Didn't get to this in time.

#### pass 1

```
x = [1,2,3]
c.a(x).b('X', 'Y')
```

#### fail 1 - "incorrect arg for some_list"

```
c.a([1,2])
```

#### fail 2 - "forgot y arg in c.a.b"

```
c.a([1,2,3]).b('X')
```

#### fail 3 - "incorrect x arg in c.a.b"

```
c.a([1,2,3]).b('Z', 'Z')
```


*** =pre_exercise_code
```{python}
class Chain():
    def a(self, some_list):
        return self
    
    def b(self, x, y):
        print(x)
        return self

c = Chain()
```

*** =sample_code
```{python}
c.a([1,2,3]).b('X', 'Y')
```

*** =solution
```{python}
c.a([1,2,3]).b('X', 'Y')
```

*** =sct
```{python}
```
