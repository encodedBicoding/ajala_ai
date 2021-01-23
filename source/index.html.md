---
title: Ajala AI

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript
  - cpp

# toc_footers:
#   - <a href='/login'>Sign Up for a Developer Key</a>
# includes:
#   - errors

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


Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec lacinia elementum imperdiet. Aliquam quis dapibus lorem. Aenean lacinia condimentum sem non pellentesque. Quisque sodales sagittis orci vel accumsan. Morbi quis lectus sed magna fringilla feugiat. Donec id porttitor nunc. Curabitur pellentesque eros ut dolor dictum, sit amet consectetur massa consequat. Maecenas luctus pulvinar aliquet. Ut malesuada orci vel nunc molestie congue. Proin tempor sed nulla ut sodales.

Etiam dapibus mi sed tortor congue efficitur. Cras pharetra lacus et venenatis euismod. Integer vitae mattis risus. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam dignissim ipsum cursus dui rutrum, vel sagittis ligula iaculis. Curabitur ultricies libero et tortor vulputate, in cursus turpis dignissim. In vitae pharetra metus, ac posuere enim. Nulla non malesuada nisl, a dictum magna. Pellentesque malesuada dapibus mi, fringilla luctus lorem. Pellentesque est velit, tincidunt ut lacinia faucibus, pharetra quis turpis. Nulla aliquam non enim id posuere. Pellentesque elementum est eu orci varius, ut bibendum urna tempor. Aenean ac accumsan diam. Vestibulum dictum mattis posuere.

Vestibulum eget lectus efficitur, sollicitudin enim sed, eleifend augue. Pellentesque mattis odio vitae lacus feugiat maximus. Cras id rutrum augue. Donec ut pulvinar eros. Maecenas malesuada magna sit amet nisi dignissim, id accumsan augue imperdiet. Mauris pellentesque nunc sit amet libero efficitur tristique. Morbi in tellus leo. Donec finibus sapien orci. Morbi egestas ex vitae fermentum viverra. Etiam rhoncus faucibus tortor in rutrum. Sed id diam erat. Mauris euismod erat nec felis vestibulum, ac malesuada massa pellentesque. Pellentesque placerat odio mi, in consequat lacus sollicitudin a.


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
import json
import requests
​
ajala_url = "https://api.ajala.ai/v1/asr"
request_body = {"language":"yorubaNG",
                "context":"conversational",
                "audioFrequency":"8000",
                "API_KEY":<API_KEY>}
​
headers = {'Content-Type':'application/json'}
wav_file = "/path/to/wav/file"
audio_upload = {'upload_file':open(wav_file,'rb')}
​
try:
    response = requests.post(ajala_url,json=request_body,headers=headers,files=audio_upload)
except Exception as e:
    print(e)
else:
    transcription = json.load(response.decode('utf-8'))

```

```javascript
function getAudioFile(audioFileName){
    var oReq = new XMLHttpRequest();
    oReq.open("GET", audioFileName, true);
    oReq.responseType = "arraybuffer";
    
    oReq.onload = function (oEvent) {
        var arrayBuffer = oReq.response;
        if (arrayBuffer) {
            var byteArray = new Uint8Array(arrayBuffer);
        }
        console.log(arrayBuffer);
        return arrayBuffer;
    };
    oReq.send(null);
}
​
function callASRAPI(apiURL, audioFileBuffer){
    
    //Initiliaze httprequest
    var Httpreq = new XMLHttpRequest();
    Httpreq.open("POST",apiURL,true);
    //Httpreq.withCredentials=true;
    //Httpreq.setRequestHeader('Content-Type', 'audio/wav');
    Httpreq.onload = function(e){console.log(e)};
    Httpreq.send(audioFileBuffer);
    
    console.log(Httpreq)
}
​
var ajalaURL = "http://api.ajala.ai/v1/asr"
var language = "yorubaNG"
var context = "properNames"
var audioFile = "names.wav"
var API_KEY = "API_KEY"
​
ajalaURL = ajalaURL + "?apikey=" + API_KEY + "&language="+language + "&context=" + context
console.log("ajalaURL:" + ajalaURL)
​
ab = getAudioFile(audioFile);
callASRAPI(ajalaURL,ab);

