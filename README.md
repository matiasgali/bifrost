jQuery Bifröst
==============

[![NPM](https://nodei.co/npm/jquery-bifrost.png?mini=true)](https://npmjs.org/package/jquery-bifrost)

A [jQuery Ajax transport](//api.jquery.com/jQuery.ajaxTransport) that uses
the *hidden iframe technique* to make **asynchronous requests**, allowing to
send both *files* and *data* even from browsers that don't support *FormData*,
the *File API* or *XMLHttpRequest* at all.

*(1.3kb minified and gzipped)*


Setup
-----

1.  Load the required files, **jquery.js** and **jquery.bifrost.js**.

2.  Make a regular [$.ajax()](//api.jquery.com/jQuery.ajax/) request
    setting the proper `dataType`:

    ```javascript
    $.ajax({
      url: 'path/to/asgard',
      method: 'POST',
      dataType: 'iframe json',
      data: { title: 'Lorem ipsum', description: 'Some data...' },
      fileInputs: $('input[type="file"]')
    }).done(function(data){
      console.log(data);
    }).fail(function(){
      console.log('Request failed!');
    });
    ```

    **Special options**:

    - `dataType`: sets the transport to use (*iframe*) and the type of data
    to expect (*json* in this case), separated by **only one space**.

    - `fileInputs` (optional): allows to send/upload files, it takes
    the **file inputs** containing the files to be sent.


3.  Enjoy! That's it, you are now using a *hidden iframe* instead of
    *XMLHttpRequest*.


Headers
-------

When using an iframe is not possible to set custom headers, so additional
headers are appended as metadata to the data object and are sent as part
of the request body or the URL query as appropriate.

By default the plugin adds the following metadata to help identify
and process the request:

- `X-Requested-With`: set to "IFrame".
- `Accept`: depends on the `dataType` and `accepts` options
(see [jQuery.ajax](https://api.jquery.com/jQuery.ajax)).
- `_method`: if the `method` option (or `type` for jQuery prior to 1.9.0) is
other than *GET* or *POST* (*DELETE*, *PUT*, *PATCH*, etc.) the request's
method is changed to *POST* and `_method` holds the original method.

Custom headers set in the `headers` option will also be appended as metadata
and overwrite the built-in ones.

If for any reason you need to keep the data object clean (no additional data),
just set the `headers` option to `false`. No headers/metadata will be appended.


Testing
-------

There is a built-in set of [QUnit](//qunitjs.com/) tests that you can run on
any browser you want to make sure it's properly supported.

The [tests](tests) depend on [Jaqen](//www.npmjs.org/package/jaqen), a minimal
testing server that allows to easily emulate APIs by setting the desired
responses on the very requests.

See the [testing doc page](tests/TESTING.md) for more information.


Acknowledgments
---------------
This *transport* is heavily inspired by this two projects:
[jQuery Iframe Transport](//github.com/cmlenz/jquery-iframe-transport) and the
[Iframe Transport from jQuery File Upload](
//github.com/blueimp/jQuery-File-Upload/blob/master/js/jquery.iframe-transport.js).

The reasons for yet another implementation are that the first one needs a
textarea within the response to work properly, the second one isn't a separately
maintained project, and both have good features that are missing in the other.

This implementation aims to get the best out of both and to add some
improvements where possible.


Why the name?
-------------
The name is an analogy to the Norse mythology where the Bifröst is a magic
bridge between Midgard (abode of mankind) and Asgard (the realm of the gods).

In this context the iframe is an almost magic fallback bridge between browser
and server to send files and data asynchronously when otherwise unsupported.


Contributing
------------
Anyone is welcomed and encouraged to open up issues and report bugs. You may
make pull requests (in a feature branch) if you want but keep in mind that the
main goal here is to keep it simple.
