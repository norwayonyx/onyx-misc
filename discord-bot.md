# 🤖 How to Create and Deploy a Discord Bot

A step-by-step guide covering both **Python** and **JavaScript (Node.js)** implementations.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Creating the Bot on Discord](#2-creating-the-bot-on-discord)
3. [Setting Up Your Project](#3-setting-up-your-project)
4. [Writing the Bot Code](#4-writing-the-bot-code)
5. [Adding Commands](#5-adding-commands)
6. [Inviting the Bot to Your Server](#6-inviting-the-bot-to-your-server)
7. [Running the Bot](#7-running-the-bot)
8. [Keeping the Bot Online 24/7 (Optional)](#8-keeping-the-bot-online-247-optional)

---

## 1. Prerequisites

### Python
- Python 3.8 or higher → [python.org](https://www.python.org/downloads/)
- `pip` (comes with Python)

### JavaScript
- Node.js 16.9 or higher → [nodejs.org](https://nodejs.org/)
- `npm` (comes with Node.js)

### Both
- A Discord account
- A text editor (e.g. VS Code)

---

## 2. Creating the Bot on Discord

This step is the same regardless of which language you use.

### Step 1 — Go to the Discord Developer Portal
Visit [https://discord.com/developers/applications](https://discord.com/developers/applications) and log in.

### Step 2 — Create a New Application
- Click **"New Application"**
- Give it a name (this will be your bot's name)
- Click **"Create"**

### Step 3 — Create the Bot User
- In the left sidebar, click **"Bot"**
- Click **"Add Bot"** → confirm with **"Yes, do it!"**

### Step 4 — Copy the Bot Token
- Under the **Token** section, click **"Reset Token"** then **"Copy"**
- ⚠️ **Keep this token secret!** Never share it or commit it to GitHub.

### Step 5 — Configure Bot Permissions
- On the same **Bot** page, scroll down to **"Privileged Gateway Intents"**
- Enable the following based on what your bot needs:
  - **Presence Intent** — to read user presence/status
  - **Server Members Intent** — to read member lists
  - **Message Content Intent** — to read message content *(required for reading messages)*

---

## 3. Setting Up Your Project

### Python

```bash
# Create a project folder
mkdir my-discord-bot
cd my-discord-bot

# (Recommended) Create a virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install the discord.py library
pip install discord.py
```

Store your token safely in a `.env` file:
```bash
pip install python-dotenv
```

Create a `.env` file in your project folder:
```
DISCORD_TOKEN=your_token_here
```

---

### JavaScript

```bash
# Create a project folder
mkdir my-discord-bot
cd my-discord-bot

# Initialize a Node.js project
npm init -y

# Install the discord.js library
npm install discord.js

# Install dotenv for token management
npm install dotenv
```

Create a `.env` file in your project folder:
```
DISCORD_TOKEN=your_token_here
```

---

### Both — Add a .gitignore

Create a `.gitignore` file to avoid accidentally leaking your token:
```
.env
node_modules/
venv/
__pycache__/
```

---

## 4. Writing the Bot Code

### Python — `bot.py`

```python
import discord
from discord.ext import commands
from dotenv import load_dotenv
import os

# Load token from .env
load_dotenv()
TOKEN = os.getenv('DISCORD_TOKEN')

# Set up intents
intents = discord.Intents.default()
intents.message_content = True  # Required to read messages

# Create the bot with a command prefix
bot = commands.Bot(command_prefix='!', intents=intents)

@bot.event
async def on_ready():
    print(f'✅ Logged in as {bot.user} (ID: {bot.user.id})')

# Run the bot
bot.run(TOKEN)
```

---

### JavaScript — `index.js`

```js
require('dotenv').config();
const { Client, GatewayIntentBits } = require('discord.js');

// Create the client with required intents
const client = new Client({
    intents: [
        GatewayIntentBits.Guilds,
        GatewayIntentBits.GuildMessages,
        GatewayIntentBits.MessageContent, // Required to read messages
    ]
});

client.once('ready', () => {
    console.log(`✅ Logged in as ${client.user.tag}`);
});

// Log in with the token
client.login(process.env.DISCORD_TOKEN);
```

---

## 5. Adding Commands

### Python

```python
# Basic command — responds to "!hello"
@bot.command()
async def hello(ctx):
    await ctx.send(f'Hello, {ctx.author.name}! 👋')

# Command with an argument
@bot.command()
async def say(ctx, *, message: str):
    await ctx.send(message)

# Command that sends an embed
@bot.command()
async def info(ctx):
    embed = discord.Embed(
        title="Bot Info",
        description="I'm a custom Discord bot!",
        color=discord.Color.blue()
    )
    embed.add_field(name="Prefix", value="!", inline=True)
    embed.set_footer(text="Made with discord.py")
    await ctx.send(embed=embed)
```

---

### JavaScript

```js
// Listen for messages
client.on('messageCreate', message => {
    // Ignore messages from bots
    if (message.author.bot) return;

    // Basic command — responds to "!hello"
    if (message.content === '!hello') {
        message.reply(`Hello, ${message.author.username}! 👋`);
    }

    // Command with an argument
    if (message.content.startsWith('!say ')) {
        const text = message.content.slice(5); // Remove "!say "
        message.channel.send(text);
    }

    // Command that sends an embed
    if (message.content === '!info') {
        const { EmbedBuilder } = require('discord.js');
        const embed = new EmbedBuilder()
            .setTitle('Bot Info')
            .setDescription("I'm a custom Discord bot!")
            .setColor(0x0099FF)
            .addFields({ name: 'Prefix', value: '!', inline: true })
            .setFooter({ text: 'Made with discord.js' });
        message.channel.send({ embeds: [embed] });
    }
});
```

---

## 6. Inviting the Bot to Your Server

### Step 1 — Generate an Invite Link
- Go back to the [Discord Developer Portal](https://discord.com/developers/applications)
- Select your application → click **"OAuth2"** in the sidebar → then **"URL Generator"**

### Step 2 — Select Scopes
Check the following:
- ✅ `bot`
- ✅ `applications.commands` *(if you plan to use slash commands)*

### Step 3 — Select Bot Permissions
Under **Bot Permissions**, select what your bot needs. For a basic bot:
- ✅ Read Messages / View Channels
- ✅ Send Messages
- ✅ Embed Links
- ✅ Read Message History

### Step 4 — Copy and Open the Link
- Scroll down and copy the generated URL
- Open it in your browser
- Select your server from the dropdown and click **"Authorize"**

---

## 7. Running the Bot

### Python

```bash
python bot.py
```

You should see:
```
✅ Logged in as YourBot#1234 (ID: 123456789)
```

### JavaScript

```bash
node index.js
```

You should see:
```
✅ Logged in as YourBot#1234
```

---

## 8. Keeping the Bot Online 24/7 (Optional)

Your bot stops when you close the terminal. Here are common solutions to keep it running:

### Option A — Using a VPS (e.g. a cheap Linux server)

**Python — use `pm2` or `systemd`:**
```bash
# Install pm2
npm install -g pm2

# Run your Python bot with pm2
pm2 start bot.py --interpreter python3 --name my-bot
pm2 save
pm2 startup
```

**JavaScript — use `pm2`:**
```bash
pm2 start index.js --name my-bot
pm2 save
pm2 startup
```

---

### Option B — Railway / Render / Fly.io (Free/cheap cloud hosting)

These platforms let you deploy your bot by connecting your GitHub repo. General steps:
1. Push your code to a **private** GitHub repository
2. Sign up at [railway.app](https://railway.app), [render.com](https://render.com), or [fly.io](https://fly.io)
3. Create a new project and connect your repo
4. Add your `DISCORD_TOKEN` as an **environment variable** in the platform's settings
5. Deploy — the platform will build and run your bot automatically

---

### Option C — Replit (Easiest, free tier available)

1. Go to [replit.com](https://replit.com) and create a new Repl
2. Choose **Python** or **Node.js**
3. Paste your bot code and add your token to **Secrets** (not in code!)
4. Use a service like [UptimeRobot](https://uptimerobot.com) to ping your Repl URL every 5 minutes to keep it awake

---

## ⚠️ Important Reminders

- **Never hardcode your token** in your code — always use environment variables
- **Never commit your `.env` file** to GitHub — add it to `.gitignore`
- If your token is ever exposed, go to the Developer Portal immediately and **reset it**
- Be mindful of Discord's **rate limits** — don't spam API calls in loops
