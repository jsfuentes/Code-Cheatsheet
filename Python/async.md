# Async Options

- `concurrent.futures` (thread pooling)
- `threading`

- `multiprocessing`
- `asyncio`

```python
if io_bound:
    if io_very_slow:
        print("Use Asyncio") #Many connections
    else:
       print("Use Threads") #Limited connections
else: 
    print("Multi Processing") #CPU Bound
```

## Asyncio

### Why asyncio?

Well, Global Interpreter Lock aka GIL was introduced to make CPython’s memory handling easier and to allow better integrations with C (for example the extensions). The GIL is a locking mechanism that the Python interpreter runs **only one thread at a time.** Multiple process work, but are expensive. 

The revolution is the *event loop*. An event loop basically waits for something to happen and then acts on the event. The event loop tracks different I/O events and switches to tasks which are ready and pauses the ones which are waiting on I/O. Thus we don’t waste time on tasks which are not ready to run right now.

### Background

**As of 9/8/18, async doesn't work very well in jupyter notebooks(probs displaying errors and underlying event loop already running)**

Async python stand library, new in py version 3.4

Uses **coroutines** which allow a ft to return without losing its state i.e python yielding iterators. Difference with threads is these are collaborative and only one coroutine run at a time, while threads are parallel

ask is a wrapper for a coroutine and a subclass of Future.

## Async/Await

Python has native support for async functions defining a coroutine. Calling these functions doesn't run the code, but returns a JS promise-like coroutine object

```python
import asyncio

async def ping_server(ip):  
    pass

@asyncio.coroutine
def load_file(path):  
    pass
```

To actually call these fts, use `await` inside another ft

```python
async def ping_local():  
    return await ping_server('192.168.1.1')
```

## Event Loop

```python
asyncio.get_event_loop().run_until_complete(my_ft()) #run ft is blocking
```

To add something to event loop

```python
asyncio.ensure_future(my_ft())
```

`loop.run_forever()` #run forever

## Important Fts

```python
await asyncio.sleep(5) #to sleep

page.waitForSelector('h3 a', { timeout: 5000 }) # default timeout 30 seconds

```

## Tasks

These let you return values from a sync ft and ??

```python
import asyncio
 
 
async def my_task(seconds):
    """
    A task to do for a number of seconds
    """
    print('This task is taking {} seconds to complete'.format(
        seconds))
    await asyncio.sleep(seconds)
    return 'task finished'
 
 
if __name__ == '__main__':
    my_event_loop = asyncio.get_event_loop()
    try:
        print('task creation started')
        task_obj = my_event_loop.create_task(my_task(seconds=2))
        my_event_loop.run_until_complete(task_obj)
    finally:
        my_event_loop.close()
 
    print("The task's result was: {}".format(task_obj.result()))
```

## Example

We use `aiohttp` for async requests, if we just used urllib or something then this whole async thing wouldn't be helpful. 

Writing is still sync, but could use async file io lib 

```python
import aiohttp
import asyncio
import async_timeout
import os
 
 
async def download_coroutine(session, url):
    with async_timeout.timeout(10):
        async with session.get(url) as response:
            filename = os.path.basename(url)
            with open(filename, 'wb') as f_handle:
                while True:
                    chunk = await response.content.read(1024)
                    if not chunk:
                        break
                    f_handle.write(chunk)
            return await response.release()
 
 
async def main(loop):
    urls = ["http://www.irs.gov/pub/irs-pdf/f1040.pdf",
        "http://www.irs.gov/pub/irs-pdf/f1040a.pdf",
        "http://www.irs.gov/pub/irs-pdf/f1040ez.pdf",
        "http://www.irs.gov/pub/irs-pdf/f1040es.pdf",
        "http://www.irs.gov/pub/irs-pdf/f1040sb.pdf"]
 
    async with aiohttp.ClientSession(loop=loop) as session:
        tasks = [download_coroutine(session, url) for url in urls]
        await asyncio.gather(*tasks)
 
 
if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main(loop))
```