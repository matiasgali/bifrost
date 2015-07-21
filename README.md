jQuery Bifröst
==============

A [jQuery Ajax transport](//api.jquery.com/jQuery.ajaxTransport) that uses
the *hidden iframe technique* to make **asynchronous requests**, allowing to
send both *files* and *data* even from browsers that don't support *FormData*,
the *File API* or *XMLHttpRequest* at all.

*(1.3kb minified and gzipped)*


How to use it
-------------

1.  Load the required files, **jquery.js** and **jquery.bifrost.js**.

2.  Make a regular [$.ajax()](//api.jquery.com/jQuery.ajax/) request
    setting the proper *dataType*:

    ```javascript
    $.ajax({
      url: 'path/to/asgard',
      type: 'POST',
      dataType: 'iframe json',
      data: { title: 'Lorem ipsum', description: 'Some data...' },
      fileInputs: $('input[type="file"]')
    }).done(function(data){
      console.log(data);
    }).fail(function(){
      console.log('Request failed!');
    });
    ```

    The **dataType** sets the transport to use (**iframe**) and the type of
    data to expect (**json** in this case), separated by just one space.

    To send **files** you need to set the *fileInputs* option (optional) with
    the file inputs that contain the files to send.

3.  Enjoy life! That's it, you are using a *hidden iframe* instead of
    *XMLHttpRequest*.

4.  This plugin is capable of sending some additional meta data (which are normally
    sent as headers) inside body and as part of multipart form data. This behaviour
    is disabled per default because if your server side implementation is not 
    flexible enough to accept those additional meta data (like Amazon S3 is not),
    it will be rejected. If you need those set the additional `sendMeta` option
    to `true` in setup.

Testing
-------

There is a built-in set of [QUnit](//qunitjs.com/) tests that you can run on
any browser you want to make sure it's properly supported.

The [tests](tests) depend on [Jaqen](//www.npmjs.org/package/jaqen), a minimal
testing server that allows to easily emulate APIs by setting the desired
responses on the very requests.

See the [testing doc page] (tests/TESTING.md) for more information.


Acknowledgments
---------------
This *transport* is heavily inspired by this two projects:
[jQuery Iframe Transport](//github.com/cmlenz/jquery-iframe-transport) and the
[Iframe Transport from jQuery File Upload](
//github.com/blueimp/jQuery-File-Upload/blob/master/js/jquery.iframe-transport.js).

The reasons for yet another implementation are that the first one needs a
textarea within the response to work properly, the second one isn't a separately
manteined project, and both have good features that are missing in the other.

This implementation aims to get the best out of both and to add some
improvements where possible.


Why the name?
-------------
The name is an analogy to the Norse mythology where the Bifröst is a magic
bridge between Midgard (abode of mankind) and Asgard, the realm of the gods.

In this context the iframe is an almost magic fallback bridge between browser
and server to send files and data asynchronously when otherwise unsupported.


Contributing
------------
Anyone is welcomed and encouraged to open up issues and report bugs. You may
make pull requests (in a feature branch) if you want but keep in mind that the
main goal here is to keep it simple.
