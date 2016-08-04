## Attributes
Each attribute describes a single allowed field value of an entity. Every entity can only contain values in the fields defined by its entity type or attribute set, and the values of those fields must match the data type and rules defined in the attribute. Each data type corresponds to a JSON type, though there are more data types than JSON types.

### Data types

| Data type  | JSON type | Description | Example |
|---|---|---|---|
|`text`|String|Textual field with basic list of characters. Can be indexed by full-text search|`"This is a title of an article"`|
|`tags`|Array|A collection of textural values|`["red", "blue"]`|
|`integer`|Number|Number type without decimals.|`101`|
|`decimal`|Number|Number type with decimals.|`101.12`|
|`datetime`|String|Date / time in ISO 8601 format.|`"2015-11-06T09:45:27"`|
|`boolean`|Boolean|Flag - Yes/No, True/False|`true`|
|`select`|String|Choice from predefined values|`"type 1"`|
|`multiselect`|Array|Multipe choice from predefined values|`["column","widget"]`|
|`asset`|Object|A reference to an asset.|`{"id":5,"type":"file"}`|
|`assets`|Array|A reference to a collection of assets|`[{"id":5,"type":"file"},{"id":6,"type":"file"}]`|
|`relation`|Object|A reference to another entity|`{"id": 5,  "type": "entity"}`|
|`relations`|Array|A reference to collection of entities|`[  {    "id": 5,    "type": "entity"  },  {    "id": 6,    "type": "entity"  }]`|
|`location`|Object|A geographic location specified in latitude and longitude.|`{"lat":"52.5018616",  "lon":"13.4112619"}`|
|`locations`|Array|A collection of geographic locations|`[{"lat":"52.5018616","lon":"13.4112619"},{"lat":"52.5018616","lon":"13.4112619"}]`|

### Attribute properties

|Property|Type|Description|
|---|---|---|
|`code`|String|Unique identifier of attribute - readable slug (fields will be represented by this property)|
|`field_type`|String|Attribute data type|
|`admin_label`|String|Label for admin panel|
|`admin_notice`|String|Description or instructions for admin panel|
|`localized`|Boolean|Flag for localization of values for this attribute|
|`unique`|Boolean|Flag whether or not values should be unique|
|`required`|Boolean|Flag whether or not values should be required|
|`filterable`|Boolean|Is filtering of entities allowed by this attribute|
|`searchable`|Boolean|Flag whether the values will be indexed by full-text search. Only applicable to textual fields.|
|`default_value`|Mixed|Default value for this attribute|
|`data`|Object|Metadata that varies for each data type like special validation, input type...|
