```python
import os

"""
if file not exist or cannot open, got error
both open and read may be error when running
"""
file_path = os.path.abspath('file.txt')
try:
    with open(file_path, 'rt', encoding='utf-8') as f:
        text = f.read()
except OSError as e:
        print(f"Error: {e}")


file_path = os.path.abspath('file.txt')
try:
    with open(file_path, 'wt', encoding='utf-8') as f:
        f.write('hello\n')
except OSError as e:
        print(f"Error: {e}")


```



```python
# check the value of x (False, [], None, '', 0)
if x:

# compare the reference (memory addr) of x and None (singleton)
if x is not None:
```
