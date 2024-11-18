# Authentication

## Authentication

To interact with the METI API, you must first authenticate and obtain an access token. This token is required for all subsequent requests and ensures secure communication with the API.

### Generate Token

To generate an authentication token, make a POST request to the `/token` endpoint.

#### Request

* **URL**: `https://api.meti.millpont.com/token`
* **Method**: POST
* **Headers**:
  * `Content-Type: application/json`
* **Body Parameters**:
  * `email` (string): Your registered email address.
  * `password` (string): Your account password.

#### Response

* **token** (string): The authentication token.
* **expires\_in** (integer): Token validity period in seconds.

#### Example Request

```bash
curl -X POST https://api.meti.millpont.com/token \
-H "Content-Type: application/json" \
-d '{
  "email": "name@domain.com",
  "password": "your_password"
}'
```

#### Example Response

```http
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600
}
```

### Using the Token

Once you have obtained a token, include it in the `Authorization` header of all API requests. The format is:

```makefile
codeAuthorization: Bearer <token>
```

#### Example Request with Token

```bash
curl -X GET https://api.meti.millpont.com/sources \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

***

### Handling Token Expiration in Automated Workflows

For workflows requiring long-term or large-scale API access, ensure your system can handle token expiration and renewal automatically.

#### Steps for Token Renewal

1. **Track Token Expiration**:
   * Use the `expires_in` field from the token response to calculate the token's expiry time.
   * Store the token and its expiry timestamp securely.
2. **Check Token Validity Before Each Request**:
   * Compare the current time with the stored expiry timestamp.
   * If the token has expired or is close to expiring, retrieve a new token.
3. **Automate Token Retrieval**:
   * Implement logic to call the `/token` endpoint with your credentials when the token is invalid or expired.

#### Example Code Snippet (Python)

```python
pythonCopy codeimport time
import requests

# Token management
token = None
token_expiry = 0

def get_token():
    global token, token_expiry
    url = "https://api.meti.millpont.com/token"
    payload = {
        "email": "name@domain.com",
        "password": "your_password"
    }
    response = requests.post(url, json=payload)
    response_data = response.json()
    token = response_data["token"]
    token_expiry = time.time() + response_data["expires_in"]

def make_authenticated_request(endpoint, method="GET", data=None):
    global token, token_expiry
    if time.time() >= token_expiry:
        get_token()  # Refresh the token
    headers = {"Authorization": f"Bearer {token}"}
    url = f"https://api.meti.millpont.com/{endpoint}"
    if method == "GET":
        response = requests.get(url, headers=headers)
    elif method == "POST":
        response = requests.post(url, json=data, headers=headers)
    return response.json()

# Example usage
get_token()  # Get the token initially
response = make_authenticated_request("sources", method="GET")
print(response)
```

#### Benefits of Automation

* Prevents downtime caused by expired tokens.
* Ensures smooth and continuous API access for large-scale or time-sensitive operations.

***

### Token Expiry

Tokens are valid for the duration specified in the `expires_in` field of the response. If your token expires, you must request a new one by re-authenticating.

### Common Errors

* **401 Unauthorized**: This error occurs if the token is missing, invalid, or expired. Ensure you provide a valid token in the `Authorization` header.

***

By implementing automated token management, you can maintain uninterrupted API access, even for complex workflows.
