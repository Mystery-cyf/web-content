# Query

<div style="background: #f9f9f9; padding: 10px; border-radius: 5px; margin-bottom: 20px;">
    <div style="display: inline-block; background: #026aca; font-size: 0.6em; border-radius: 10px; color: #ffffff; padding: 0.3em 1em; line-height: 1.5em;">
        <span>POST</span>
    </div>
    <div style="display: inline-block; font-size: 0.85em; font-weight: 700; margin-left: 10px;">
        <span>http://${MILVUS_URI}/v2/vectordb/entities/query</span>
    </div>
</div>

This operation conducts a filtering on the scalar field with a specified boolean expression.

## Example

```shell
export MILVUS_URI="localhost:19530"

curl --location --request POST "http://${MILVUS_URI}/v2/vectordb/entities/query" \
--header "Content-Type: application/json" \
--data-raw '{
    "collectionName": "quick_setup",
    "filter": "color like \"red_%\"",
    "outputFields": [
        "color"
    ],
    "limit": 3
}'
```
Possible response is similar to the following.
```json
{
    "code": 0,
    "data": [
        {
            "color": "red_7025",
            "id": 1
        },
        {
            "color": "red_4794",
            "id": 4
        },
        {
            "color": "red_9392",
            "id": 6
        }
    ]
}
```

## Request

### Parameters

- Header parameters

    | Parameter        | Description                                                                               |
    |------------------|-------------------------------------------------------------------------------------------|
    | `Request-Timeout`  | **integer**<br/>The timeout duration for this operation.<br/>Setting this to None indicates that this operation timeouts when any response arrives or any error occurs.|
    | `Authorization`  | **string**<br/>The authentication token.|

- No query parameters required

- No path parameters required

### Request Body

```json
{
    "dbName": "string",
    "collectionName": "string",
    "filter": "string",
    "outputFields": [],
    "partitionNames": []
}
```

| Parameter        | Description                                                                               |
|------------------|-------------------------------------------------------------------------------------------|
| `dbName`  | __string__<br/>The name of the database.  |
| `collectionName` <span style="color:red">*</span> | __string__<br/>The name of the collection to which this operation applies.  |
| `filter` <span style="color:red">*</span> | __string__<br/>The filter used to find matches for the search.  |
| `outputFields` | __array__<br/>An array of fields to return along with the search results. |
| `outputFields[]`  | __string__<br/>  |
| `partitionNames` | __array__<br/>The name of the partitions to which this operation applies. |
| `partitionNames[]`  | __string__<br/>PartitionName  |

## Response

A list of dictionaries with each dictionary representing a queried entity.

### Response Bodies

- Response body if we process your request successfully

```json
{
    "code": "integer",
    "data": [
        {}
    ]
}
```

- Response body if we failed to process your request

```json
{
    "code": integer,
    "message": string
}
```

### Properties

The properties in the returned response are listed in the following table.

| Property | Description                                                                                                                                 |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------|
| `code`   | __integer__<br/>Indicates whether the request succeeds.<br/><ul><li>`0`: The request succeeds.</li><li>Others: Some error occurs.</li></ul> |
| `message`  | __string__<br/>Indicates the possible reason for the reported error. |
| `data` | __array__<br/> |
| `data[]` | __object__<br/> |
