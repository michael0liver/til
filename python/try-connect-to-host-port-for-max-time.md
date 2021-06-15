# Wait for port to open on host

I was using PostgreSQL inside a Python application and wanted to wait a specific length of time for the database to become available before giving up.

I built a reusable function (async) function for this:

```python
import asyncio
import time


async def wait_for_host_port(
    host: str,
    port: int,
    duration: int = 10,
    interval: int = 2,
) -> bool:
    """Wait for a port on a host to open until `duration` seconds has passed.

    Args:
        host: Host ip address or hostname.
        port: Port number.
        duration: Total duration in seconds to wait. Defaults to 10.
        interval: Delay in seconds between each try. Defaults to 2.
    """
    max_time = time.time() + duration
    while time.time() < max_time:
        try:
            _, writer = await asyncio.wait_for(
                asyncio.open_connection(host, port), timeout=5
            )
            writer.close()
            await writer.wait_closed()
            return True
        except OSError:
            print(f"Unable to connect host='{host}' port='{port}'.")
            await asyncio.sleep(interval)
    return False
```

Called like this:

```python
can_connect = await wait_for_host_port("localhost", 5423, duration=120)
if not can_connect:
    ...
```
