import telebot
from g4f.client import Client

# Устанавливаем токен бота
TOKEN = input("введите токен телеграм бота ")
bot = telebot.TeleBot(TOKEN)

# Переменная для хранения текущей модели
current_model = "claude-3-haiku"

@bot.message_handler(commands=['start', 'help'])
def send_welcome(message):
    bot.reply_to(message, "Привет! Я готов помочь. Просто напиши мне запрос.чтобы использовать нейросеть claude 3 напишите /model claude,если blacbox ai то введите /model blackbox")

@bot.message_handler(commands=['model'])
def change_model(message):
    global current_model
    if message.text.lower() == '/model claude':
        current_model = "claude-3-haiku"
        bot.reply_to(message, "Модель изменена на Claude.")
    elif message.text.lower() == '/model blackbox':
        current_model = "blackbox"
        bot.reply_to(message, "Модель изменена на Blackbox.")
    else:
        bot.reply_to(message, "Неверная команда. Используйте /model claude или /model blackbox.")

@bot.message_handler(func=lambda message: True)
def handle_message(message):
    user_prompt = message.text
    client = Client()
    response = client.chat.completions.create(
        model=current_model,
        messages=[{"role": "user", "content": user_prompt}],
    )
    bot.reply_to(message, response.choices[0].message.content)

bot.polling()
