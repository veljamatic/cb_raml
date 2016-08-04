Management API is a REST API for managing content. Apps and websites depend on the structure of content, so every entity must comply to a specific entity type. Entities are represented as JSON data. The API can be securely accessed via HTTPS and will only be available to clients that are authenticated with an access token and have permissions for Management API. It shouldn't be used to massively deliver content to end users. For example, you shouldn't use the Management API to display blog posts on a web site or pull information into a mobile web app unless that app is meant for editing content.
## Talking to API
Management API is a HTTP API and whole communication is done over HTTP endpoints that handle requests to the backend. Every endpoint is RESTful, and common RESTful rules apply to Management API endpoints. Request and response payloads are always in JSON format and we are trying to follow JSON API specification.
## RESTful
Every resource in Management API can be accessed and managed in common RESTful API specification ways.
## Requests
TBD
## Responses
Every response coming from Management API is in JSON format. Root object of responses has 3 properties data, meta and links. Main payload is in data property, metadata about request is in meta property and links for resources and paging are in links property. Example:
```javascript
{
   "data":{
      "id":1,
      "type":"entity-type",
      "code":"page",
      "endpoint":"pages",
      "name":"Page",
      "localized":1,
      "created_at":"2016-04-07T15:31:00+0000",
      "updated_at":"2016-04-07T15:31:00+0000",
      "attribute_sets":[
         {
            "id":1,
            "type":"attribute-set",
            "links":{
               "self":"http://example.com/api/attribute-sets/1"
            }
         },
         {
            "id":8,
            "type":"attribute-set",
            "links":{
               "self":"http://example.com/api/attribute-sets/8"
            }
         }
      ],
      "workflow":{
         "id":2,
         "type":"workflow",
         "links":{
            "self":"http://example.com/api/workflows/2"
         }
      },
      "type":"entity-type",
      "links":{
         "self":"http://example.com/api/entity-types/1"
      }
   },
   "meta":{
      "id":"1",
      "include":[

      ]
   },
   "links":{
      "self":"http://example.com/api/entity-types/1"
   }
}
```
## Errors
Whenever something goes wrong with an API request, the server returns an error. Information about the error is indicated by an HTTP status code, with further details in the response body, which will be a JSON resource. Errors always have a message property which will be a short description of what went wrong. Finally, some errors resulting from bad input (such as validation errors) contain errors property. This property is structured data that indicates more precisely what was wrong with the input.
Types of errors:

|Code|Error|Description|
|---|---|---|
|500|Server Error|There is something wrong in backend.|
|400|Bad Request Error|Request is malformed or there are some inputs that server doesn’t know how to process.|
|401|Authentication Error|Client is not authenticated.|
|403|Authorization Error|Client is not authorized to perform requested action.|
|404|Not Found Error|The requested resource or endpoint doesn’t exist.|
|422|Validation Error|The request payload was a valid JSON, but something was wrong with the data. Check the error details.|

Error response body example:
```javascript
{
   "message":"422 Unprocessable Entity",
   "errors":{
      "entity":{
         "fields":{
            "title":[
               "This field is required."
            ]
         }
      }
   },
   "status_code":422
}
```
##Authentication
TBD

##Endpoints
Managing entities, entity types, workflows, etc. is done by many resources which are all available through Management API. In it every resource has its own endpoint where you can query, create, update or delete the resources. Here’s a list of endpoints:

| Endpoint | Description |
|---|---|
| `api/attributes`| Attribute definition resource|
| `api/attribute-sets`| Attribute set or entity type schema resource|
| `api/entity-types`| Entity type definition resource|
| `api/entities`| Entity resource|
| `api/locales`| Locale resource|
| `api/workflows`| Workflow definition resource|
| `api/workflow-points`| Workflow point or stage resource|
| `api/users`| User resource|
| `api/consumers`| Consumer or application resource|
