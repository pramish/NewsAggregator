> **_NOTE:_**  Please note that the web app is not ready to create API Key. However, you can use Postman or any other REST client to create API Key.


# Create API Key

> **_NOTE:_**  Before creating an API key, you should create an account. Please follow the instructions in [Sign Up](./SignUp.md), [Account Verification](./AccountVerification.md), and [Sign In](./SignIn.md) to create an account and sign in.

```typescript
POST /api/v1/apikey
Headers: 
    Content-Type: application/json
    authorizationtoken: 'string'
```
Response
```typescript
// This is the response object
interface ICreateAPIKeyResponse {
    success: boolean;
    message: string;
    apiKeyData?: {
        apiKey: string;
    };
}
```

## Example response

### Success

```typescript
{
    "success": true,
    "message": "API Key created.",
    "apiKeyData": {
        "apiKey": "some api key"
    }
}
```
### When authorizationtoken is not passed

```typescript
{
    "message": "Authentication token expired",
    "isSuccess": false
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
  method: 'POST',
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

response = requests.post(api_url, headers=headers)

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

    req, err := http.NewRequest("POST", apiURL, nil)
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
