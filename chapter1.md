---
title       : Insert the chapter title here
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


--- type:NormalExercise lang:python xp:100 skills:1 key:03eebf7448
## Simple tests (1)

### pass 1

```python
import numpy

x = numpy.array([1,2,3])

print(x)
```

### pass 2

```python
import numpy as npp

x = y = npp.array([1,2,3])

print(y)
```

### fail 1

```python
import numpy as np

x = [1,2,3]

print(x)
```

### fail 2

```python
import pandas as pd

x = pd.np.array([1,2,3])

print(x)
```

*** =instructions
- instruction 1

*** =hint
- hint 1

*** =pre_exercise_code
```{python}
```

*** =sample_code
```{python}

```

*** =solution
```{python}
import numpy as np

x = np.array([1,2,3])

print(x)
```

*** =sct
```{python}
# "did you import numpy?"

# "x is undefined"
# "your value of x is incorrect"

# "expected [1,2,3] in your output"

```

--- type:NormalExercise lang:python xp:100 skills:2 key:d71dfcb25c
## Simple tests (2)


*** =instructions

*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}
def f(a): return a*2

f("b")
```

*** =solution
```{python}

```

*** =sct
```{python}

```