```

```cpp
#include "json/rapidjson.h"
#include "json/document.h"
#include "curl/curl.h"
#include <sstream>
​
struct string {
    char *ptr;
    size_t len;
};
​
void init_string(struct string *s){
    s->len = 0;
    s->ptr = (char *)malloc(s->len+1);
    if(s->ptr == NULL){
        fprintf(stderr,"malloc() failed\n");
        exit(EXIT_FAILURE);
    }
    s->ptr[0] = '\0';
}
​
size_t writefunc(void *ptr, size_t size, size_t nmemb, struct string *s){
    size_t new_len = s->len + size*nmemb;
    s->ptr = (char *)realloc(s->ptr, new_len+1);
    if(s->ptr==NULL){
            fprintf(stderr,"malloc() failed\n");
            exit(EXIT_FAILURE);
    }
    memcpy(s->ptr+s->len,ptr,size*nmemb);
    s->ptr[new_len] = '\0';
    s->len = new_len;
    return size*nmemb;
}
​
int main(void){
​
    static const char *ajalaURL = "http://api.ajala.ai/v1/asr";
    static const char *wavPath = "/path/to/wav/file/for/transcription";
    static const char *requestFields = "language=<lang>&context=<ctxt>&audioFrequency=<freq>&API_KEY=<API_KEY>";
    
    CURL *curl;
    CURLcode res;
    struct stat fileInfo;
    FILE *fd;
    
    //Read audio file from local store
    fd = fopen(wavPath,"rb");
    curl = curl_easy_init();
    
    //Initialize struct string to capture json response
    struct string s;
    init_string(&s);
    
    try {
        //Configure curl to execute POST request
        curl_easy_setopt(curl, CURLOPT_URL, ajalaURL);
        curl_easy_setopt(curl, CURLOPT_UPLOAD, 1L);
        curl_easy_setopt(curl, CURLOPT_READDATA,fd);
        curl_easy_setopt(curl, CURLOPT_POSTFIELDS,requestFields);
        curl_easy_setopt(curl, CURLOPT_POSTFIELDSIZE, (long)strlen(requestFields));
        curl_easy_setopt(curl, CURLOPT_VERBOSE,1L);
        curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION,writefunc);
        curl_easy_setopt(curl, CURLOPT_WRITEDATA, &s);
         
         //Execute POST request
         res = curl_easy_perform(curl);
         
         if(res==CURLE_OK){
             //Initialize JSON document to receive results of POST request
             rapidjson::Document aDoc;
             aDoc.Parse<0>(s.ptr);
             
             //Parse JSON response
             ...
         }
        curl_easy_cleanup(curl);
        free(s.ptr);
    } catch (const std::exception& error) {
        curl_easy_cleanup(curl);
        fclose(fd);
    }
    return 0;
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
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec lacinia elementum imperdiet. Aliquam quis dapibus lorem. Aenean lacinia condimentum sem non pellentesque. Quisque sodales sagittis orci vel accumsan. Morbi quis lectus sed magna fringilla feugiat. Donec id porttitor nunc. Curabitur pellentesque eros ut dolor dictum, sit amet consectetur massa consequat. Maecenas luctus pulvinar aliquet. Ut malesuada orci vel nunc molestie congue. Proin tempor sed nulla ut sodales.

