# Sign In

```typescript
POST /auth/signin
Headers: Content-Type: application/json
Body: {
    "email": "string"
}
```
Response
```typescript
// This is the response object
interface ISignInResponse {
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

 "message": "Verification code has been sent."
}
```
### When email is not provided

```typescript
{
    "isSuccess": false,

    "message": "Please provide email"
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

const apiUrl = "https://news-scraper-0fmx.onrender.com/api/v1/auth/signin";
const body = {
    "email": "email@email.com"
};

fetch(apiUrl, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(body)
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```
#### Python
```bash
import requests
import json

api_url = "https://news-scraper-0fmx.onrender.com/api/v1/auth/signin"
body = {
    "email": "email@email.com"
}

headers = {
    "Content-Type": "application/json"
}

response = requests.post(api_url, headers=headers, data=json.dumps(body))

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
    "bytes"
)

func main() {
    apiURL := "https://news-scraper-0fmx.onrender.com/api/v1/auth/signin"
    body := []byte(`{"email":"email@email.com"}`)

    req, err := http.NewRequest("POST", apiURL, bytes.NewBuffer(body))
    if err != nil {
        fmt.Println("Error creating request:", err)
        return
    }

    req.Header.Set("Content-Type", "application/json")

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
