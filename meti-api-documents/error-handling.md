# Error Handling

## Error Handling

The METI API uses standard HTTP status codes to indicate the success or failure of API requests. This section explains the common errors you might encounter and how to resolve them.

***

### Common HTTP Status Codes

#### **2xx: Success**

* **200 OK**: The request was successful.
* **201 Created**: The resource was successfully created.

***

#### **4xx: Client Errors**

Errors in this category indicate issues with the request made by the client.

**400 Bad Request**

The server could not process the request due to invalid syntax or missing/invalid parameters.

* **Possible Causes**:
  * Invalid GeoJSON structure in a `POST /sources` request.
  * Missing required fields such as `email` or `password`.
* **How to Fix**:
  * Ensure all required parameters are included and properly formatted.

**401 Unauthorized**

Authentication is missing, invalid, or expired.

* **Possible Causes**:
  * Missing or incorrect `Authorization` header.
  * Expired token.
* **How to Fix**:
  * Include a valid `Authorization: Bearer <token>` header in the request.
  * If the token has expired, reauthenticate by calling `POST /token`.

**403 Forbidden**

The client is authenticated but does not have permission to access the resource.

* **Possible Causes**:
  * Attempting to delete or modify a resource without appropriate permissions.
* **How to Fix**:
  * Contact your administrator to ensure your account has the necessary permissions.

**404 Not Found**

The requested resource does not exist.

* **Possible Causes**:
  * Using an incorrect or nonexistent source ID in a `GET` or `DELETE` request.
* **How to Fix**:
  * Verify the resource ID and try again.

**422 Unprocessable Entity**

The server understands the request, but the data provided is invalid.

* **Possible Causes**:
  * GeoJSON polygons are invalid. Validation can be checked with [GeoJSONLint](https://geojsonlint.com/).
  * Dates are outside the acceptable range.
* **How to Fix**:
  * Validate the data before making the request, ensuring all inputs meet API requirements.

***

#### **5xx: Server Errors**

Errors in this category indicate issues on the server side. If you encounter these errors, contact the METI support team.

**500 Internal Server Error**

An unexpected error occurred on the server.

* **Possible Causes**:
  * API service issues or a bug in the system.
* **How to Fix**:
  * Retry the request after some time or contact support.

**503 Service Unavailable**

The API service is temporarily unavailable.

* **Possible Causes**:
  * Server maintenance or unexpected downtime.
* **How to Fix**:
  * Wait for a while and try again.

***

### Example Error Response

When an error occurs, the response typically includes:

* **status**: HTTP status code.
* **message**: A short description of the error.

#### Example Response for 400 Bad Request

```http
{
  "status": 400,
  "message": "Invalid GeoJSON structure. 'type' must be 'FeatureCollection'."
}
```

#### Example Response for 401 Unauthorized

```json
jsonCopy code{
  "status": 401,
  "message": "Token has expired. Please reauthenticate."
}
```

***

### Best Practices for Error Handling

1. **Validate Inputs**: Ensure all parameters meet the API's requirements before making a request.
2. **Handle Expired Tokens**: Implement token refresh logic to avoid interruptions (see [Authentication](authentication.md#steps-for-token-renewal)).
3. **Retry Logic**: For `5xx` errors, implement exponential backoff to retry requests after a delay.
4. **Monitor Responses**: Log error responses to identify recurring issues.

***

For additional support, contact the METI team at membership@millpont.com&#x20;
