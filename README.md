# rpc.py

An easy-to-use and powerful RPC framework. Base WSGI & ASGI.

## Usage

Server side:

```python
import uvicorn
from rpcpy import RPC

app = RPC()


@app.register
async def sayhi(name: str) -> str:
    return f"hi {name}"


if __name__ == "__main__":
    uvicorn.run(app.asgi, interface="asgi3", port=65432)
```

Client side:

```python
import httpx
from rpcpy.client import Client

app = Client(httpx.Client(), base_url="http://127.0.0.1:65432")


@app.remote_call
def sayhi(name: str) -> str:
    ...


if __name__ == "__main__":
    print(sayhi("rpc.py"))
```