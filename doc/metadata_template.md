Metadata Templates
==================

Metadata that belongs to a file is grouped by templates. Templates allow the metadata service to provide a multitude of services, such as pre-defining sets of key:value pairs or schema enforcement on specific fields. 

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Create Metadata Template](#create-metadata-template)
- [Update Metadata Template](#update-metadata-template)
- [Get Metadata Template](#get-metadata-template)
  - [Get by scope and template key](#get-by-scope-and-template-key)
  - [Get by ID](#get-by-id)
- [Get Enterprise Metadata Templates](#get-enterprise-metadata-templates)
- [Delete a Metadata Template](#delete-a-metadata-template)
- [Execute Metadata Query](#execute-metadata-query)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Create Metadata Template
------------------------

The [`createMetadataTemplate(BoxAPIConnection api, String templateScope, String templateKey, String displayName, Boolean hidden, List<Field> fields)`][create-metadata-template]
method will create a metadata template schema.

You can create custom metadata fields that will be associated with the metadata template.

<!-- sample post_metadata_templates_schema -->
```java
MetadataTemplate.Field metadataField = new MetadataTemplate.Field();
metadataField.setType("string");
metadataField.setKey("text");
metadataField.setDisplayName("Text");

List<MetadataTemplate.Field> fields = new ArrayList<MetadataTemplate.Field>();
fields.add(metadataField);

MetadataTemplate template = MetadataTemplate.createMetadataTemplate(api, "enterprise", "CustomField", "Custom Field", false, fields);

final JsonObject jsonObject = new JsonObject();
jsonObject.add("text", "This is a test text");

Metadata metadata = new Metadata(jsonObject);
boxFile.createMetadata("CustomField", metadata);
```

[create-metadata-template]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#createMetadataTemplate-com.box.sdk.BoxAPIConnection-java.lang.String-java.lang.String-java.lang.String-boolean-java.util.List-

Update Metadata Template
------------------------

To update an existing metadata template, call the
[`updateMetadataTemplate(BoxAPIConnection api, String scope, String template, List<FieldOperation> fieldOperations)`][update-metadata-template]
method with the scope and key of the template, and the list of field operations to perform:

<!-- sample put_metadata_templates_id_id_schema -->
```java
List<MetadataTemplate.FieldOperation> updates = new ArrayList<MetadataTemplate.FieldOperation>();

String addCategoryFieldJSON = "{\"op\":\"addField\","\"data\":{"
    + "\"displayName\":\"Category\",\"key\":\"category\",\"hidden\":false,\"type\":\"string\"}}";
updates.add(new MetadataTemplate.FieldOperation(addCategoryFieldJSON));

String changeTemplateNameJSON = "{\"op\":\"editTemplate\",\"data\":{"
    + "\"displayName\":\"My Metadata\"}}";
updates.add(new MetadataTemplate.FieldOperation(changeTemplateNameJSON));

MetadataTemplate.updateMetadataTemplate(api, "enterprise", "myData", updates);
```

[update-metadata-template]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#updateMetadataTemplate-com.box.sdk.BoxAPIConnection-java.lang.String-java.lang.String-java.util.List-

Get Metadata Template
---------------------

### Get by scope and template key

The [`getMetadataTemplate(BoxAPIConnection api)`][get-metadata-template-1]
method will return information about default metadata schema.  Also,
[`getMetadataTemplate(BoxAPIConnection api, String templateKey)`][get-metadata-template-2] and
[`getMetadataTemplate(BoxAPIConnection api, String templateKey, String templateScope, String... fields)`][get-metadata-template-3]
can be used to set metadata template name, metadata scope and fields to retrieve.

<!-- sample get_metadata_templates_id_id_schema -->
```java
MetadataTemplate template = MetadataTemplate.getMetadataTemplate(api, "templateName");
```

[get-metadata-template-1]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getMetadataTemplate-com.box.sdk.BoxAPIConnection-
[get-metadata-template-2]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getMetadataTemplate-com.box.sdk.BoxAPIConnection-java.lang.String-
[get-metadata-template-3]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getMetadataTemplate-com.box.sdk.BoxAPIConnection-java.lang.String-java.lang.String-java.lang.String...-

### Get by ID

The static [`MetadataTemplate.getMetadataTemplateByID(BoxAPIConnection api, String templateID)`][get-template-by-id]
method will return a specific metadata template.

<!-- sample get_metadata_templates_id -->
```java
MetadataTemplate template = MetadataTemplate.getMetadataTemplateByID(api, "37c0204b-3fe1-4a32-b9da-f28e88f4c4c6");
```

[get-template-by-id]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getMetadataTemplateByID-com.box.sdk.BoxAPIConnection-java.lang.String-

Get Enterprise Metadata Templates
---------------------------------

Calling the static
[`getEnterpriseMetadataTemplates(BoxAPIConnection api, String... fields)`][get-enterprise-metadata-1]
will return an iterable that will page through all metadata templates within a user's enterprise.
Also, [`getEnterpriseMetadataTemplates(String templateScope, BoxAPIConnection api, String... fields)`][get-enterprise-metadata-2] and
[`getEnterpriseMetadataTemplates(String templateScope, int limit, BoxAPIConnection api, String... fields)`][get-enterprise-metadata-3]
can be used to set metadata scope, limit of items per single response.

<!-- sample get_metadata_templates_enterprise -->
```java
Iterable<MetadataTemplate> templates = MetadataTemplate.getEnterpriseMetadataTemplates(api);
for (MetadataTemplate templateInfo : templates) {
    // Do something with the metadata template.
}
```

To return the metadata templates available to all enterprises pass in the
`global` scope.

<!-- sample get_metadata_templates_global -->
```java
Iterable<MetadataTemplate> templates = MetadataTemplate.getEnterpriseMetadataTemplates('global', api);
for (MetadataTemplate templateInfo : templates) {
    // Do something with the metadata template.
}
```

[get-enterprise-metadata-1]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates-com.box.sdk.BoxAPIConnection-java.lang.String...-
[get-enterprise-metadata-2]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates-java.lang.String-com.box.sdk.BoxAPIConnection-java.lang.String...-
[get-enterprise-metadata-3]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates-java.lang.String-int-com.box.sdk.BoxAPIConnection-java.lang.String...-

Delete a Metadata Template
--------------------------

The [`deleteMetadataTemplate(BoxAPIConnection api, String scope, String template)`][delete-metadata-template]
method will remove a metadata template schema from an enterprise.

<!-- sample delete_metadata_templates_id_id_schema -->
```java
MetadataTemplate.deleteMetadataTemplate(api, "enterprise", "templateName");
```

[delete-metadata-template]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#deleteMetadataTemplate-com.box.sdk.BoxAPIConnection-java.lang.String-java.lang.String-

Execute Metadata Query
--------------------------

The [`executeMetadataQuery(BoxAPIConnection api, String from, String query, JsonObject queryParameters, String ancestorFolderId, String indexName, JsonArray orderBy, String ... fields)`][execute-metadata-query-with-fields] method queries files and folders based on their metadata and allows for fields to be passed in.

```java
String from = "enterprise_341532.test";
String query = "testfield = :arg";
String ancestorFolderId = "0";
JsonObject queryParameters = new JsonObject().add("arg", "test");
JsonArray orderBy = new JsonArray();
JsonObject primaryOrderBy = new JsonObject().add("field_key", "primarySortKey").add("direction", "asc");
JsonObject secondaryOrderBy = new JsonObject().add("field_key", "secondarySortKey").add("direction",
    "asc");
orderBy.add(primaryOrderBy).add(secondaryOrderBy);

BoxResourceIterable<BoxItem.Info> results = MetadataTemplate.executeMetadataQuery(api, from, query, queryParameters, ancestorFolderId, null, orderBy, "id", "name", "metadata.enterprise_341532.test");
for (BoxItem.Info itemInfo : results) {
    if (itemInfo instanceof BoxFile.Info) {
        BoxFile.Info fileInfo = (BoxFile.Info) itemInfo;
        // Do something with the file.

        // Example with metadata
        Metadata fileMetadata = fileInfo.getMetadata("test", "enterprise_341532");
        String customFieldValue = fileMetadata.getString("/customField");
        System.out.println(customFieldValue);

    } else if (itemInfo instanceof BoxFolder.Info) {
        BoxFolder.Info folderInfo = (BoxFolder.Info) itemInfo;
        // Do something with the folder.
    }
}
```

[execute-metadata-query]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#executeMetadataQuery-com.box.sdk.BoxAPIConnection-java.lang.String-java.lang.String-com.eclipsesource.json.JsonObject-java.lang.String-java.lang.String-com.eclipsesource.json.JsonArray-
[execute-metadata-query-with-fields]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html
