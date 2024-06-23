# grok-regexp

This is a tool that interprets the format of the Grok pattern contained in the passed string and converts it into a named capturing group through a native JavaScript regular expression.

## Usage

```sh
npm install @okuryu/grok-regexp
```

```ts
import { GrokRegExp } from "@okuryu/grok-regexp";

const pattern =
  '%{IP:client} \\[%{TIMESTAMP_ISO8601:timestamp}\\] "%{WORD:method} %{URIHOST:site}%{URIPATHPARAM:url}" %{INT:code} %{INT:request} %{INT:response} - %{NUMBER:took} \\[%{DATA:cache}\\] "%{DATA:mtag}" "%{DATA:agent}"';
const input =
  '203.35.135.165 [2016-03-15T12:42:04+11:00] "GET memz.co/cloud/" 304 962 0 - 0.003 [MISS] "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/48.0.2564.116 Safari/537.36"';

const gre = new GrokRegExp(pattern);
const result = gre.exec(input);
console.log(result?.groups);
```

```json
{
  "client": "203.35.135.165",
  "timestamp": "2016-03-15T12:42:04+11:00",
  "method": "GET",
  "site": "memz.co",
  "url": "/cloud/",
  "code": "304",
  "request": "962",
  "response": "0",
  "took": "0.003",
  "cache": "MISS",
  "mtag": "-",
  "agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/48.0.2564.116 Safari/537.36"
}
```
