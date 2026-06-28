# send — Telegram Notifications from Your Terminal

A lightweight, dependency-free CLI utility that lets you send yourself notifications, files, and images on Telegram directly from the command line. Useful for getting pinged when a long-running task — a system update, a build, a backup — finally finishes.

```bash
sudo apt update && sudo apt upgrade -y && send message "Update finished!"
```

![Architecture](assets/architecture.png)

## How It Works

`send` is a small Bash script — the command you actually type. It hands your request off to `telegramSendMessage.js`, a Node.js script (uses Node 18+'s built-in `fetch`/`FormData`/`Blob`, no npm packages needed) that reads your bot credentials from a config file and calls the Telegram Bot API to deliver the message.

## Commands

| Command | Usage | What it does |
|---|---|---|
| `message` | `send message "Update finished!"` | Sends a plain text message |
| `img` | `send img screenshot.png` | Sends an image (rendered as a photo preview) |
| `file` | `send file backup.zip` | Sends any file as a document, unmodified |
| `url` | `send url https://example.com` | Sends a link (Telegram auto-generates the preview) |
| `find-chat-id` | `telegramSendMessage find-chat-id` | Lists chat IDs of everyone who has messaged your bot |

## Setup

**1. Create a bot** — message **@BotFather** on Telegram, send `/newbot`, copy the token.

**2. Get your chat ID** — message your new bot once (e.g. "hi"), then with the token saved (step 3) run:
```bash
node telegramSendMessage.js find-chat-id
```

**3. Create the config file:**
```bash
mkdir -p ~/.config/telegram-api
nano ~/.config/telegram-api/credentials.conf
```
```ini
botToken="123456789:AAExampleTokenGoesHere"
chatId="987654321"
```
```bash
chmod 600 ~/.config/telegram-api/credentials.conf
```

**4. Install:**
```bash
sudo cp send /bin/send
sudo cp telegramSendMessage.js /usr/bin/telegramSendMessage
sudo chmod +x /bin/send /usr/bin/telegramSendMessage
```

Requires **Node.js 18+**.

