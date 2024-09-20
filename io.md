```python
import os

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
