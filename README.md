jcurl: JSON-oriented cURL wrapper

The plan is:

- Validate input is actually json
- add "Accept: application/json" and "Content-Type: application/json" (Where applicable).
- try to parse response body as json; If successful, pretty-print it. Else, dump as-is.
