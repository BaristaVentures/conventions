# Status Codes

Common cases
--------------

Status codes for common scenarios:

* General:
        - `200 Ok`: If the user exists in the db, should return the session token.
        - `201 Created`: The resource was created.
        - `202 Accepted`: The request was processed and will be processed asap
        - `401 Unauthorized`: If the social access token is invalid (checked with Facebook or Google SDK).
        - `403 Forbidden`: The user might be authenticated but does not have the necessary permissions
        - `404 Not Found`: The resource identifier is invalid or not recognized by the server
        - `426`: If the client have an incompatible app version that needs to be updated
        - `412 Precondition Failed`: There is ho precondition guaranties to process the request (validations)

* Force update:
        - `426`: If the user have an app version that should be updated.

Force updates
-------------

Clients should send the next headers on every request to our api:

  * `bv-app-version`: `platform/typeApp/version/build` (**each value separated by `/`**) where:

    - `platform`: platform who make the request in lower case (ej: ios, android)
    - `typeApp`: app profile who make the request in lower case (ej: customer, driver, admin) if there are only one app could be mobile for mobile apps
    - `version`: current app version following semver standard (x.y.z)
    - `build` **(optional)** : current build version, could be number or letters

Force update errors will follow the same errors format and structure as every other endpoint of the API, taking into account the following fields need to be included:
    - error have to include a message to show in the alert
    - error have to include an URL for the app redirect

CORS errors
-----------

A `403 Forbidden`
CORS errors will follow the same error format and structure as every other endpoint of the API.

Error example:
```json
{
  "errors": [
    {
      "title": "Invalid request origin",
      "message": "Invalid origin, the request has been refused"
    }
  ]
}
```