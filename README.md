# Proof of concept not intended for use.

# pycurltx

`pycurltx` provides an `httpx` transport that executes requests with `pycurl`.

This is a proof of concept and is not meant to be used.

## Install

```bash
pip install pycurltx
```

## Usage

```python
import httpx
from pycurltx import PyCurlTx

transport = PyCurlTx(timeout=10.0)
async with httpx.AsyncClient(transport=transport) as client:
    response = await client.get("https://example.com")
    print(response.status_code)
    print(response.text)

debug_transport = PyCurlTx(
    verbose=True,
    debug_callback=lambda info_type, data: print(info_type, data),
)
```

## Notes

- This transport is implemented on top of pycurl's multi interface.
- Verbose curl logging is supported via `verbose=True` and optional `debug_callback`.

## TODO

- curl supports proxies
- curl supports native certificate store on some builds
- configure curl to use cacerts store
- ...