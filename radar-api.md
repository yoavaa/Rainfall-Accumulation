# radar-api

the radar api exposes radar historic data that accomolates over time, starting at `202512132000`
data is stored per 5 minutes and indexed using the format `202512132000` which is 
`{year}{month}{day}{hour}{minute}`.

the API automatically uploads images every hour, and exposes the `import_next_image` to upload 
the next images one at a time.

All the API methods support CORS and can be accessed directly by an HTML page.

The api exposes a few operations:

## get images

gets a list of images for a timeframe.

example
```
https://yoav68.wixstudio.com/radar/_functions/images_time_range?fromTime=202512180100&toTime=202512180200
```

returns
```
[
    {"_id":"202512180100","url":"https://static.wixstatic.com/media/c569b3_30d909359be0473881093a297a338810~mv2.png"},
    {"_id":"202512180105","url":"https://static.wixstatic.com/media/c569b3_fae17aa0426e4630961ceeb3e707e5cf~mv2.png"},
    {"_id":"202512180110","url":"https://static.wixstatic.com/media/c569b3_305188a4d437406ba2be63fbacef54c2~mv2.png"},
    {"_id":"202512180115","url":"", status: 'no-image'},
    {"_id":"202512180120","url":"https://static.wixstatic.com/media/c569b3_74a909ebfbc940c4b96d7ab741ab605a~mv2.png"},
    {"_id":"202512180125","url":"https://static.wixstatic.com/media/c569b3_b7334f785389438b8dd655e4ae69fc4d~mv2.png"},
    {"_id":"202512180130","url":"https://static.wixstatic.com/media/c569b3_309f0e4aade6434287a04b0a60876b0a~mv2.png"},
    {"_id":"202512180135","url":"https://static.wixstatic.com/media/c569b3_8997f7ee6f8448a386ea17fc7362fa2b~mv2.png"},
    {"_id":"202512180140","url":"https://static.wixstatic.com/media/c569b3_6bb628425ea44a0282330497ba354090~mv2.png"},
    {"_id":"202512180145","url":"https://static.wixstatic.com/media/c569b3_994dd4aef008495daf83b27a7c042312~mv2.png"},
    {"_id":"202512180150","url":"https://static.wixstatic.com/media/c569b3_4ce1e4b1fcd54552a4ce7dd51d2e6bb6~mv2.png"},
    {"_id":"202512180155","url":"https://static.wixstatic.com/media/c569b3_8de49f2f09e5435bb0b01e46e4e5ba44~mv2.png"}]
```

* The API can retrieve up to 300 images per request
* images may be missing for specific time frames, indicated with `status: 'no-image'`
* the images themselves are available in the provided urls

## get time range

returns the minimum and maximum timestamp for which we have data

```
https://yoav68.wixstudio.com/radar/_functions/time_range
```

returns 
```
{"start":"202512132000","end":"202512191225"}
```
## get import next image

The api triggers an update to import new radar image, the next after the end time from get time range.
```
https://yoav68.wixstudio.com/radar/_functions/import_next_image
```

returns
```
{"status":"ok","_id":"202512192320","url":"https://static.wixstatic.com/media/bf20c6_f556630a5709479285281a930853a606~mv2.png"}
```

or, if the end time is up to date
```
{"status":"no-image-to-import","_id":"202512192320",}
```

## get import prior image

The api triggers the import of the image before the first
```
https://yoav68.wixstudio.com/radar/_functions/import_prior_image
```