Etiam dapibus mi sed tortor congue efficitur. Cras pharetra lacus et venenatis euismod. Integer vitae mattis risus. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam dignissim ipsum cursus dui rutrum, vel sagittis ligula iaculis. Curabitur ultricies libero et tortor vulputate, in cursus turpis dignissim. In vitae pharetra metus, ac posuere enim. Nulla non malesuada nisl, a dictum magna. Pellentesque malesuada dapibus mi, fringilla luctus lorem. Pellentesque est velit, tincidunt ut lacinia faucibus, pharetra quis turpis. Nulla aliquam non enim id posuere. Pellentesque elementum est eu orci varius, ut bibendum urna tempor. Aenean ac accumsan diam. Vestibulum dictum mattis posuere.

Vestibulum eget lectus efficitur, sollicitudin enim sed, eleifend augue. Pellentesque mattis odio vitae lacus feugiat maximus. Cras id rutrum augue. Donec ut pulvinar eros. Maecenas malesuada magna sit amet nisi dignissim, id accumsan augue imperdiet. Mauris pellentesque nunc sit amet libero efficitur tristique. Morbi in tellus leo. Donec finibus sapien orci. Morbi egestas ex vitae fermentum viverra. Etiam rhoncus faucibus tortor in rutrum. Sed id diam erat. Mauris euismod erat nec felis vestibulum, ac malesuada massa pellentesque. Pellentesque placerat odio mi, in consequat lacus sollicitudin a.


# User Provisioning Service

## Post TTS

```python
import json
import base64
import requests
​
ajala_url = "https://api.ajala.ai/v1/tts"
text_to_synthesize = "ògbójú ode ninu igbó irúnmanlẹ̀"
request_body = {"language":"yorubaNG",
                "speakerGender":"female",
                "source_text":text_to_synthesize,
                "API_KEY":<API_KEY>}
                
headers = {'Content-Type':'application/json'}
​
try:
    response = requests.post(ajala_url,json=request_body,headers=headers)
except Exception as e:
    print(e)
else:
    synthesized_audio = json.load(response.decode('utf-8'))
    with open('synthesized_audio.wav','w') as f:
        f.write(base64.b64decode(synthesized_audio["data"]["sound_base64"]))
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
function callTTSAPI(apiURL){
    var XMLHttpRequest = require("xmlhttprequest").XMLHttpRequest;
    var Httpreq = new XMLHttpRequest();
    
    Httpreq.open("GET",apiURL,false);
    Httpreq.send(null);
    return Httpreq.responseText;
}
​
var ajalaURL = "http://api.ajala.ai/v1/tts"
var speakerGender = "male"
var language = "swahiliKen"
var text_to_synthesize = "Jina lako nani?"
var API_KEY = "API_KEY"
​
ajalaURL = ajalaURL + "?apikey=" + API_KEY + "&language="+language + "&context=" + context
console.log("ajalaURL:" + ajalaURL)
​
var jsonResponse = JSON.parse(callTTSAPI(ajalaURL));
console.log(jsonResponse.success)

```
```cpp
//Helper function
std::string replaceURLWhitespace(std::string aString){
    for(std::string::iterator it = aString.begin(); it!=aString.end(); ++it){
        if(*it==' '){
            *it='+';
        }
    }
    return aString;
}
​
int main(){
    std::string ajalaURL = "http://api.ajala.ai/v1/tts";
    
    //Kiswahili example
    std::string text_to_synthesize = "Jina lako nani?";
    std::string speakerGender, audioFormat, language, API_KEY, transcriptURL, postFields;
    
    speakerGender = "male";
    language = "swahiliKen";
    audioFormat = "wav";
    API_KEY = "XXXXXXXXXXXX";
    wavPath = "/path/to/save/audio/file/response/to/request/name.wav";
    
    text_to_synthesize = replaceWhitespaceForURL(text_to_synthesize);
    postFields = "&language=" + language + "&text=" + text_to_synthesize + "&gender=" + speakerGender + "&fmt=" + audioFormat + "&API_KEY=" + API_KEY;
    ajalaURL += postFields;
    
    CURL *curl;
    CURLcode res;
    
    curl_global_init(CURL_GLOBAL_ALL);
    curl = curl_easy_init();
    
    try:{
        struct string s;
        init_string(&s);
        
        curl_easy_setopt(curl,CURLOPT_URL, ajalaURL.c_str());
        curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION,writefunc);
        curl_easy_setopt(curl, CURLOPT_WRITEDATA, &s);
​
        res = curl_easy_perform(curl);
        
        if(res == CURLE_OK){
            rapidjson::Document aDoc;
            aDoc.Parse<0>(s.ptr);
            
            if(aDoc.IsObject() && aDoc.HasMember("success") && aDoc.HasMember("data") && aDoc["success"].IsTrue()){
                std::string decodedAudio = " ";
​
                if(aDoc["data"]["sound_base64"].IsString()){
                    //Decode audio to make playable
                    std::string encodedAudio = aDoc["data"]["sound_base64"].GetString();
                    decodedAudio = base64_decode(encodedAudio);
​
                    //Save decoded audio file & play
                    std::ofstream supp_info_output(wavPath, std::ios::out | std::ios::binary);
                    unsigned int stringLen = decodedAudio.length();
                    supp_info_output.write((char*)(&stringLen), sizeof(stringLen));
                    supp_info_output.write(decodedAudio.c_str(),decodedAudio.length());
                    supp_info_output.close();
                }
            }
        }
        free(s.ptr);
        curl_easy_cleanup(curl);
    } catch (const std::exception& error) {
        curl_easy_cleanup(curl);
    }
    return 0
}

```

