# Test resources for sandbox error CORS

## Content

- [`html/`](html/) ― The page loading the external script.
- [`script/`](script/) ― The external script.
    * The script is hosted on GitHub Pages for testing purposes: https://santosoj.github.io/corscheck/script/app.js

## Testing

- Serve `html/` locally:
  ```shell
  npm i -g serve
  serve  # defaults to port 3000
  ```
- Point an ngrok domain to local:
  ```shell
  ngrok http --domain <yourdomain>.ngrok.io 3000
  ```
- Open the page in the browser through `<yourdomain>.ngrok.io`
- The external script throws a `ReferenceError`. Observe the output from `window.onerror` in the browser console.
- Use Chrome [header overrides](https://developer.chrome.com/docs/devtools/overrides/) to change the value of the `Access-Control-Allow-Origin` header.

## Test results

```yaml
"Access-Control-Allow-Origin set to script domain | crossorigin=anon..
  Script fails to load with CORS error.
"Access-Control-Allow-Origin set to script domain | no crossorigin":
  window.onerror:
    event: Script error.
    source:
    lineno: 0
    colno: 0
    error: null
    new Error().stack: >
      "Error at window.onerror
      (https://shoopshoop.au.ngrok.io/:28:46)"
    using captureStackTrace: >
      "Error at window.onerror
      (https://shoopshoop.au.ngrok.io/:19:17)"
"Access-Control-Allow-Origin: * | crossorigin=anonymous":
  window.onerror:
    event: "Uncaught ReferenceError: bar is not defined"
    source: https://santosoj.github.io/app.js
    lineno: 3
    colno: 5
    error: "ReferenceError: bar is not defined"
    new Error().stack: >
      "Error at window.onerror
      (https://shoopshoop.au.ngrok.io/:28:46)"
    using captureStackTrace: >
      "Error at window.onerror
      (https://shoopshoop.au.ngrok.io/:19:17)"
"Access-Control-Allow-Origin: * | no crossorigin":
  window.onerror:
    event: Script error.
    source:
    lineno: 0
    colno: 0
    error: null
    new Error().stack: >
      "Error at window.onerror
      (https://shoopshoop.au.ngrok.io/:28:46)"
    using captureStackTrace: >
      "Error at window.onerror
      (https://shoopshoop.au.ngrok.io/:19:17)"
```
---- 
