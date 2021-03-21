# Requests

**requests** - python-пакет для автоматизации пывна через HTTP.

## Запрос

`get('http://example.com/')` - GET-запрос на указанный URL

`get('http://example.com/', {'queryParam1': 'hello', 'queryParam2': 'world'})` - GET-запрос на указанный URL с Query-параметрами

`post('http://example.com/')` - Пустой POST-запрос на указанный URL

`post('http://example.com/', {'formParam1': 'hello', 'formParam2': 'world'})` - POST-запрос на указанный URL с <u>form-encoded</u> параметрами

`post('http://example.com/', b'formParam1=hello&formParam2=world')` - POST-запрос на указанный URL с сырыми байтами в качестве параметров

`post('http://example.com/', file_object)` - POST-запрос на указанный URL с файлом

остальное - см. справку `requests.request?`



## Ответ

`headers` - словарь заголовков

`text` - закодированный текст тела ответа (юникод)

`content` - байты тела ответа



## Сессии

Сессия запоминает куки и хранит соединение с сервером (TCP connect)

```python
from requests import Session

s = Session()
r = s.post('http://example.com/login', {'login': 'Patrick', 'password': 'p@$5w0rD!'})
r = s.get('http://example.com/profile')
```

Альтернативно можно использовать [CookieJar](https://requests.readthedocs.io/en/latest/api/#requests.cookies.RequestsCookieJar) для сохранения кук в файл или другое хранилище.



## Debug

Включение дебага, 1 способ:

```python
import requests
import logging
import httplib

# Debug logging
httplib.HTTPConnection.debuglevel = 1
logging.basicConfig()
logging.getLogger().setLevel(logging.DEBUG)
req_log = logging.getLogger('requests.packages.urllib3')
req_log.setLevel(logging.DEBUG)
req_log.propagate = True
```

2 способ:

```python
# source: https://stackoverflow.com/a/57325050/10504918

import requests
import logging
from http.client import HTTPConnection  # py3

log = logging.getLogger('urllib3')
log.setLevel(logging.DEBUG)

# logging from urllib3 to console
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)
log.addHandler(ch)

# print statements from `http.client.HTTPConnection` to console/stdout
HTTPConnection.debuglevel = 1
```

