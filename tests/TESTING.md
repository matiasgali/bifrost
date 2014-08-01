How to test Bifröst
===================

Testing that the transport parses data properly requires some way to emulate or
fake requests and responses. Given that it uses an *iframe* there aren't much
alternatives other than a testing server.

The built-in tests are intended to run with
[Jaqen] (//www.npmjs.org/package/jaqen), which is a small testing server built
on node.js that allows to programmatically emulate responses and APIs.


Installing Jaqen
----------------

Once you have [node.js](//nodejs.org/download) on your system, run this in a
console to globally install Jaqen:

```bash
$ npm install -g jaqen
```

After installing you should be able to fire up an instance by typing *jaqen*:

```bash
$ jaqen
=> Jaqen is listening on port 9000.
=> Press Ctl+C to stop the server.
```


Running tests
-------------

**Important:** Browsers in general don't allow accessing cross-domain content
from iframes, so test files need to be served from the same domain as the fake
requests for the tests to run properly.

1.  Move to the project's root folder and run *jaqen* from there so it can serve
    Bifröst and the tests as static files from the same domain as the fake requests:

    ```bash
    $ cd bifrost
    $ jaqen
    => Jaqen is listening on port 9000.
    => Press Ctl+C to stop the server.
    ```

2.  Open up a browser and visit *http://localhost:9000/tests*.
    You should see the tests run and their results.

    If you run Jaqen in a different port you need to change Jaqen's address in
    *tests/index.html*.

Happy testing!
