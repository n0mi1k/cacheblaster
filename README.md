# cacheblaster
A web cache poisoning denial of service (CPDoS) test tool written in Python. This tool sends requests of different header payloads to force an error which may be cached on the server. If successful, this can causes a denial of service attack when other users browse to the same URL. This causes other users to see the similar error instead of loading the desired the page properly.

## Payload Options
1. **HTTP Meta Characters [Default]** - Sends harmful meta characters such as \0x7\x07
2. **Oversized HTTP Header** - Sends oversized header > 8192 bytes (Slow)
3. **HTTP Method Override** - Override with unsupported HTTP method (Default=DELETE)

## Usage
```
Usage:
  python3 cacheblaster.py -u [URL] [Other Flags]

Flags:
  -u, --url            The target URL [Required]
  -c, --cachebuster    Enable cachebuster to avoid affecting other users [Default=Disabled]
  -p, --payload        Payload to use (1. HTTP Metachars, 2. Oversize Header, 3. Method Override)
  -t, --threads        Number of threads to use [Default=20]
  -r, --request        Number of payload requests to send [Default=100]
  -h, --help           Display the help page

```
**Note:** Enable cachebuster mode with `-c` to avoid DoS on active pages

## Demo Run
![cachebuster](https://github.com/n0mi1k/cacheblaster/assets/28621928/8ed5b750-63c7-4f3b-bca5-828619dc3b76)

## Testing Tips
- Use on a URL that obtains a 200 response [Recommended]
- Enable cachebuster to prevent affecting other users with `-c`, a GET parameter URL will be generated
- If a non 200 OK response is obtained, visit the URL to see if the error response is cached
- This test requires trial an error. If it is not successful, try using a different path or run again later
- Sometimes a vulnerable page may show that it is not, as the 200 OK responses are cached

## Disclaimer

This tool is for educational and testing purposes only. Do not use it to exploit the vulnerability on any system that you do not own or have permission to test. The authors of this script are not responsible for any misuse or damage caused by its use.
