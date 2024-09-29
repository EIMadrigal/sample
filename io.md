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

[How does do client authentication work over https](https://security.stackexchange.com/questions/187694/how-does-do-client-authentication-work-over-https)

[Why must I send certificate and private key when make HTTPS requests](https://security.stackexchange.com/questions/240214/why-must-i-send-certificate-and-private-key-when-make-https-requests)

```python
import requests
import json

url = 'https://bing.com/api/users'

response = requests.get(url, verify=True, cert=('/path/to/cert.pem', '/path/to/private.key'))
print(response.status_code)



headers = {'Content-Type': 'application/json'}
payload = {'name': 'John', 'mail': 'john@gmail.com'}
response = requests.post(url, headers=headers, data=payload)
response = requests.post(url, headers=headers, json=json.dumps(payload))


# load json into dict if dealing with JSON data
try:
    response_dict = response.json()
except requests.exceptions.JSONDecodeError as e:
    print(f'Error: {e}')
else:
    print(response_dict)

```


```python
from threading import Thread
import time
import random


# keyword-only argument
def download(*, filename):
    start = time.time()
    print(f'start downloading {filename}')
    time.sleep(random.randint(3, 6))
    print(f'finish downloading {filename}')
    end = time.time()
    print(f'{filename} download time: {end - start:.3f}s')


def main():
    threads = [
        Thread(target=download, kwargs={'filename': 'a.txt'}),
        Thread(target=download, kwargs={'filename': 'b.exe'}),
        Thread(target=download, kwargs={'filename': 'c.yml'})
    ]
    start = time.time()
    for thread in threads:
        thread.start()
    '''
    thread status is stopped if function finishes, but still exists and joinable
    https://stackoverflow.com/questions/56163276
    https://stackoverflow.com/questions/15085348
    '''
    for thread in threads:
        # main thread gets blocked until thread terminates
        thread.join()
    end = time.time()
    print(f'total download time: {end - start:.3f}s')


if __name__ == '__main__':
    main()
```
