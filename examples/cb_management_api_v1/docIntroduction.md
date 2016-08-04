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