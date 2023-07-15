---
title: REST API
---

## Kiểm tra API sử dụng POST method

- Chỉnh sửa lại `url`, `headers`, `data`

```python
import requests

# set the API endpoint and headers
url = 'https://api.example.com/post'
headers = {'Content-type': 'application/json', 'Authorization': 'Bearer your_access_token'}

# set the data to be sent in the request
data = {'name': 'John Doe', 'email': 'johndoe@example.com'}

# send the POST request using the Requests library
response = requests.post(url, headers=headers, json=data)

# verify the response
print(response.status_code)
print(response.text)
```
