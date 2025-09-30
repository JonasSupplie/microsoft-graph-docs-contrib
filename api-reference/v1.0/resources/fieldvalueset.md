---
author: spgraph-docs-team
ms.date: 09/11/2017
title: fieldValueSet resource type
ms.localizationpriority: medium
description: "Represents the column values in a listItem resource."
ms.subservice: sharepoint
doc_type: resourcePageType
---

# fieldValueSet resource type

Namespace: microsoft.graph

Represents the column values in a [listItem](listitem.md) resource.

## JSON representation

Here's a JSON representation of a **fieldValueSet** resource.
<!-- { "blockType": "resource", "@odata.type": "microsoft.graph.fieldValueSet",
      "optionalProperties": ["Author", "AuthorLookupId", "Name", "Color", "Quantity" ],
       "baseType": "microsoft.graph.entity", "openType": true } -->

```json
{
    "Author": "Brad Cleaver",
    "AuthorLookupId": "13",
    "Color": "Red",
    "Name": "Kangaroos and Wallabies: A Deep Dive",
    "Quantity": 350,
}
```

## Properties

Each user-visible field in the **listItem** is returned as a name-value pair in the **fieldValueSet**.
The example above is for a list that contains four columns, **Author**, **Name**, **Color**, and **Quantity**.

Lookup fields (like `Author` above) aren't returned by default.
Instead, the server returns a 'LookupId' field (like `AuthorLookupId` above) referencing the listItem targeted in the lookup.
The name of the 'LookupId' field is the original field name followed by `LookupId`.

Graph API does not support retrieving lookup columns for lists with more then 12 lookup columns.
If a list contains more than 12 lookup collumns, only the first 12 may be returned.
This limitation cannot be bypassed using pagination, filters, or $select.
While partial retrieval beyond this limit may occasionally work, it is not officially supported.

The server returns lookup values if your request includes a `select` statement with the fields you need.
Example:

```http
GET https://graph.microsoft.com/beta/sites/{site-id}/lists/{list-id}/items?expand=fields(select=Author,BookTitle,PageCount)
```

You may request up to 12 lookup fields in a single query, plus any number of regular fields.

<!-- {
  "type": "#page.annotation",
  "description": "",
  "keywords": "",
  "section": "documentation",
  "tocPath": "Resources/FieldValueSet"
} -->

