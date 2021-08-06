<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

## toFile

Write output image data to a file.

If an explicit output format is not selected, it will be inferred from the extension,
with JPEG, PNG, WebP, TIFF, DZI, and libvips' V format supported.
Note that raw pixel data is only supported for buffer output.

A `Promise` is returned when `callback` is not provided.

### Parameters

-   `fileOut` **[String][1]** the path to write the image data to.
-   `callback` **[Function][2]?** called on completion with two arguments `(err, info)`.
    `info` contains the output image `format`, `size` (bytes), `width`, `height`,
    `channels` and `premultiplied` (indicating if premultiplication was used).
    When using a crop strategy also contains `cropOffsetLeft` and `cropOffsetTop`.

### Examples

```javascript
sharp(input)
  .toFile('output.png', (err, info) => { ... });
```

```javascript
sharp(input)
  .toFile('output.png')
  .then(info => { ... })
  .catch(err => { ... });
```

-   Throws **[Error][3]** Invalid parameters

Returns **[Promise][4]&lt;[Object][5]>** when no callback is provided

## toBuffer

Write output to a Buffer.
JPEG, PNG, WebP, TIFF and RAW output are supported.
By default, the format will match the input image, except GIF and SVG input which become PNG output.

`callback`, if present, gets three arguments `(err, data, info)` where:

-   `err` is an error, if any.
-   `data` is the output image data.
-   `info` contains the output image `format`, `size` (bytes), `width`, `height`,
    `channels` and `premultiplied` (indicating if premultiplication was used).
    When using a crop strategy also contains `cropOffsetLeft` and `cropOffsetTop`.

A `Promise` is returned when `callback` is not provided.

### Parameters

-   `options` **[Object][5]?** 
    -   `options.resolveWithObject` **[Boolean][6]?** Resolve the Promise with an Object containing `data` and `info` properties instead of resolving only with `data`.
-   `callback` **[Function][2]?** 

### Examples

```javascript
sharp(input)
  .toBuffer((err, data, info) => { ... });
```

```javascript
sharp(input)
  .toBuffer()
  .then(data => { ... })
  .catch(err => { ... });
```

```javascript
sharp(input)
  .toBuffer({ resolveWithObject: true })
  .then(({ data, info }) => { ... })
  .catch(err => { ... });
```

Returns **[Promise][4]&lt;[Buffer][7]>** when no callback is provided

## withMetadata

Include all metadata (EXIF, XMP, IPTC) from the input image in the output image.
The default behaviour, when `withMetadata` is not used, is to strip all metadata and convert to the device-independent sRGB colour space.
This will also convert to and add a web-friendly sRGB ICC profile.

### Parameters

-   `withMetadata` **[Object][5]?** 
    -   `withMetadata.orientation` **[Number][8]?** value between 1 and 8, used to update the EXIF `Orientation` tag.

### Examples

```javascript
sharp('input.jpg')
  .withMetadata()
  .toFile('output-with-metadata.jpg')
  .then(info => { ... });
```

-   Throws **[Error][3]** Invalid parameters

Returns **Sharp** 

## jpeg

Use these JPEG options for output image.

### Parameters

-   `options` **[Object][5]?** output options
    -   `options.quality` **[Number][8]** quality, integer 1-100 (optional, default `80`)
    -   `options.progressive` **[Boolean][6]** use progressive (interlace) scan (optional, default `false`)
    -   `options.chromaSubsampling` **[String][1]** set to '4:4:4' to prevent chroma subsampling when quality &lt;= 90 (optional, default `'4:2:0'`)
    -   `options.trellisQuantisation` **[Boolean][6]** apply trellis quantisation, requires mozjpeg (optional, default `false`)
    -   `options.overshootDeringing` **[Boolean][6]** apply overshoot deringing, requires mozjpeg (optional, default `false`)
    -   `options.optimiseScans` **[Boolean][6]** optimise progressive scans, forces progressive, requires mozjpeg (optional, default `false`)
    -   `options.optimizeScans` **[Boolean][6]** alternative spelling of optimiseScans (optional, default `false`)
    -   `options.optimiseCoding` **[Boolean][6]** optimise Huffman coding tables (optional, default `true`)
    -   `options.optimizeCoding` **[Boolean][6]** alternative spelling of optimiseCoding (optional, default `true`)
    -   `options.quantisationTable` **[Number][8]** quantization table to use, integer 0-8, requires mozjpeg (optional, default `0`)
    -   `options.quantizationTable` **[Number][8]** alternative spelling of quantisationTable (optional, default `0`)
    -   `options.force` **[Boolean][6]** force JPEG output, otherwise attempt to use input format (optional, default `true`)

### Examples

```javascript
// Convert any input to very high quality JPEG output
const data = await sharp(input)
  .jpeg({
    quality: 100,
    chromaSubsampling: '4:4:4'
  })
  .toBuffer();
```

-   Throws **[Error][3]** Invalid options

Returns **Sharp** 

## png

Use these PNG options for output image.

PNG output is always full colour at 8 or 16 bits per pixel.
Indexed PNG input at 1, 2 or 4 bits per pixel is converted to 8 bits per pixel.

### Parameters

