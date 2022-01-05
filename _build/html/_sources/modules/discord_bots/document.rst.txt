.. _my-reference-label:

Mongo Document
==============

The bread and butter on my bots. The ``Document`` class which can be found
`here <https://github.com/Skelmis/DPY-Bot-Base/blob/master/bot_base/db/document.py>`_

This document is written against ``_version = 9`` and make's no guarantees otherwise.

General setup (Outside of BotBase)
**********************************

.. code-block:: python
    :linenos:

    from bot_base.db import Document

    # Create a Mongo connection
    conn = AsyncIOMotorClient(connection_url)
    db = conn["my_database"]

    # This will create a Document called "config"
    # on the "my_database", Mongo database.
    config: Document = Document(db, "config")

General setup (Using BotBase)
**********************************

Want to know how to get autocomplete?
You will need to follow the ``Converters in BotBase``
section, just with or without converters.
Its the exact same process.

.. code-block:: python
    :linenos:

    from bot_base import BotBase

    bot = BotBase(
        command_prefix="t.",
        mongo_url=os.environ["MONGO_URL"], # Your connection url
        mongo_database_name="my_bot", # The name of the database to use
    )

    # ALL Documents are accessed via
    # self.db.document_name
    # So the previous example, this is how you would do it
    bot.db.config

    # Except it's automatically setup so you can start using it
    await bot.db.config.insert({"_id": ctx.guild.id, "prefix": "!"})


General Usage
*************

Theres more to it, for that I'd recommend checking out
the source code `here <https://github.com/Skelmis/DPY-Bot-Base/blob/master/bot_base/db/document.py>`_

.. code-block:: python
    :linenos:

    # ``document_id`` is either the `_id` field
    # or a Dictionary which acts as the filter

    # To fetch a document using its `_id` field
    # This can be None if that Document doesn't exist
    data = await config.find(document_id)


    # To insert data
    await config.insert({"_id": document_id, "prefix": "!", "guild_name": "testing"})
    data = await config.find(document_id)
    print(data) # -> {"_id": document_id, "prefix": "!", "guild_name": "testing"}

    # To update data, this overwrites EVERYTHING
    await config.update({"_id": document_id, "prefix": "?"})
    data = await config.find(document_id)
    print(data) # -> {"_id": document_id, "prefix": "?"}

    # The BETTER way to insert/update data is UPSERT
    # This will INSERT if required, otherwise it will UPDATE
    # This way you do not need to worry if it exists.
    await config.upsert({"_id": document_id, "prefix": "!", "guild_name": "testing"})
    data = await config.find(document_id)
    print(data) # -> {"_id": document_id, "prefix": "!", "guild_name": "testing"}


    # If you want to only update ONE field,
    # then you should use ``update_field_to`` to save
    # needing to fetch the data before
    await config.update_field_to(document_id, "prefix", ".")
    data = await config.find(document_id)
    print(data) # -> {"_id": document_id, "prefix": ".", "guild_name": "testing"}

    # This is equivalent and recommend over the following
    data = await config.find(document_id)
    data["prefix"] = "="
    await config.upsert(data)
    # Which achieves the same results, but double the db queries
    # If you need to update more fields, its up to you which you pick


    # Lets say we want to find ALL guilds with the prefix "?"
    # This will find and return a list of all guilds with
    # the field "prefix" as a "?", note this dict can be anything
    guilds = await config.find_many_by_custom({"prefix": "?"})


    # Delete all the data for a guild
    await config.delete(document_id)


    # Got a field which keeps count of something?
    # Increment (Or decrement by passing a negative)
    # the field using this method
    await config.increment(document_id, 5, "field_to_increase")


    # Remove ONE field
    await config.unset(document_id, "guild_name")


    # Get EVERYTHING in the database
    all_data = await config.get_all()

Converters
**********

The Document class features the ability to use converters,
so rather then get ``Dict``'s back you get class instances.

Dynamically created Document's will not use converters, if
you wish to use them then your ``MongoManager`` should have
them manually defined via a subclass and disabling the
built-in manager class.

.. code-block:: python
    :linenos:

    from typing import Any

    class Options:
        """
        Our database is:

        {
            "_id": Any,
            "guild_id": int
        }
        """
        def __init__(self, _id, guild_id):
            self._id: Any = _id
            self.guild_id: int = guild_id

Then when we wish to use it we can do:

.. code-block:: python
    :linenos:

    options_db: Document = Document(
        self.db, "options", converter=Options
    )

    my_option: Options = await options_db.find(document_id_here)
    print(f"This option is for {my_option.guild_id}")

Converters in BotBase
^^^^^^^^^^^^^^^^^^^^^

Defining converters on built-in documents is a tad tricky.

.. code-block:: python
    :linenos:

    # First create a subclass of MongoManager
    from bot_base.db import Document, MongoManager

    class AmbroseMongoManager(MongoManager):
        def __init__(self, connection_url, database_name):
            super().__init__(connection_url=connection_url, database_name=database_name)

            # Now define any documents you want explicit
            self.my_option: Document = Document(
                self.db, "options", converter=Options
            )

    # Now subclass BotBase
    from bot_base import BotBase

    class Ambrose(BotBase):
        def __init__(self, *args, **kwargs):
            # This gives us autocomplete!
            self.db: AmbroseMongoManager = AmbroseMongoManager(os.environ["MONGO_URL"])

            # leave_db means BotBase won't override our database
            super().__init__(*args, **kwargs, leave_db=True)


    # Now we can use it!
    bot = Ambrose(
        command_prefix="t.",
        mongo_url=os.environ["MONGO_URL"], # Your connection url
        mongo_database_name="my_bot", # The name of the database to use
    )

    bot.db.options....