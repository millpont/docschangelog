# Endpoints

## Endpoints

This section describes the available endpoints for the METI API. Each endpoint includes details on its usage, parameters, and examples to help you interact seamlessly with the API.

***

### Base URL

All API requests should start with the following base URL:

```http
https://api.meti.millpont.com/
```

***

### Endpoints Overview

#### Source Management

1. **GET /sources/?id={id}**: Retrieve details of a single source by its ID.
2. **POST /sources**: Create a new source using GeoJSON data.
3. **DELETE /sources/?id={id}**: Delete a source by its ID.

#### Authentication

4. **POST /token**: Generate an authentication token.

***

#### **GET /sources/**?id=**{id}**

Retrieve details of a source by its unique ID.

* **URL**: `https://api.meti.millpont.com/sources/`?id=`{id}`
* **Method**: GET
* **Headers**:
  * `Authorization: <token>`
* **Path Parameters**:
  * `{id}` (string): The unique ID of the source starting with 'src\_'.

**Example Request**

```bash
curl -X GET "https://api.meti.millpont.com/sources/?id=src_6ETupIGAbhjb7" \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

***

#### **POST /sources**

Create a new source using GeoJSON data.

* **URL**: `https://api.meti.millpont.com/sources`
* **Method**: POST
* **Headers**:
  * `Content-Type: application/json`
  * `Authorization: <token>`
* **Body**:
  * A valid GeoJSON FeatureCollection with:
    * **id** (string): Your internal ID (a SSID will also be assigned).
    * **properties** (object): Includes `start_at` and `end_at` dates in ISO 8601 format.
    * **geometry** (object): Must contain a valid Polygon.

**Example Request**

```bash
curl -X POST https://api.meti.millpont.com/sources \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..." \
-d '{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": "APITEST2",
      "properties": {
        "start_at": "2024-11-01T16:25:00.000Z",
        "end_at": "2024-11-10T16:25:00.000Z"
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [-95.99151831445964, 32.776695443574994],
            [-95.99151831445964, 32.77064374883592],
            [-95.98497521320726, 32.77064374883592],
            [-95.98497521320726, 32.776695443574994],
            [-95.99151831445964, 32.776695443574994]
          ]
        ]
      }
    }
  ]
}'
```

**Example Response**

```http
{
  "id": "src_6ETupIGAbhjb7",
  "message": "Source created successfully."
}
```

***

#### **DELETE /sources/**?id=**{id}**

Delete a source by its unique ID.

* **URL**: `https://api.meti.millpont.com/sources/`?id=`{id}`
* **Method**: DELETE
* **Headers**:
  * `Authorization: <token>`
* **Path Parameters**:
  * `{id}` (string): The unique ID of the source to delete.
* **Response**:
  * `message` (string): Confirmation of deletion.

**Example Request**

```bash
curl -X DELETE "https://api.meti.millpont.com/sources/?id=src_tJsijx0UmuGE9" \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

**Example Response**

```http
{
  "message": "Source deleted successfully."
}
```

***

### Authentication Endpoint

#### **POST /token**

Generate an authentication token.

* **URL**: `https://api.meti.millpont.com/token`
* **Method**: POST
* **Headers**:
  * `Content-Type: application/json`
* **Body Parameters**:
  * `email` (string): Your registered email address.
  * `password` (string): Your account password.
* **Response**:
  * `token` (string): The authentication token.
  * `expires_in` (integer): Token validity period in seconds.

**Example Request**

<pre class="language-bash"><code class="lang-bash"><strong>curl -X POST https://api.meti.millpont.com/token \
</strong>-H "Content-Type: application/json" \
-d '{
  "email": "name@domain.com",
  "password": "your_password"
}'
</code></pre>

***

### Error Handling

Refer to the **Error Handling** section for details on common errors and their solutions.
