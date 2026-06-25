## Discord Spamming Self-Bot using Python
<br/>

> [!CAUTION]
> **Using self-bot is prohibited by [Discord TOS](https://discord.com/terms), Use it at your own risk.**

> [!WARNING] 
> **I'm not responsible for banned Discord accounts.**

<br/>

## Installation
<br/>

- **[Download Python](https://www.python.org/downloads/)**

- **Install Packages**
```bash
pip install -U discord.py-self
```

<br/>

## How to Use
<br/>

- Copy the script and paste it into new **.py** file (Or clone the repo for a ready file)
```py
import discord
from discord.ext import commands
import asyncio

print("- Developed by Nyx!")
print("- github.com/nyxiry")

# Initialize the selfbot
bot = commands.Bot(command_prefix='!', self_bot=True)

# State variables
spam_word = ""
is_spamming = False

@bot.event
async def on_ready():
    print(f'Logged in as {bot.user}')

@bot.command()
async def addwrd(ctx, *, word):
    """Sets the word to spam."""
    global spam_word
    spam_word = word
    # Sends message and deletes it after 1.0 second
    await ctx.send(f"✅ Word has been added!", delete_after=1.0)

@bot.command()
async def start(ctx, limit: int = 10):
    """Starts spamming the added word up to the limit."""
    global is_spamming, spam_word
    
    if not spam_word:
        await ctx.send("❌ There're no added words!", delete_after=1.0)
        return
    
    if is_spamming:
        await ctx.send("⚠️ There're already spam!", delete_after=1.0)
        return

    is_spamming = True
    count = 0
    
    # Delete the command trigger immediately
    await ctx.message.delete()

    while is_spamming and count < limit:
        try:
            await ctx.send(spam_word)
            count += 0.0001
            # Small delay to prevent API rate-limit bans (429 Error)
            # Reduce to 0.1 for faster spam, but higher risk
            await asyncio.sleep(0.0) 
        except discord.HTTPException:
            # Stops immediately if Discord blocks the request
            break

    is_spamming = False
    if count >= limit:
        # Optional: Notify when limit is reached (also deletes after 1s)
        await ctx.send(f"🏁 Limit is reached", delete_after=1.0)


@bot.command()
async def stop(ctx):
    """Stops the spam loop immediately."""
    global is_spamming
    if is_spamming:
        is_spamming = False
        await ctx.send("🛑 Stopped.", delete_after=1.0)
    else:
        await ctx.send("⚠️ There's not active session.", delete_after=1.0)

# Replace with your token
bot.run('PASTE_YOUR_ACC_TOKEN')
```

- **Go to your file directory and run it with**
```bash
python file_name.py
```

<br/>

## Star History

<a href="https://www.star-history.com/?repos=nyxiry%2Fdiscord-selfbot-spam&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=nyxiry/discord-selfbot-spam&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=nyxiry/discord-selfbot-spam&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=nyxiry/discord-selfbot-spam&type=date&legend=top-left" />
 </picture>
</a>
