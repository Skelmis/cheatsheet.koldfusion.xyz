Bot Template
============

I created a bot template to suit my needs, find it `here <https://github.com/Skelmis/DPY-Bot-Base>`_

Features
--------

Database
********

There is a built-in database management system using Mongo.

This will dynamically add ``Documents``
for your usage as required, so no need to manually define them.

Read more about them here: :ref:`my-reference-label`

**Usage:**

.. code-block:: python
    :linenos:

    bot = BotBase(
        command_prefix="!",
        mongo_url=os.environ["MONGO_URL"],
        mongo_database_name="my_bot" # Optional, defaults to 'production'
    )

    ...
    guild_options = await bot.db.guild_options.find(ctx.guild.id)
    guild_options["prefix"] = "?"
    await bot.db.guild_options.upsert(guild_options)

    # For more usages, view the Document class linked before.

    # To create a backup of the collection, simply call
    await bot.db.run_backup()

If you do not wish for a database to be setup, simply do this
when you initialise the bot.

.. code-block:: python
    :linenos:

    bot = BotBase(
        command_prefix="!",
        leave_db=True
    )

Command Statistics
******************

By default the bot will log command usage statistics,
you can disable this by passing ``do_command_stats=False`` in your init.

Blacklist System
****************

Features a built in blacklist system, if a user or guild attempts to
run a command then a ``BlacklistedEntry`` exception is thrown.

This exception has a ``.message`` attribute to show to the end person.

.. code-block:: python
    :linenos:

    if isinstance(error, BlacklistedEntry):
        await ctx.send(error.message)

**Usage:**

These are built-in commands and must be enabled by passing
``load_builtin_commands=True`` to your bot constructor.

All commands besides list have an option ``reason`` param.

+-----------------------------+---------------+-------------------------+
| Command                     | Args          | Desc                    |
+=============================+===============+=========================+
| ``blacklist add person``    | User/Member   | Blacklist someone       |
+-----------------------------+---------------+-------------------------+
| ``blacklist add guild``     | Guild         | Blacklist a guild       |
+-----------------------------+---------------+-------------------------+
| ``blacklist remove person`` | User/Member   | Un-blacklist someone    |
+-----------------------------+---------------+-------------------------+
| ``blacklist remove guild``  | Guild         | Un-blacklist a guild    |
+-----------------------------+---------------+-------------------------+
| ``blacklist list``          |               | Show all blacklists     |
+-----------------------------+---------------+-------------------------+

In code:

.. code-block:: python
    :linenos:

    # Blacklist a guild
    bot.blacklist.add_to_blacklist(9876, reason="My enemy!")

    # Un-blacklist a guild
    bot.blacklist.remove_from_blacklist(9876, reason="I forgave them")

    # Blacklist a user
    bot.blacklist.add_to_blacklist(12345, reason="My enemy!", is_guild_blacklist=False)

    # Un-blacklist a user
    bot.blacklist.remove_from_blacklist(12345, reason="I forgave them", is_guild_blacklist=False)

Uptime
******

The bot persists its creation time and provides easy access to uptimes.

.. code-block:: python
    :linenos:

    bot.get_bot_uptime()

Wrapped Types
*************

All attempts to use typehints to convert ``nextcord.Member``,
``nextcord.User`` and ``nextcord.TextChannel`` will return
a wrapped instance of those classes.

Wrapped instances have the following features:

Simple Prompts
^^^^^^^^^^^^^^

``.prompt(message, *, timeout=60.0, delete_after=True, author_id=None)``

- Easily get back a Yes or No to a given message

.. code-block:: python

    Parameters
    -----------
    message: str
        The message to show along with the prompt.
    timeout: float
        How long to wait before returning.
    delete_after: bool
        Whether to delete the confirmation message after we're done.
    author_id: Optional[int]
        The member who should respond to the prompt.
        Defaults to the author of the Context's message.

        This is required when calling on a wrapped TextChannel.

    Returns
    --------
    Optional[bool]
        True if explicit confirm,
        False if explicit deny,
        None if deny due to timeout

Simple usage:

.. code-block:: python

    @bot.command()
    async def prompt(ctx):
        answer = await ctx.prompt("Should I say hi back?")
        if answer:
            await ctx.send("Hi!")

