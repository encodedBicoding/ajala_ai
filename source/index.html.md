---
title: Ajala AI

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript
  - c++

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
includes:
  - errors

search: true

code_clipboard: true
---

# Authentication

## Get Help
> Make sure to replace `XXXXXXXXXX` with your API key.

```shell
# With shell, you can just pass the correct header with each request
curl "http://api.ajala.ai/help"
  -H "api_key: XXXXXXXXXXXXXXXXXXXXX"
```

```python
import ajala

api = ajala.authorize('XXXXXXXXXXX')
```

```javascript
const ajala = require('ajala');

let api = ajala.authorize('XXXXXXXXXXX');
```

```cpp
import ajala;

void main() {
  var api = ajala.authorize('XXXXXXXXXXXXXX')
}
```

> The above command returns JSON structured like this:

```json
{
  "account_sid": "YYYYYYYYYYYY",
  "api_version": "v1",
  "date_created":"<UTC Time>",
  "date_sent":"<UTC TIme>",
  "error_code": null,
  "error_message": null,
  "status": "OK",
  "asr":"/v1/asr",
  "tts":"/v1/tts",
  "data": {
    "/v]/data": [
      "/v1/data/language",
      "/v1/data/audit"
    ],
  }
}
```


GET help TEXT GOES HERE

## POST Audio Recording
```shell
# With shell, you can just pass the correct header with each request
curl -H 'Content-Type: application/x-www-form-urlencoded' \
-d '{"language": "<language>", 
    "context":"<context>", 
    "audioFile":"<encoded_audio_file>", 
    "audioFrequency":"<sample_rate>", 
    "transcription_id":"ZZZZZZZZZZZZZ", 
    "API_KEY":"XXXXXXXXXXX", 
    "ACCOUNT_SID":"YYYYYYYYYY"}' \ 
  http://api.ajala.ai/v1/asr
```

```python
import requests
AJALA_API_URL = "http://api.ajala.ai/v1/asr"
data = {
  language: "<language>",
  context: "<context>",
  audioFile: "<encoded_audio_file>",
  audioFrequency: "<sample_rate>",
  transcription_id:"zzzzzzzzzzzzzzzzz",
  API_KEY: "XXXXXXXXX",
  ACCOUNT_SID: "YYYYYYYYYY"
}

response = requests.post(AJALA_API_URL, data)
print(response.json())
```

```javascript
const fetch = require('node-fetch');
const AJALA_API_URL = "http://api.ajala.ai/v1/asr";
const data = {
  language: "<language>",
  context: "<context>",
  audioFile: "<encoded_audio_file>",
  audioFrequency: "<sample_rate>",
  transcription_id:"zzzzzzzzzzzzzzzzz",
  API_KEY: "XXXXXXXXX",
  ACCOUNT_SID: "YYYYYYYYYY"
};

fetch(AJALA_API_URL, data)
.then(resp => resp.json())
.then((result) => {
  console.log(result);
})

```

```cpp
import ajala;

void main() {
  var api = ajala.authorize('XXXXXXXXXXXXXX')
}
```

> The above command returns JSON structured like this:

```json
{
  "account_sid": "YYYYYYYYYYYY",
  "api_version": "v1",
  "date_created":"<UTC Time>",
  "date_sent":"<UTC TIme>",
  "error_code": null,
  "error_message": null,
  "status": "OK",
  "hypothesis": [
    {
      "utterance": "utterance in specified language"
    }
  ],
  "id":"873903cls-438jdieo933"
}
```
POST TEXT GOES HERE


# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

