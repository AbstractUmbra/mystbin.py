# MystBin.py!

A small simple wrapper around the [MystB.in](https://mystb.in/) API.

----------
![Code Linting](https://github.com/AbstractUmbra/mystbin.py/workflows/Code%20Linting/badge.svg?branch=main)
![Code Analysis](https://github.com/AbstractUmbra/mystbin.py/workflows/Code%20Analysis/badge.svg?branch=main)
![Build](https://github.com/AbstractUmbra/mystbin.py/workflows/Build/badge.svg)
### Features

- [x] - `POST`ing to the API, which will return the provided url.
- [x] - `GET`ting from the API, provided you know the URL or paste ID.
- [ ] - `DELETE`ing from the API, provided the paste is attached to your account.
- [ ] - `PATCH`ing to the API, provided the paste is attached to your account.
- [x] - Ability to pass in a sync or async session / parameter so it is flexible.
- [x] - Write a real underlying Client for this, it will be required for...
- [ ] - ... Authorization. Awaiting the API making this public as it is still WIP.

### Installation
This project will be on [PyPI](https://pypi.org/project/mystbin.py/) as a stable release, you can always find that there.

Installing via `pip`:
```shell
python -m pip install -U mystbin.py
# or for optional sync addon...
python -m pip install -U mystbin.py[requests]
```

Installing from source:
```shell
python -m pip install git+https://github.com/AbstractUmbra/mystbin-py.git #[requests] for sync addon
```

### Usage examples
Since the project is considered multi-sync, it will work in a sync/async environment, see the optional dependency of `requests` below.

```py
# async example - it will default to async
import mystbin

mystbin_client = mystbin.Client()
#NOTE: The `api_key` kwarg in the Client constructor is optional.

paste = await mystbin_client.post("Hello from MystBin!", syntax="python")
str(paste)
>>> 'https://mystb.in/<your generated ID>.python'

paste.url
>>> 'https://mystb.in/<your generated ID>.python'

get_paste = await mystbin_client.get("https://mystb.in/<your generated ID>")
str(get_paste)
>>> "Hello from MystBin!"

paste.created_at
>>> datetime.datetime(2020, 10, 6, 10, 53, 57, 556741)
```

```py
# sync example - we need to pass a session though
import mystbin
import requests

sync_session = requests.Session()
mystbin_client = mystbin.Client(session=sync_session)
#NOTE: The `api_key` kwarg in the Client constructor is optional.

paste = mystbin_client.post("Hello from sync Mystb.in!", syntax="text")
str(paste)
>>> 'https://mystb.in/<your generated ID>.text'
```

NOTE: There is a timeout of 15s for each operation.

### Dependencies

`aiohttp` - required \
`requests` - optional