-   `options` **[Object][5]?** 
    -   `options.progressive` **[Boolean][6]** use progressive (interlace) scan (optional, default `false`)
    -   `options.compressionLevel` **[Number][8]** zlib compression level, 0-9 (optional, default `9`)
    -   `options.adaptiveFiltering` **[Boolean][6]** use adaptive row filtering (optional, default `false`)
    -   `options.force` **[Boolean][6]** force PNG output, otherwise attempt to use input format (optional, default `true`)

### Examples

```javascript
// Convert any input to PNG output
const data = await sharp(input)
  .png()
  .toBuffer();
```

-   Throws **[Error][3]** Invalid options

Returns **Sharp** 

## webp

Use these WebP options for output image.

### Parameters

-   `options` **[Object][5]?** output options
    -   `options.quality` **[Number][8]** quality, integer 1-100 (optional, default `80`)
    -   `options.alphaQuality` **[Number][8]** quality of alpha layer, integer 0-100 (optional, default `100`)
    -   `options.lossless` **[Boolean][6]** use lossless compression mode (optional, default `false`)
    -   `options.nearLossless` **[Boolean][6]** use near_lossless compression mode (optional, default `false`)
    -   `options.force` **[Boolean][6]** force WebP output, otherwise attempt to use input format (optional, default `true`)

### Examples

```javascript
// Convert any input to lossless WebP output
const data = await sharp(input)
  .webp({ lossless: true })
  .toBuffer();
```

-   Throws **[Error][3]** Invalid options

Returns **Sharp** 

## tiff

Use these TIFF options for output image.

### Parameters

-   `options` **[Object][5]?** output options
    -   `options.quality` **[Number][8]** quality, integer 1-100 (optional, default `80`)
    -   `options.force` **[Boolean][6]** force TIFF output, otherwise attempt to use input format (optional, default `true`)
    -   `options.compression` **[Boolean][6]** compression options: lzw, deflate, jpeg, ccittfax4 (optional, default `'jpeg'`)
    -   `options.predictor` **[Boolean][6]** compression predictor options: none, horizontal, float (optional, default `'horizontal'`)
    -   `options.xres` **[Number][8]** horizontal resolution in pixels/mm (optional, default `1.0`)
    -   `options.yres` **[Number][8]** vertical resolution in pixels/mm (optional, default `1.0`)
    -   `options.squash` **[Boolean][6]** squash 8-bit images down to 1 bit (optional, default `false`)

### Examples

```javascript
// Convert SVG input to LZW-compressed, 1 bit per pixel TIFF output
sharp('input.svg')
  .tiff({
    compression: 'lzw',
    squash: true
  })
  .toFile('1-bpp-output.tiff')
  .then(info => { ... });
```

-   Throws **[Error][3]** Invalid options

Returns **Sharp** 

## raw

Force output to be raw, uncompressed uint8 pixel data.

### Examples

```javascript
// Extract raw RGB pixel data from JPEG input
const { data, info } = await sharp('input.jpg')
  .raw()
  .toBuffer({ resolveWithObject: true });
```

Returns **Sharp** 

## toFormat

Force output to a given format.

### Parameters

-   `format` **([String][1] \| [Object][5])** as a String or an Object with an 'id' attribute
-   `options` **[Object][5]** output options

### Examples

```javascript
// Convert any input to PNG output
const data = await sharp(input)
  .toFormat('png')
  .toBuffer();
```

-   Throws **[Error][3]** unsupported format or options

Returns **Sharp** 

## tile

Use tile-based deep zoom (image pyramid) output.
Set the format and options for tile images via the `toFormat`, `jpeg`, `png` or `webp` functions.
Use a `.zip` or `.szi` file extension with `toFile` to write to a compressed archive file format.

Warning: multiple sharp instances concurrently producing tile output can expose a possible race condition in some versions of libgsf.

### Parameters

-   `tile` **[Object][5]?** 
    -   `tile.size` **[Number][8]** tile size in pixels, a value between 1 and 8192. (optional, default `256`)
    -   `tile.overlap` **[Number][8]** tile overlap in pixels, a value between 0 and 8192. (optional, default `0`)
    -   `tile.angle` **[Number][8]** tile angle of rotation, must be a multiple of 90. (optional, default `0`)
    -   `tile.depth` **[String][1]?** how deep to make the pyramid, possible values are `onepixel`, `onetile` or `one`, default based on layout.
    -   `tile.container` **[String][1]** tile container, with value `fs` (filesystem) or `zip` (compressed file). (optional, default `'fs'`)
    -   `tile.layout` **[String][1]** filesystem layout, possible values are `dz`, `zoomify` or `google`. (optional, default `'dz'`)

### Examples

```javascript
sharp('input.tiff')
  .png()
  .tile({
    size: 512
  })
  .toFile('output.dz', function(err, info) {
    // output.dzi is the Deep Zoom XML definition
    // output_files contains 512x512 tiles grouped by zoom level
  });
```

-   Throws **[Error][3]** Invalid parameters

Returns **Sharp** 

[1]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[2]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function

[3]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error

[4]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise

[5]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[6]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[7]: https://nodejs.org/api/buffer.html

[8]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number