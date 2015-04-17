# SeetiTel API Endpoints

The SeetiTel API is a RESTful API, and is designed to use standardized resource URI's and HTTP verbs, with semantic HTTP error response codes to indicate API errors and state.

**All endpoints referenced have the following base: https://seeti.tel/api/v1/**

## Quick Reference

Request  | Description
------------- | -------------
`GET /whistles/{offset}`  | Returns an array of 25 teasers, skipping `offset` rows
`GET /whistles/search/{phrase}`  | Returns an array of teasers that contain the given string (`phrase`)
`GET /whistle/{id}`  | Returns a full whistle with the given id (`id`)
`POST /whistle/demo/{type}`  | Creates a single test whistle with the given `type`
`GET /status`  | Returns a DB and API status report
`DELETE /whistles`  | Flushes all whistles.

**Whistle teaser format:**
```JSON
{
	"id": 2564,
	"created": 1428974705,
	"type": 1,
	"encrypted": false,
	"teaser": "This is an audio whistle."
}
```

**Full whistle format:**
```JSON
{
    "id": 2564,
    "created": 1428974705,
    "type": 1,
    "encrypted": false,
    "content": "/data/ba67de8f40abebd6.mp3"
}
```


## Multiple Whistles & Search

### Recent Whistles

Returns an array of 25 whistles, from most to least recent.

#### Query

`GET whistles/{offset}`

Parameter  | Description
------------- | -------------
`offset`  | number of results to skip

#### Result
```JSON
[
  {
    "id": 2564,
    "created": 1428974705,
    "type": 1,
    "encrypted": false,
    "teaser": "This is an audio whistle."
  },
  {
    "id": 2565,
    "created": 1428974605,
    "type": 0,
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
`type`  | int; `0` for text, `1` for audio, `2` for graphic
`encrypted`  | bool; if true, indicates that the leak is encrypted with AES-128
`teaser`  | string; the first 40 characters of the whistle, or a sentence explaining that the whistle is audio or image based.

This endpoint will return HTTP 410 (`GONE`) if there are no more records to be displayed.

### Search 
Returns whistles that contain a given phrase, sorted from most to least recent.

#### Query

`GET whistles/search/{phrase}`

Parameter  | Description
------------- | -------------
`phrase`  | string that will be searched for

#### Result

*See `Recent Whistles`*. Returns `410 GONE` if there are no matching records.

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
    "id": 2564,
    "created": 1428974705,
    "type": 1,
    "encrypted": false,
    "content": "/data/ba67de8f40abebd6.mp3"
}
```

Parameter  | Description
------------- | -------------
`id`  | UUIDv4; unique whistle ID - can be used for direct lookup
`created`  | UNIX timestamp; creation date in UTC time WITH MILLISECONDS
`type`  | int; `0` for text, `1` for audio, `2` for graphic
`encrypted`  | bool; if true, indicates that the leak is encrypted with AES-128
`content`  | if the leak is text, the full text of the leak. If the leak is audio or an image, this will be the URL that the data is accessible at.

This endpoint will return HTTP 404 if there is no such whistle.

## Maintenance

### Add demo row

Adds a demo row with dummy data

#### Query

`POST whistle/demo/{type}`

Parameter  | Description
------------- | -------------
`type`  | type of entry. `1` for unencrypted text, `2` for encrypted text with the key of 128 zeroes, `3` for graphic, `4` for audio

#### Result
```JSON
{
    "message": "Demo entry added."
}
```

This endpoint will return 200 if all is well, and 500 if there is an error.

### Delete Whistles
Deletes all given whistles.

#### Query

`DELETE whistles`

(Requires Basic Auth)

#### Result
It will return 204 upon successful deletion.

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
