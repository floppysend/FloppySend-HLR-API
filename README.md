## FloppySend HLR API

FloppySend’s HLR API provides a way to send Network Queries to any mobile number globally. It allows you to view what mobile number (MSISDN) belongs to what operator in real-time and see if the number is active.

Request Types
 - GET: If the request is get method you need to append params as query string inside the params section
 - POST: If request is post method you need to append params as x-www-form-urlencoded inside the body of the request

```
https://api.floppy.ai/hlr
```
```
{
    X-api-key:"Your x-api-key" (string required)
    X-Secret-Hash:"Your x-secret-hash" 
    (string required if added from dashboard)
}
```
You can get your X-Api-Key And X-Secret-Hash from your [account setting](https://app.floppysend.com/) page in Api Keys section

#### Parameters
  | Parameter | Type | Required | Description |
  | --------- | ---- | -------- | ----------- |
  | Msisdn | String | Yes | number sending to |

#### HLR API Responses
```JSON
{
    "Result": "Success",
    "Datainfo": [
        {
            "Number": "{phone_number}",
            "Country": "{phone_number_country}",
            "Network": "{phone_number_network}",
            "Operator": "{phone_number_operator}",
            "Type": "{phone_type}",
            "ErrorText": "{error_text}",
            "ErrorCode": "{error_code}",
            "Status": "{status}",
            "MccMnc": "{MccMnc}",
            "IsPorted": "{true_or-false}",
            "IsRoaming": "{true_or-false}",
            "Date": "{checing_date}",
            "Cost": "{checking_cost}"
        }
    ]
}
```

#### HLR API Code Sample

You need to add your "X-Secret-Hash" in the header if you have one.

```PHP
//PHP

<?php

$curl = curl_init();
curl_setopt_array($curl, array(
        CURLOPT_URL => 'https://api.floppy.ai/hlr',
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => '',
        CURLOPT_MAXREDIRS => 10,
        CURLOPT_TIMEOUT => 0,
        CURLOPT_FOLLOWLOCATION => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => 'POST',
        CURLOPT_POSTFIELDS => 'Msisdn={phone_number}',
        CURLOPT_HTTPHEADER => array(
        'x-api-key: "Your x-api-key"',
        'Content-Type: application/x-www-form-urlencoded'
        ),
    ));
$response = curl_exec($curl);
curl_close($curl);
echo $response;
```

```ruby
//Ruby

require "uri"
require "net/http"
url = URI("https://api.floppy.ai/hlr")
https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true
request = Net::HTTP::Post.new(url)
request["x-api-key"] = "Your x-api-key"
request["Content-Type"] = "application/x-www-form-urlencoded"
request.body = "Msisdn={phone_number}"
response = https.request(request)
puts response.read_body
```

```Java
//JAVA

//The OkHttpClient is an external package, you need to install it before making the request, 
//And don't forget to add user permission for the internet inside "\MyApplication\app\src\main\AndroidManifest.xml"
//Also, you need to add required dependencies inside "MyApplication\app\build.gradle"

OkHttpClient client = new OkHttpClient().newBuilder()
.build();
MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType, "Msisdn={phone_number}");
Request request = new Request.Builder()
.url("https://api.floppy.ai/hlr")
.method("POST", body)
.addHeader("x-api-key", "Your x-api-key")
.addHeader("Content-Type", "application/x-www-form-urlencoded")
.build();
Response response = client.newCall(request).execute();
```

```C#
//C#

var client = new RestClient("https://api.floppy.ai/hlr");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("x-api-key", "Your x-api-key");
request.AddHeader("Content-Type", "application/x-www-form-urlencoded");
request.AddParameter("Msisdn", "{phone_number}");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```JavaScript
//NodeJs
//Make sure to import Axios and install npm packages before doing the request

var axios = require('axios');
var qs = require('qs');
var data = qs.stringify({
    'Msisdn': 'NUMBER'
});
var config = {
    method: 'post',
    url: 'https://api.floppy.ai/hlr',
    headers: {
        'x-api-key': 'YOUR-API-KEY',
        'Content-Type': 'application/x-www-form-urlencoded'
    },
    data: data
};

axios(config)
    .then(function (response) {
        console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
        console.log(error);
    });
```
