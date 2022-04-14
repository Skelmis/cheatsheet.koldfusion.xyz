HTTP Header Info Leakage
========================

When we make requests to the web server,
the server returns various HTTP headers.
These headers can sometimes contain useful
information such as the webserver software
and possibly the programming/scripting language in use.

.. code-block:: shell
    :linenos:

    curl <url> -v