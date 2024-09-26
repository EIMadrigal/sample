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


```python
import json

try:
    with open('data.json', 'r', encoding='utf-8') as f:
        parsed_json = json.load(f)
except Exception as e:
    print(f"Error: {e}")
else:
    print(type(parsed_json))
    print(parsed_json)




my_dict = {
    'first_name': 'Guido',
    'second_name': 'Rossum',
    'titles': ['BDFL', 'Developer'],
}

try:
    with open('data.json', 'w', encoding='utf-8') as f:
        json.dump(my_dict, f)
except Exception as e:
    print(f"Error: {e}")




json_str = '{"first_name": "Guido", "last_name":"Rossum"}'
try:
    parsed_json = json.loads(json_str)
except Exception as e:
    print(f"Error: {e}")
else:
    print(parsed_json)




json_str = json.dumps(my_dict)
print(json_str)

```
