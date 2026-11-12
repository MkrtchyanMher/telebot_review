# Telegram ML Bot

A Python Telegram bot that takes a text message, passes it to a pre-trained machine learning model, and sends the prediction back to the chat.

## How It Works

1. Send `/start` to the bot. It greets you by your first name.
2. Send a text message. The bot passes it to the model as a one-item list using `model.predict([text])`.
3. The bot sends the model's prediction back to the chat.

## Technologies

- **Python** for the bot logic
- **pyTelegramBotAPI (`telebot`)** for receiving and sending Telegram messages
- **`pickle`** for loading the pre-trained model from `bot.pkl`

## Setup and Usage

1. Install the Telegram library.

   ```bash
   python -m pip install pyTelegramBotAPI
   ```

   Install any libraries required by the model using the same versions that were used when it was saved.

2. Put `bot.pkl` in the directory from which you run the script. Only load pickle files from trusted sources.

3. Create a Telegram bot using `@BotFather` and the `/newbot` command. Store the bot token in an environment variable and read it in your Python script.

   ```python
   import os

   bot = telebot.TeleBot(os.environ["TELEGRAM_BOT_TOKEN"])
   ```

4. Set the token and run the bot. In Windows PowerShell, use the following commands.

   ```powershell
   $env:TELEGRAM_BOT_TOKEN = "<YOUR_BOT_TOKEN>"
   python bot.py
   ```

   Replace `bot.py` with your script's filename if it differs.

5. Open your bot in Telegram, send `/start`, and enter a test message.

## Troubleshooting

If `predict()` returns a list or NumPy array, convert the first prediction to a string before sending it to Telegram.

```python
prediction = mymodel.predict([message.text])[0]
bot.send_message(message.chat.id, str(prediction))
```
