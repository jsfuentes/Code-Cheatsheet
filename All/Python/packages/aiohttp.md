# AIOHTTP

ASYNC HTTP Client/Server, see asyncio for more async info

```bash
pip install aiohttp
pip install cchardet #Optional Faster Replacement
pip install aiodns #highly recommended to speed up DNS
```

## Client

A session contains a connection pool inside and good for multiple requests

```python
async with aiohttp.ClientSession() as session:
    async with session.get('http://httpbin.org/get') as resp:
        print(resp.status)
        print(await resp.text())
```

```python
session.get('http://httpbin.org/get',                       params={'key1': 'value1', 'key2': 'value2'})
session.post('http://httpbin.org/post', data=b'data')
session.put('http://httpbin.org/put', data=b'data')
session.delete('http://httpbin.org/delete')
session.head('http://httpbin.org/get')
session.options('http://httpbin.org/get')
session.patch('http://httpbin.org/patch', data=b'data')
```

### Full Asyncio Ex

```python
import aiohttp
import asyncio

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main():
    async with aiohttp.ClientSession() as session:
        html = await fetch(session, 'http://python.org')
        print(html)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

