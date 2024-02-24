> **_NOTE:_**  Please note that the web app is not ready to create API Key. However, you can use Postman or any other REST client to create API Key.

```typescript
const BASE_URL = 'https://news-scraper-0fmx.onrender.com/api/v1/'
```

## Sign Up

```typescript
POST /auth/signup
Headers: 'Content-Type: application/json'
Body: {
    email: "string",
    isPublic: true
}
```
Response
```typescript
// This is the response object
interface ISignUpResponse {
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
    "message": "User created"
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

const apiUrl = "https://news-scraper-0fmx.onrender.com/api/v1/auth/signup";
const body = {
    "email": "email@email.com",
    "isPublic": true
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

api_url = "https://news-scraper-0fmx.onrender.com/api/v1/auth/signup"
body =  {
    "email": "email@email.com",
    "isPublic": true
};

headers = {
    "Content-Type": "application/json"
}

response = requests.post(api_url, headers=headers, data=json.dumps(body))

if response.status_code == 201:
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
    apiURL := "https://news-scraper-0fmx.onrender.com/api/v1/auth/signup"
    body := []byte(`{"email":"email@email.com", "isPublic":true}`)

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

### Now please proceed to verification of your account and sign in

[Verify your account](./AccountVerification.md)