# SeetiTel API Endpoints

The SeetiTel API is a RESTful API, and is designed to use standardized resource URI's and HTTP verbs, with semantic HTTP error response codes to indicate API errors and state.

**All endpoints referenced have the following base: https://seeti.tel/api/v1/**


## Multiple Whistles & Search

### Recent Whistles

Returns whistles, from most to least recent.

#### Query

`GET whistles/list/{offset}/{count}`

Parameter  | Description
------------- | -------------
`offset`  | number of records to skip before collecting
`count`  | number of recent whistles to retrieve, starting at the `offset`th record

#### Result
```JSON
[
  {
    "id": "2564",
    "created": "1428974705",
    "type": "1",
    "encrypted": 0,
    "teaser": "This is an audio whistle."
  },
  {
    "id": "2565",
    "created": "1428974605",
    "type": "0",
    "encrypted": 0,
    "teaser": "This is the first 40 characters of the whistle."
  }
]
```

The results are permitted to return fewer than the requested record count.

Parameter  | Description
------------- | -------------
`id`  | unique whistle ID; can be used for direct lookup
`created`  | UNIX timestamp of the creation date in UTC time
`type`  | `0` for text, `1` for audio
`encrypted`  | `1` or `0` to indicate that the leak is encrypted with AES-128
`teaser`  | the first 40 characters of the whistle, or a sentence explaining that the whistle is audio-based.

This endpoint will return HTTP 410 (`GONE`) if there are no more records to be displayed.

### Search 
Returns whistles that contain a given phrase, sorted from most to least recent.

#### Query

`GET whistles/search/{phrase}/{offset}/{count}`

Parameter  | Description
------------- | -------------
`phrase`  | string that will be searched for
`offset`  | number of records to skip before collecting
`count`  | number of recent whistles to retrieve, starting at the `offset`th record

#### Result

*See `Recent Whistles`*

## Single Whistles

### Get Single Whistle

Returns whistles, from most to least recent.

#### Query

`GET whistle/{id}`

Parameter  | Description
------------- | -------------
`id`  | unique ID of the desired whistle

#### Result
```JSON
{
    "id": "2564",
    "created": "1428974705",
    "type": "1",
    "encrypted": 0,
    "content": "This is an audio whistle."
}
```

Parameter  | Description
------------- | -------------
`id`  | unique whistle ID; can be used for direct lookup
`created`  | UNIX timestamp of the creation date in UTC time
`type`  | `audio` or `text`
`encrypted`  | `1` or `0` to indicate that the leak is encrypted with AES-128
`content`  | if the leak is text, the full text of the leak. If the leak is audio, this will be NULL.

This endpoint will return HTTP 404 if there is no such whistle.

### Get Whistle's Audio Content

Returns the MP3 of a given audio whistle

#### Query

`GET whistle/{id}/audio`

Parameter  | Description
------------- | -------------
`id`  | unique ID of the desired audio whistle

#### Result
`[binary MP3 data]`

This endpoint will return HTTP 404 if there is no such whistle, and 400 if the requested whistle is not an audio whistle.

### Delete Single Whistle
Deletes the given whistle, including audio, if applicable.

#### Query

`DELETE whistle/{id}/{secret}`

Parameter  | Description
------------- | -------------
`id`  | unique ID of the desired whistle
`secret` | secret password to allow deletion

#### Result
This endpoint will return HTTP 404 if there is no such whistle. It will return 204 upon successful deletion.

## Status

### Get API status

Returns API uptime

#### Query

`GET status/infrastructure`

#### Result
{
    "message": "API has been running since Mon Apr 13 2015 20:09:03 GMT-0700 (Pacific Daylight Time)"
}

This endpoint will return 200 if all is well.

### Get DB status

Returns DB rowcount

#### Query

`GET status/db`

#### Result
{
    "message": "DB is up with 94 rows"
}

This endpoint will return 200 if all is well, and 500 if there is an error.
