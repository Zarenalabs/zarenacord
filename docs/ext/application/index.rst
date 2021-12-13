.. _discord_application_commands:

``discord.zarena`` -- application commands
===========================================

.. versionadded:: 2.0.0

``slash_command(**kwargs)``
---------------------------------
Defines a function as a slash-type application command.

Parameters:

- name: ``str``

  - The display name of the command. If unspecified, will use the functions name.
- guild_id: ``Optional[int]``

  - The guild ID this command will belong to. If unspecified, the command will be uploaded globally.
- description: ``str``

  - The description of the command. If unspecified, will use the functions docstring, or "No description provided" otherwise.

``message_command(**kwargs)``
------------------------------------
Defines a function as a message-type application command.

Parameters:

- name: ``str``

  - The display name of the command. If unspecified, will use the functions name.
- guild_id: ``Optional[int]``

  - The guild ID this command will belong to. If unspecified, the command will be uploaded globally.

``user_command(**kwargs)``
---------------------------------
Defines a function as a user-type application command.

Parameters:

- name: ``str``

  - The display name of the command. If unspecified, will use the functions name.
- guild_id: ``Optional[int]``

  - The guild ID this command will belong to. If unspecified, the command will be uploaded globally.

``describe(**kwargs: str)``
---------------------------------
Sets the description for the specified parameters of the slash command. Sample usage:

.. code:: py

    @zarena.slash_command()
    @describe(channel="The channel to ping")
    async def mention(self, ctx: zarena.Context, channel: discord.TextChannel):
        await ctx.send(f'{channel.mention}')

If this decorator is not used, parameter descriptions will be set to "No description provided." instead.

``class Range(min: NumT | None, max: NumT)``
---------------------------------------------
Defines a minimum and maximum value for float or int values. The minimum value is optional.

.. code:: py

    async def number(self, ctx, num: zarena.Range[0, 10], other_num: zarena.Range[10]):
        ...


``class Bot(command_prefix, help_command=<default-help-command>, description=None, **options)``
------------------------------------------------------------------------------------------------
None

**Methods:**

    ``get_application_command(self, name: str)``


Gets and returns an application command by the given name.

Parameters:

- name: ``str``

  - The name of the command.

Returns:

- |Command|_

  - The relevant command object
- ``None``

  - No command by that name was found.

ㅤ

    ``async delete_all_commands(self, guild_id: int | None = None)``


Deletes all commands on the specified guild, or all global commands if no guild id was given.

Parameters:

- guild_id: ``Optional[str]``

  - The guild ID to delete from, or ``None`` to delete global commands.

ㅤ

    ``async delete_command(self, id: int, guild_id: int | None = None)``


Deletes a command with the specified ID. The ID is a snowflake, not the name of the command.

Parameters:

- id: ``int``

  - The ID of the command to delete.
- guild_id: ``Optional[str]``

  - The guild ID to delete from, or ``None`` to delete a global command.

ㅤ

    ``async sync_commands(self)``


Uploads all commands from cogs found and syncs them with discord.
Global commands will take up to an hour to update. Guild specific commands will update immediately.



``class Context(bot: BotT, command: Command[CogT], interaction: discord.Interaction)``
---------------------------------------------------------------------------------------
The command interaction context.

Attributes

- bot: |zarena.Bot|_

  - Your bot object.
- command: Union[|SlashCommand|_, |UserCommand|_, |MessageCommand|_]

  - The command used with this interaction.
- interaction: |discord.Interaction|_

  - The interaction tied to this context.

Methods:

    ``async send(self, content=..., **kwargs)``


Responds to the given interaction. If you have responded already, this will use the follow-up webhook instead.
Parameters ``embed`` and ``embeds`` cannot be specified together.
Parameters ``file`` and ``files`` cannot be specified together.

Parameters:

- content: ``str``

  - The content of the message to respond with
- embed: |discord.Embed|_

  - An embed to send with the message. Incompatible with ``embeds``.
- embeds: |List[discord.Embed]|_

  - A list of embeds to send with the message. Incompatible with ``embed``.
- file: |discord.File|_

  - A file to send with the message. Incompatible with ``files``.
- files: |List[discord.File]|_

  - A list of files to send with the message. Incompatible with ``file``.
- ephemeral: ``bool``

  - Whether the message should be ephemeral (only visible to the interaction user).

Returns

- |discord.InteractionMessage|_ if this is the first time responding.
- |discord.WebhookMessage|_ for consecutive responses.


    ``property cog(self)``

The cog this command belongs to.

    ``property guild(self)``

The guild this interaction was executed in.

    ``property message(self)``

The message that executed this interaction.

    ``property channel(self)``

The channel the interaction was executed in.

    ``property author(self)``

The user that executed this interaction.


``class ApplicationCog(*args: Any, **kwargs: Any)``
----------------------------------------------------
The cog that must be used for application commands.

Attributes:

- bot: 
  |zarena.Bot|_

  - The bot instance.


.. _zarena.Bot: #class-botcommand_prefix-help_commanddefault-help-command-descriptionnone-options
.. |zarena.Bot| replace:: ``zarena.Bot``

.. _Command: #slash_commandkwargs
.. |Command| replace:: ``Command``
.. _SlashCommand: #slash_commandkwargs
.. |SlashCommand| replace:: ``SlashCommand``
.. _UserCommand: #user_commandkwargs
.. |UserCommand| replace:: ``UserCommand``
.. _MessageCommand: #message_commandkwargs
.. |MessageCommand| replace:: ``MessageCommand``

.. _discord.Embed: https://zarenacord.readthedocs.io/en/master/api.html#discord.Embed
.. |discord.Embed| replace:: ``discord.Embed``
.. _discord.File: https://zarenacord.readthedocs.io/en/master/api.html#discord.File
.. |discord.File| replace:: ``discord.File``
.. _List[discord.Embed]: https://zarenacord.readthedocs.io/en/master/api.html#discord.Embed
.. |List[discord.Embed]| replace:: ``List[discord.Embed]``
.. _List[discord.File]: https://zarenacord.readthedocs.io/en/master/api.html#discord.File
.. |List[discord.File]| replace:: ``List[discord.File]``

.. _discord.Interaction: https://zarenacord.readthedocs.io/en/master/api.html#discord.Interaction
.. |discord.Interaction| replace:: ``discord.Interaction``
.. _discord.InteractionMessage: https://zarenacord.readthedocs.io/en/master/api.html#discord.InteractionMessage
.. |discord.InteractionMessage| replace:: ``discord.InteractionMessage``
.. _discord.WebhookMessage: https://zarenacord.readthedocs.io/en/master/api.html#discord.WebhookMessage
.. |discord.WebhookMessage| replace:: ``discord.WebhookMessage``