# SeetiTel API Endpoints

The SeetiTel API is a RESTful API, and is designed to use standardized resource URI's and HTTP verbs, with semantic HTTP error response codes to indicate API errors and state.

**All endpoints referenced have the following base: https://seeti.tel/api/v1/**


## Multiple Whistles & Search

### Recent Whistles

Returns whistles, from most to least recent.

#### Query

`GET whistles/{offset}`

Parameter  | Description
------------- | -------------
`offset`  | unique ID of the last result of the last set you got

#### Result
```JSON
[
  {
    "id": "2564",
    "created": "1428974705",
    "type": "1",
    "encrypted": false,
    "teaser": "This is an audio whistle."
  },
  {
    "id": "2565",
    "created": "1428974605",
    "type": "0",
    "encrypted": false,
    "teaser": "This is the first 40 characters of the whistle."
  }
]
```

The results are permitted to return fewer than the requested record count.

Parameter  | Description
------------- | -------------
`id`  | UUIDv4; unique whistle ID - can be used for direct lookup
`created`  | UNIX timestamp; creation date in UTC time WITH MILLISECONDS
`type`  | int; `0` for text, `1` for audio
`encrypted`  | bool; if true, indicates that the leak is encrypted with AES-128
`teaser`  | string; the first 40 characters of the whistle, or a sentence explaining that the whistle is audio-based.

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
Deletes all given whistles.

#### Query

`DELETE whistles`

(Requires Basic Auth)

#### Result
It will return 204 upon successful deletion.

## Status

### Get API status

Returns API uptime & DB status

#### Query

`GET status`

#### Result
{
    "infrastructure": "API has been running since Mon Apr 13 2015 23:10:37 GMT-0700 (Pacific Daylight Time)",
    "db": "DB is up with 0 rows."
}

This endpoint will return 200 if all is well, and 500 if there is an error.
