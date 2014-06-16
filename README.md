jcurl: JSON-oriented cURL wrapper

This is a small utility to make curl easier when working with JSON-based APIs.

It wraps calls to `curl`, with the following changes:

- adds --data-json, which is encoded as json.
- (optionally) encode -d data as json.
- add "Accept: application/json" and "Content-Type: application/json".
- If the response is valid json, pretty-print it; Else, just dump it as is.


Example:

  Before:

    ~$ curl graph.facebook.com
    {"error":{"message":"Unsupported get request.","type":"GraphMethodException","code":100}}~$ <prompt>


  After:

    ~$ jcurl graph.facebook.com
    {
      "error": {
        "message": "Unsupported get request.",
        "code": 100,
        "type": "GraphMethodException"
      }
    }
    ~$ <prompt>



Usage:

  jcurl [options] [-- [curl_options]] [URL...]

  Any argument not understood by jcurl, and any argument after the first `--`,
  are passed directly to the `curl` command. These arguments will take precedent
  over any argument generated by jcurl.

  Options:

    -h, --help          Show a help message.

    --data-json <data>  Encode this data as JSON. <data> format is based on the
                        format commonly used with curl:
                          `name=content`
                        jcurl will collect all --data-json arguments and encode
                        them as a single json object.

    --no-json-data      By default, jcurl will parse `-d` as `--data-json`. with
                        --no-json-data, they will be passed directly to curl.
    --no-accept         Do not send 'Accept: application/json' header.
    --no-content-type   Do not send 'Content-Type: application/json' header.
                        (A content-type header will only be added if there is
                        content).

    --[no-]pretty       jcurl will try to pretty-print if output is tty. Use
                        these commands to force it to, or not to, pretty-print.

    --no-silence        jcurl adds `-sS` by default, to suppress the progress
                        bar. Use this option to not add it.

Gotchas:

  curl dumps the output of `-i` onto stdout, which breaks jcurl's ability to
  parse any json out of it. `-v` goes to stderr, so it will still work.


Installation:

  Just copy (or symlink) the `jcurl` file to ~/bin/jcurl (Or any other location
  in your PATH).
  Python is required.



TODO:

- Support -i (by parsing either -i or -v).
- Bash completions
