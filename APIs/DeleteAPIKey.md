# Delete API Key

```typescript
DELETE /api/v1/apikey
Headers: 
    Content-Type: application/json
    authorizationtoken: 'string'
```
Response
```typescript
// This is the response object
interface IDeleteAPIKeyResponse {
    statusCode: number;
    isSuccess: boolean;
    message: string;
}
```

## Example response

### Success

```typescript
{
    "statusCode": 200,
    "isSuccess": true,
    "message": "API Key deleted"
}
```
### When authorizationtoken is not passed

```typescript
{
    "message": "Authentication token expired",
    "isSuccess": false
}
```
### When user does not have API key

```typescript
{
    "statusCode": 400,
    "isSuccess": false,
    "message": "API Key does not exists."
}
```
### When a server is not available

```typescript
{
    "statusCode": 500,

    "isSuccess": false,

    "message": "Internal Server Error"
}
```
### When a method is not allowed

```typescript
{
    "statusCode": 405,

    "isSuccess": false,

    "message": "Method not allowed"
}
```
### Examples on different languages
#### JavaScript
```bash
const fetch = require('node-fetch');

const apiUrl = "https://news-scraper-0fmx.onrender.com/api/v1/apikey";

fetch(apiUrl, {
  method: 'DELETE',
  headers: {
    'Content-Type': 'application/json',
    'authorizationtoken': 'sometoken'
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```
#### Python
```bash
import requests
import json

api_url = "https://news-scraper-0fmx.onrender.com/api/v1/apikey"

headers = {
    "Content-Type": "application/json",
    "authorizationtoken": "sometoken"
}

response = requests.delete(api_url, headers=headers)

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print(f"Error: {response.status_code}")
```
#### Go
```bash
package main

import (
    "fmt"
    "net/http"
    "io/ioutil"
)

func main() {
    apiURL := "https://news-scraper-0fmx.onrender.com/api/v1/apikey"

    req, err := http.NewRequest("DELETE", apiURL, nil)
    if err != nil {
        fmt.Println("Error creating request:", err)
        return
    }

    req.Header.Set("Content-Type", "application/json")
    req.Header.Set("authorizationtoken", "sometoken")

    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        fmt.Println("Error sending request:", err)
        return
    }
    defer resp.Body.Close()

    respBody, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        fmt.Println("Error reading response:", err)
        return
    }

    fmt.Println(string(respBody))
}
```