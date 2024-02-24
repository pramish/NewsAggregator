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