Basic Embeds
^^^^^^^^^^^^

Send a basic embed, its cute and easy.

.. code-block:: python

    async def send_basic_embed(
        desc: str,
        *,
        color=None,
        target=None,
        reply: bool = False,
        contain_timestamp: bool = True,
        include_command_invoker: bool = True,
        **kwargs,
    ) -> discord.Message:

``target`` is an optional param denoting
where to send the embed, I.e. ``target=ctx.author``

``reply`` is used to mark whether or not the messages
should use discord's 'reply' feature.

``**kwargs`` get passed to the ``.send`` call

This will not set footers or timestamps if called
on a wrapped channel instance.

Input
^^^^^

.. code-block:: python

    async def get_input(
        title: str = None,
        description: str = None,
        *,
        timeout: int = 100,
        delete_after: bool = True,
        author_id=None,
    ) -> Optional[str]:

Formats an embed with the given ``title`` / ``description``
before waiting for a response or timeout.

``author_id`` is generally ``ctx.author.id``, unless you call
this on a wrapped channel in which case it's required.

Where These Exist
^^^^^^^^^^^^^^^^^

Both ``ctx.author`` and ``ctx.channel`` also include these methods
assuming your haven't modified ``bot_base.BotContext``.

Get or Fetch
^^^^^^^^^^^^

Removes the pain of needing chains to ensure you
actually get said object. These also return the
wrapped instances of said classes for ease of use.

Ideally you would use these *everywhere* instead of
the regular ``get_ | fetch_`` methods.

.. code-block:: python

    from bot_base.wraps import WrappedUser, WrappedChannel, WrappedMember

    user: WrappedUser = await bot.get_or_fetch_user(user_id)

    channel: WrappedChannel = await bot.get_or_fetch_channel(channel_id)

    guild: discord.Guild = await bot.get_or_fetch_guild(guild_id)

    member: WrappedMember = await bot.get_or_fetch_member(guild, member_id)

Converter Autocomplete
^^^^^^^^^^^^^^^^^^^^^^

All attempts to use typehints to convert ``nextcord.Member``,
``nextcord.User`` and ``nextcord.TextChannel`` will return
a wrapped instance of those classes. Although the type's
are currently playing up so you might get autocomplete errors
even though it works.

If you wish to fix this, I recommended doing the following.

.. code-block:: python
    :linenos:

    from bot_base.wraps import WrappedMember

    @bot.command()
    async def test(ctx, member: WrappedMember):
        # Now you have the correct autocomplete for member


Caches
******

The template features a ``TimedCache`` class, which
functions as you'd expect a ``TimedCache`` to function.

Check it out `here <https://github.com/Skelmis/DPY-Bot-Base/blob/master/bot_base/caches/timed.py>`_

.. code-block:: python
    :linenos:

    import datetime

    from bot_base.caches import TimedCache

    tc = TimedCache()
    tc.add_entry("key", "value") # Won't expire
    tc.add_entry("timed_key", "value", ttl=datetime.timedelta(days=1)) # Valid for 1 day

    tc.add_entry("key", "value2") # Throws ExistingEntry
    tc.add_entry("key", "value2", override=True) # Overwrites the key

    value = tc.get_entry("key")
    assert value == "value2"

    tc.delete_entry("key")
    tc.get_entry("key") # Will throw NonExistentEntry

    tc.force_clean() # Evicts expired items

    # Check for existence
    assert "timed_key" in tc


Optimisation
************

Please note, all wrapped classes are not slotted.


Disnake Pagination
******************

Go read the file and method docstrings for full docs. Find em `here <https://github.com/Skelmis/DPY-Bot-Base/blob/master/bot_base/paginators/disnake_paginator.py>`_

.. code-block:: python
    :linenos:

    from bot_base.paginators.disnake_paginator import DisnakePaginator

    paginator: DisnakePaginator = DisnakePaginator(
        3,
        [1,2,3,4,5,6],
        page_formatter=lambda paginator, page_items, page_number: disnake.Embed(
            description="\n".join(item for item in page_items)
        ).set_footer(text=f"Page {page_number}/{paginator.total_pages}"),
    )
    await paginator.start(interaction=inter)