> The above command returns JSON structured like this:

```json
{
  "account_sid": "yyyyyyyyyyyyy",
  "api_version":"v1",
  "date_created":"<UTC_Date>",
  "date_sent":"<UTC_Date>",
  "error_code": null,
  "status":"OK",
  "data": {
    "sound_base64": "UkaGlagha8js",
    "voice":"Yoruba Nigerian Male"
  }
}
```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec lacinia elementum imperdiet. Aliquam quis dapibus lorem. Aenean lacinia condimentum sem non pellentesque. Quisque sodales sagittis orci vel accumsan. Morbi quis lectus sed magna fringilla feugiat. Donec id porttitor nunc. Curabitur pellentesque eros ut dolor dictum, sit amet consectetur massa consequat. Maecenas luctus pulvinar aliquet. Ut malesuada orci vel nunc molestie congue. Proin tempor sed nulla ut sodales.

Etiam dapibus mi sed tortor congue efficitur. Cras pharetra lacus et venenatis euismod. Integer vitae mattis risus. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam dignissim ipsum cursus dui rutrum, vel sagittis ligula iaculis. Curabitur ultricies libero et tortor vulputate, in cursus turpis dignissim. In vitae pharetra metus, ac posuere enim. Nulla non malesuada nisl, a dictum magna. Pellentesque malesuada dapibus mi, fringilla luctus lorem. Pellentesque est velit, tincidunt ut lacinia faucibus, pharetra quis turpis. Nulla aliquam non enim id posuere. Pellentesque elementum est eu orci varius, ut bibendum urna tempor. Aenean ac accumsan diam. Vestibulum dictum mattis posuere.

Vestibulum eget lectus efficitur, sollicitudin enim sed, eleifend augue. Pellentesque mattis odio vitae lacus feugiat maximus. Cras id rutrum augue. Donec ut pulvinar eros. Maecenas malesuada magna sit amet nisi dignissim, id accumsan augue imperdiet. Mauris pellentesque nunc sit amet libero efficitur tristique. Morbi in tellus leo. Donec finibus sapien orci. Morbi egestas ex vitae fermentum viverra. Etiam rhoncus faucibus tortor in rutrum. Sed id diam erat. Mauris euismod erat nec felis vestibulum, ac malesuada massa pellentesque. Pellentesque placerat odio mi, in consequat lacus sollicitudin a.


