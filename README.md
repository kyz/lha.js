# lha.js
List and unpack LhA archives in the browser

    LHA.readFromURL("my_files/foo.lha", function (entries) {
         for (var e in entries) {
             var entry = entries[e];
             var name  = entry.name;         // full path and filename
             var data  = LHA.unpack(entry);  // unpacked data as Uint8Array
         }
    })

This Javascript library lets you unpack **[LhA files](https://en.wikipedia.org/wiki/LHA_(file_format))** in the browser.

LhA files (also known as LHarc files or LZH files) are popular in Japan, and are the standard archive format for [Aminet](http://aminet.net/), the world's largest collection of Amiga software.

## API Reference

<a name="readFromURL" href="#readFromURL">#</a> LHA.<b>readFromURL</b>(<i>url</i>, <i>callback</i>)

Gets a URL using `XMLHttpRequest` and parses the response as an LhA archive. The callback is called with an array of entries, one for each entry in the archive.

Each entry has these fields:

* <b>name:</b> the full path and filename
* <b>packMethod:</b> the method used to compress the file, e.g. `-lh1-`, `-lh5-`. The value `-lhd-` means this entry is a directory rather than a file
* <b>packedLength:</b> the compressed file size
* <b>length:</b> the uncompressed file size
* <b>lastModified:</b> a `Date` of when the file was last modified
* <b>comment:</b> an optional comment for the file

<a name="read" href="#read">#</a> LHA.<b>read</b>(<i>data</i>)

Parses the provided `Uint8Array` as an LhA archive and returns an array of entries, one for each entry in the archive. Each entry has the same fields as described above.

<a name="unpack" href="#unpack">#</a> LHA.<b>unpack</b>(<i>entry</i>)

Unpacks a file and returns its uncompressed data as a `Uint8Array`. If this is a text file, you can convert it back a a string with `String.fromCharCode` or `TextDecoder`.
