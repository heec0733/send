send — сповіщення в Telegram з терміналу
==========================================

Легка утиліта без залежностей, щоб надсилати собі повідомлення, файли
й картинки в Telegram прямо з командного рядка. Зручно, коли довга
задача (оновлення системи, збірка, бекап) нарешті закінчилась.

    sudo apt update && sudo apt upgrade -y && send message "Update finished!"


Як працює
---------

`send` — це Bash-скрипт (команда, яку вводиш). Він передає запит до
`telegramSendMessage.js` (Node.js, потрібен Node 18+, без npm-пакетів),
який бере токен бота й chat ID з конфігу і відправляє через Telegram
Bot API.


Команди
-------

message
    send message "Текст"
    → надсилає текстове повідомлення

img
    send img screenshot.png
    → надсилає картинку (як фото)

file
    send file backup.zip
    → надсилає файл як документ

url
    send url https://example.com
    → надсилає лінк (з прев'ю)

find-chat-id
    telegramSendMessage find-chat-id
    → показує chat ID всіх, хто писав боту


Інструкція

1. Створити бота
   Написати @BotFather, /newbot, зберегти токен.

2. Отримати chat ID
   Написати своєму боту (напр. "hi"), потім:

       node telegramSendMessage.js find-chat-id

3. Створити конфіг:

       mkdir -p ~/.config/telegram-api
       nano ~/.config/telegram-api/credentials.conf

   Вміст файлу:

       botToken="токен_тут"
       chatId="chat_id_тут"

       chmod 600 ~/.config/telegram-api/credentials.conf

4. Встановити:

       git clone https://github.com/heec0733/send
       cd send/
       sudo cp send /bin/send
       sudo cp telegramSendMessage.js /usr/bin/telegramSendMessage
       sudo chmod +x /bin/send /usr/bin/telegramSendMessage

Потрібен Node.js 18+.
