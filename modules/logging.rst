Python Logging
--------------

Python has some beautiful logging.
Here is my goto format:

.. code-block:: python
    :linenos:

    import logging
    logging.basicConfig(
        format="%(levelname)-7s | %(asctime)s | %(filename)12s:%(funcName)-12s | %(message)s",
        datefmt="%I:%M:%S %p %d/%m/%Y",
        level=logging.INFO,
    )


Killing individual loggers is quite nice
when you don't want to hear about there problems.

.. code-block:: python
    :linenos:

    import logging
    logger = logging.getLogger("module.submodule")
    logger.setLevel(logging.WARNING)


My goto bot setup

.. code-block:: python
    :linenos:

    logging.basicConfig(
        format="%(levelname)-7s | %(asctime)s | %(filename)12s:%(funcName)-12s | %(message)s",
        datefmt="%I:%M:%S %p %d/%m/%Y",
        level=logging.INFO,
    )
    gateway_logger = logging.getLogger("nextcord.gateway")
    gateway_logger.setLevel(logging.WARNING)
    client_logger = logging.getLogger("nextcord.client")
    client_logger.setLevel(logging.WARNING)
    http_logger = logging.getLogger("nextcord.http")
    http_logger.setLevel(logging.WARNING)