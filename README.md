# Quill Forms Make API Docs

## Request:

### URL:

- Client website (connection.website_url)

### Method:

- POST

### Headers:

- content-type: application/x-www-form-urlencoded
- accept: application/json

### Body:

- Content type is application/x-www-form-urlencoded
- Must contains `api_key` parameter for authentication (connection.api_key)
- Must contains `quillforms_make_action` parameter (See Actions Section below)

## Response:

### Status:

- 200 for success.
- 401 for unauthorized.
- 422 for unprocessable entity.
- other 4xx.

### Body:

- Content type is application/json
- json response contains:
  - `success`: boolean
  - `data`: array|object

## Actions:

### `test_authentication` :

Used to test the authentication (used at connection communication).

#### Request example:

- POST {connection.website_url}
- headers  
  `content-type: application/x-www-form-urlencoded`  
  `accept: application/json`
- body:  
  `api_key={connection.api_key}&quillforms_make_action=test_authentication`

#### Success response example:

- status: 200
- body:

```
{
    success: true,
    data: {
        "message": "Successful authentication."
    }
}
```

#### Error response example:

- status: 401
- body:

```
{
    success: false,
    body: {
        "message": "Invalid api key."
    }
}
```

### `subscribe` :

Used for attaching `NewFormEntry` webhook.

#### Request example:

- POST {connection.website_url}
- headers  
  `content-type: application/x-www-form-urlencoded`  
  `accept: application/json`
- body:  
  `api_key={connection.api_key}&quillforms_make_action=subscribe&form_id=1&webhook_url=https://hook.us1.make.com/xxxxxxxx`

### `unsubscribe` :

Used for detaching `NewFormEntry` webhook.

#### Request example:

- POST {connection.website_url}
- headers  
  `content-type: application/x-www-form-urlencoded`  
  `accept: application/json`
- body:  
  `api_key={connection.api_key}&quillforms_make_action=unsubscribe&form_id=1&webhook_id=xxxxxxxx`

### `get_forms` :

Used for getting available forms (`NewFormEntry` & `FormEntries` modules).

#### Request example:

- POST {connection.website_url}
- headers  
  `content-type: application/x-www-form-urlencoded`  
  `accept: application/json`
- body:  
  `api_key={connection.api_key}&quillforms_make_action=get_forms`

### `get_entries` :

Used for getting entries of a specific form (`FormEntries` module).

#### Request example:

- POST {connection.website_url}
- headers  
  `content-type: application/x-www-form-urlencoded`  
  `accept: application/json`
- body:  
  `api_key={connection.api_key}&quillforms_make_action=get_entries&form_id=1&page=1`

### `get_fields` :

Used for getting item `(entry)` interface of a specific form (`NewFormEntry` & `FormEntries` modules).

#### Request example:

- POST {connection.website_url}
- headers  
  `content-type: application/x-www-form-urlencoded`  
  `accept: application/json`
- body:  
  `api_key={connection.api_key}&quillforms_make_action=get_fields&form_id=1`
