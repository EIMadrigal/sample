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
    end = time.time()
    print(f'{filename} download finish, time: {end - start:.3f}s')


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

```python
from threading import Thread
import time
import random


class DownloadThread(Thread):

    def __init__(self, filename):
        self.filename = filename
        super().__init__()

    def run(self):
        start = time.time()
        print(f'start downloading {self.filename}')
        time.sleep(random.randint(3, 6))
        end = time.time()
        print(f'{self.filename} download finish, time: {end - start:.3f}s')


def main():
    threads = [
        DownloadThread('a.txt'),
        DownloadThread('b.exe'),
        DownloadThread('c.yml')
    ]
    start = time.time()
    for thread in threads:
        thread.start()
    for thread in threads:
        # main thread gets blocked until thread terminates
        thread.join()
    end = time.time()
    print(f'total download time: {end - start:.3f}s')


if __name__ == '__main__':
    main()
```


```python
import time
import random
from concurrent.futures import ThreadPoolExecutor


def download(*, filename):
    start = time.time()
    print(f'start downloading {filename}')
    time.sleep(random.randint(3, 6))
    end = time.time()
    print(f'{filename} download finish, time: {end - start:.3f}s')


def main():
    with ThreadPoolExecutor(max_workers=4) as pool:
        filenames = ['a.txt', 'b.exe', 'c.yml']
        start = time.time()
        for filename in filenames:
            # non-block, return a handle on the task immediately
            pool.submit(download, filename=filename)
    end = time.time()
    print(f'total download time: {end - start:.3f}s')


if __name__ == '__main__':
    main()
```

```python
import time
from threading import Thread


def display(content):
    while True:
        print(content, end='', flush=True)
        time.sleep(0.1)


def main():
    '''
    The daemon thread will accompany with all non-daemon threads
    The entire Python program exits when only daemon threads are left
    https://stackoverflow.com/questions/23285743
    https://stackoverflow.com/questions/1489669
    '''
    Thread(target=display, args=('Ping', )).start()
    Thread(target=display, args=('Pong', ), daemon=True).start()
    time.sleep(5)


if __name__ == '__main__':
    main()
```
