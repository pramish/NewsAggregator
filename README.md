# NewsAggregator

> **_NOTE:_**  Please note that the web app is not ready. However, you can use Postman or any other REST client.

List of APIs exposed

Before you can fetch news, you have to create an account.

<details>
  <summary>Create an account</summary>
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
</details>

After you've created your account, please verify your account and you'll be signed in

<details>
  <summary>Account verification</summary>
# Account Verification and Token Generation

```typescript
POST /auth/verify
Headers: Content-Type: application/json
Body: {
    "email": "string",
    "verifyCode": "number"
}
```
Response
```typescript
// This is the response object
interface IVerifyResponse {
    statusCode: number;
    isSuccess: boolean;
    message: string;
    token?: string;
}
```

## Example response

### Success

```typescript
{
 "statusCode": 200,

 "isSuccess": true,

 "message": "Successfully signed in."
}
```
### When email or verifyCode is not provided

```typescript
{
    "isSuccess": false, 
    "message": "Please provide required body params"
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

const apiUrl = "https://news-scraper-0fmx.onrender.com/api/v1/auth/verify";
const body = {
    email: "email@email.com",
    verifyCode: 1234
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

api_url = "https://news-scraper-0fmx.onrender.com/api/v1/auth/verify"
body = {
    "email": "email@email.com",
    "verifyCode": 1234
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
    apiURL := "https://news-scraper-0fmx.onrender.com/api/v1/auth/verify"
    body := []byte(`{"email":"email@email.com", "verifyCode":1234}`)

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
</details>

After you've verified your account, you can sign in and get your authentication token to get token to create API Key

<details>
  <summary>Sign In</summary>
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
</details>

After you've signed in, you can get your authentication token to create API Key

<details>
  <summary>Create API Key</summary>
# Create API Key

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
</details>

If you forgot your API Key, you can get it by signing in and retrieving your API Key.

<details>
  <summary>Get API Key</summary>
# Retrieve API Key 

```typescript
GET /api/v1/apikey
Headers: 
    Content-Type: application/json
    authorizationtoken: 'string'
```
Response
```typescript
// This is the response object
interface IRetrieveAPIKeyResponse {
    success: boolean;
    message: string;
    apiKeyData?: {
        apiKey: string;
        userId: string;
        createdAt: number;
        updatedAt: number;
    };
}
```

## Example response

### Success

```typescript
{
    "success": true,
    "message": "API Key retrieved",
    "apiKeyData": {
        "apiKey": "someAPIKey",
        "userId": "userId",
        "createdAt": 1708775942,
        "updatedAt": 1708775942
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
  method: 'GET',
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

response = requests.get(api_url, headers=headers)

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

    req, err := http.NewRequest("GET", apiURL, nil)
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

</details>

If you would like to delete your API Key.

<details>
  <summary>Delete API Key</summary>
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
</details>

If you want to update your API Key.

<details>
  <summary>Update API Key</summary>
# Update API Key

```typescript
PATCH /api/v1/apikey
Headers: 
    Content-Type: application/json
    authorizationtoken: 'string'
```
Response
```typescript
// This is the response object
interface IUpdateAPIKeyResponse {
    success: boolean;
    message: string;
}
```

## Example response

### Success

```typescript
{
    "success": true,
    "message": "API Key updated"
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
  method: 'PATCH',
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

response = requests.patch(api_url, headers=headers)

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

    req, err := http.NewRequest("PATCH", apiURL, nil)
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
</details>

Get news types

<details>
  <summary>Get News Types</summary>
# Get News Type

```typescript
GET /news-type
Headers: news_api_key: "API_KEY"
Content-Type: application/json
```
Response
```typescript
// This is the response object
interface INewsType {
    typeId: string;
    type: string;
}
```
```typescript
statusCode: number;
isSuccess: boolean;
message: string;
type: Array<INewsType>
```
## Example response

### Success

```typescript
{
	"statusCode": 200,

	"isSuccess": true,

	"message": "Successfully retrieved news type",

	"type":
            [
                {
                    "typeId": "f60391c2-eef6-451b-8609-f1ce39abf05b",
                    "type": "NSW News"
                },

                {
                    "typeId": "c8380049-fc85-487a-993b-c9815478eb00",
                    "type": "FIFA Women's World Cup™"
                },
            ]
}
```
### Empty News Type

```typescript
{
    "statusCode": 404,
    
    "isSuccess": false,
    
    "message": "No news type found"
}
```
### When an API key is not provided/incorrect

```typescript
{
    "statusCode": 403,

    "isSuccess": false,

    "message": "Forbidden"
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

const apiKey = "API_KEY";
const apiUrl = "https://news-scraper-0fmx.onrender.com/api/v1/news/news-type";

fetch(apiUrl, {
  method: 'GET',
  headers: {
    'news_api_key': apiKey,
    'Content-Type': 'application/json'
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```
#### Python
```bash
import requests

api_url = "https://news-scraper-0fmx.onrender.com/api/v1/news/news-type"
api_key = "API_KEY"

headers = {
    "news_api_key": api_key,
    "Content-Type": "application/json"
}

response = requests.get(api_url, headers=headers)

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
    apiURL := "https://news-scraper-0fmx.onrender.com/api/v1/news/news-type"
    apiKey := "API_KEY"

    req, err := http.NewRequest("GET", apiURL, nil)
    if err != nil {
        fmt.Println("Error creating request:", err)
        return
    }

    req.Header.Set("news_api_key", apiKey)
    req.Header.Set("Content-Type", "application/json")

    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        fmt.Println("Error sending request:", err)
        return
    }
    defer resp.Body.Close()

    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        fmt.Println("Error reading response:", err)
        return
    }
    
    fmt.Println(string(body))
}
```
</details>

# More APIs coming soon ...

Please get in touch with [Pramish Luitel](https://www.linkedin.com/in/pramish-luitel/) if you want to discuss further.

Happy Coding!!
