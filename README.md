# cacheblaster
A web cache poisoning denial of service (CPDoS) test tool written in Python. This tool sends requests of different header payloads to force an error on the target which may be cached on the server. If the response is cached, a denial of service attack occurs when affected URLs stop loading properly. It can also disrupt the functionalities and cause abnormal behaviors on the website by preventing dependant files such as JS and CSS from loading.

<img src="https://github.com/n0mi1k/cacheblaster/assets/28621928/3370ff1c-94cc-45da-940e-130ff76220f1" width="620">

## Payload Options
1. **HTTP Meta Characters [Default]** - Sends harmful meta characters such as \x07\x07
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

## Demo Attack
<img src="https://github.com/n0mi1k/cacheblaster/assets/28621928/bf1c88e4-a100-4f96-82d4-2d6555f37dae" width="620">

Above demo is on a vulnerable target running on a Cloudflare CDN. After sending the payload, the error response is cached and the page no longer loads. A cachebuster GET parameter is used to prevent other users from being affected by the DoS.

## Testing Tips
- Use on a URL that obtains a 200 response [Recommended]
- Enable cachebuster to prevent affecting other users with `-c`, a GET parameter URL will be generated
- If a non 200 OK response is obtained, visit the URL to see if the error response is cached
- This test requires trial an error. If it is not successful, try using a different path or run again later
- Sometimes a vulnerable page may show that it is not vulnerable, when the 200 OK responses are cached
- False positives are expected, always validate again by browsing the URL

## Disclaimer

This tool is for educational and testing purposes only. Do not use it to exploit the vulnerability on any system that you do not own or have permission to test. The authors of this script are not responsible for any misuse or damage caused by its use.
