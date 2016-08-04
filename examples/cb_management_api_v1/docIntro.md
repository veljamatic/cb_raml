#Introduction
##Build Apps & Websites with CookBook
CookBook enables you to build apps and websites without thinking about content management. Write your software in a technology that you are most comfortable with and integrate it easily with CookBook backend using our JSON API. Simply define, edit and publish your content in a CookBook administration panel or with our Management API, use the SDK to query and fetch content from our Delivery API, and display it into your app seamlessly.
##The APIs
CookBook takes an API-first approach to content management, offering REST APIs for working with your content. Each of these APIs serve a different purpose, so which one to use depends on what you want to do:

- If you're retrieving content to display to users in an app or website, you want to use the Delivery API. Delivery API is a read-only API for delivering content from our backend to apps, websites and other media. Content is delivered as JSON data.

- If you want to programmatically create or update content items, you want to use the Management API. Management API is a read-write API for managing your content and you can use it to build custom editing experiences or integrate with other backend systems. In fact, our administration panel is built on top of this API.

- Finally, when retrieving images stored in CookBook you can apply various transforms to images by appending query parameters to the URL, so we refer to this as our Images API. With the Images API you can resize and crop images, or convert them to different formats. Using our backend for these transformations lets you upload high-quality assets, and deliver exactly what your app needs.

##Managing your content with CookBook
You can entirely manage your content model and content entries over Management API. Our intuitive and easy to use administration panel helps developers and publishers to manage content by offering modern web user interface with nice looking forms for entries and tools for uploading assets, writing HTML or markdown text, pinpointing locations, defining content relations or browsing and filtering content.
##Localization
Localization allows you to add multiple versions of your content in different languages. You can have as many locales as you need. We have built CookBook with localization in mind, you can choose which data you want to be localized on every level and easily manage your content translations with specific endpoints and API filtering.
##Custom Workflows
Every organizations has its own process for content creation and management. We didn’t want to impose any predefined workflow, with CookBook you have the freedom to adapt your software to the organization that’s using it not the other way round. By creating your own workflow you are free to define stages of your content and the content transition rules. By combining different stages, their visibility in API and user permissions you have a powerful tool to tighten your process and make it mistake free.
##Webhooks
Webhooks automatically send data to the URL of your choice whenever content is edited in your CookBook backend. For example, this can be used to trigger a static site rebuild, notify your team on Slack™ or even create a row in your Google Drive spreadsheet when content has been changed.
##Users, Consumers, Roles, Permissions
To get content or store data in CookBook app should first authenticate and have permission to complete the desired action. CookBook uses OAuth 1.0a protocol for authentication process and we are working on enabling OAuth 2.0 in near future. We support one legged, two legged, three legged and X-auth variations of OAuth 1.0, though not on the same consumer. Users can have different roles with different permissions. At this moment permissions and roles are at simple level, mostly predefined, but we are working on new version of authentication and authorization system that will enable very granular definition of user scopes.
#Data concept
CookBook takes a very flexible approach to content definition, there are no predefined structures for pages, blog posts etc. You are free to define content model by your needs. Content data structure and rules in CookBook are defined with entity types and attributes, each entity type represents one resource (projects, pages, articles, books, clients). Resource structure and data bits are described with sets of attributes. Attributes represent fields ( or columns in relational database context) with name, data type, and other metadata like validation for example.

Individual pieces of data or content entries are stored as entities or assets. Entity represents one resource of one entity type and assets are used for storing binary data like images or videos.
#Management API
Management API is a REST API for managing content. Apps and websites depend on the structure of content, so every entity must comply to a specific entity type. Entities are represented as JSON data. The API can be securely accessed via HTTPS and will only be available to clients that are authenticated with an access token and have permissions for Management API. It shouldn't be used to massively deliver content to end users. For example, you shouldn't use the Management API to display blog posts on a web site or pull information into a mobile web app unless that app is meant for editing content.
##Talking to API
Management API is a HTTP API and whole communication is done over HTTP endpoints that handle requests to the backend. Every endpoint is RESTful, and common RESTful rules apply to Management API endpoints. Request and response payloads are always in JSON format and we are trying to follow JSON API specification.
##RESTful
Every resource in Management API can be accessed and managed in common RESTful API specification ways.
##Requests
TBD
##Responses
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
##Errors
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

Authentication
TBD

Endpoints
Managing entities, entity types, workflows, etc. is done by many resources which are all available through Management API. In it every resource has its own endpoint where you can query, create, update or delete the resources. Here’s a list of endpoints:

|Endpoint              | Description                                  |
|----------            |-------------                                 |
|`api/attributes`      |Attribute definition resource                 |
|`api/attribute-sets`  |Attribute set or entity type schema resource  |
|`api/entity-types`    |Entity type definition resource               |
|`api/entities`        |Entity resource                               |
|`api/locales`         |Locale resource                               |
|`api/workflows`       |Workflow definition resource                  |
|`api/workflow-points` |Workflow point or stage resource              |
|`api/users`           |User resource                                 |
|`api/consumers`       |Consumer or application resource              |

