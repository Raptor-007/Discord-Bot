![LH-Cyber-Security](Images/image.png)

----------

# Music Bot



## Commands


| Commands | Example | Description | Authorization |
| ------ | ------ |  ------ | ------ |
| !play | !play "URL"| Plays the URL | @everyone  |
| !loop | !loop "URL" "8" | Loops the track eight times | @everyone  |
| !stop | !pause, !break, !stop | The bot stops the current song | @everyone  |
| !start | !play, !start | Restarts the paused song | @everyone  |
| !queue | !queue | Shows the queue | @everyone  |
| !join | !join, !join "#channel" | Joins in the channel | @everyone  |
| !leave | !leave | Leaves the channel | @everyone  |
| !clear | !clear queue, !clear loop | Clears the queue or the loop | @everyone  |
| !help | !help | Shows a help page | @everyone  |
| !restet | !restet | Resets everything | @owner |
| !prefix | !prefix "new prefix" | Changes the prefix to "prefix". | @owner |

----------

## Important

* If the bot is playing something in a channel it cannot be moved with "!join".
* The bot leaves the channel automatically after 5 min inactivity.
* When the bot leaves or changes the channel, all songs and queues will be reseted.
* The bot must be able to run multiple times on the same server.

----------

![LH-Cyber-Security](Images/image.png)

----------

# Community Bot




## Commands


| Commands | Example | Description | Authorization |
| ------ | ------ |  ------ | ------ |
| !meme | !meme | Sends a meme | @everyone  |
| !game | !game | A little game | @everyone  |
| !ban | !ban "@USER" | Ban a user | @owner  |
| !unban | !unban "@USER" | Unban the user | @owner  |
| !mute | !mute "@USER" | Mute a user | @owner  |
| !unmute | !unmute "@USER" | Unmute a user | @owner  |
| !set | !set join "#channel", !set leave "#channel" | Sets the channel in which the (welcome / leave) messages are sent to. | @owner  |
| !del | !del join "#channel", !del leave "#channel" | Removes the channel in which the (welcome / leave) messages are sent to. | @owner  |
| !help | !help | Shows a help page | @everyone  |
| !prefix | !prefix "new prefix" | Changes the prefix to "prefix". | @owner |
| !info | !info "@USER", !serverinfo, !info server | Shows information about the server as well as about the user. | @everyone |
| !leaderboard | !leaderboard, !leaderboard invites, leaderboard activity | Shows a ranking of the most active users or with the most invites. | @everyone |
| !verify | !verify "#channel" | Sets the channel in which the verification query will be made | @owner |


----------



## JoinMessage Example

```python
@client.event
async def on_member_join(member):

    embed = discord.Embed(title=f"Willkommen {member.display_name}",
                          description=f"Im Kanal {client.get_channel(ytChannel).mention} wirst du immer die neusten Videos von LH Cyber Security finden. Um dir Self Roles zuzuweisen gehe in den Channel {client.get_channel(settingsChannel).mention} und wähle da deine Themen aus. Schau dich einfach mal um und bei Fragen stehen wir dir gerne zur Verfügung. Das LH Team wünscht dir {member.mention} einen angenehmen Aufenthalt.",
                          embed=discord.Embed(color=0xfefbfb),
                          timestamp=datetime.datetime.utcnow()
                          )

    embed.set_thumbnail(
        url="https://media.discordapp.net/attachments/707638208124682260/764405331182485514/LH_Logo.png"
    )

    embed.set_footer(text='Community Bot', icon_url='https://media.discordapp.net/attachments/707638208124682260/764405331182485514/LH_Logo.png')

    await client.get_channel(joinChannel).send(embed=embed)

```

 ## Verify Command

```python
import discord
from discord.ext import commands

TOKEN = ""
owner_ids = [334567239342620675, 338711554683830292]
role = "Member" #Rolle nach verifikation
status = ['LH Bot', 'Protects the Discord', 'Verification Bot']
queue = []
welcome_channel_id = 707638208124682260
bot = commands.Bot(command_prefix='!', owner_id=owner_ids)
bot.remove_command('help')

#Wenn Bot gestartet
@bot.event
async def on_ready():
    welcome_channel = bot.get_channel(welcome_channel_id)
    print(f"Eingeloggt als: {bot.user.name} - {bot.user.id}\nVersion: {discord.__version__}\n")
    await bot.change_presence(status=discord.Status.online)
    print('Erfolgreich gestartet...\n')
    print('Events:\n\n')

#Wenn Bot gestopt
@bot.command(name='stop', aliases=['shutdown'])
async def stop(ctx):
    if ctx.author.id in bot.owner_id:
        await ctx.send('Bot stoppt...')
        await bot.close()

#Wenn !verify
@bot.command(name='verify')
@commands.has_permissions(administrator=True)
async def verify(ctx):


    embed = discord.Embed(colour=discord.colour.Colour.blue(),
                          url="https://media.discordapp.net/attachments/707638208124682260/764118143429771314/LH_Logo.png")
    embed.set_author(name="Verification Bot",
                     url="https://www.youtube.com/channel/UCe4PsvZK8Tdn1R3M-j-bqOQ",
                     icon_url="https://media.discordapp.net/attachments/707638208124682260/764118143429771314/LH_Logo.png")
    embed.set_thumbnail(
        url="https://media.discordapp.net/attachments/707638208124682260/764118143429771314/LH_Logo.png")
    embed.add_field(name="Bitte klicke auf :white_check_mark: um deinen Account zu verifizieren.",
                    value="Wenn du Problem hast mit der Verifikation kontaktiere einen Admin.", inline=True)

    await ctx.send(embed=embed)

#Rollen verteilung
@bot.event
async def on_reaction_add(reaction, user):
    if str(reaction.emoji) == "✅": 
        Member = discord.utils.get(user.guild.roles, name=Member)
        await user.add_roles(Member)



#Bot Token
bot.run(TOKEN)
```

----------







## Links
[![N|Solid](Images/Discord.png)](https://discord.gg/aUP35py)
