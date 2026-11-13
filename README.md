# crypto-radar-bot

import os
from telegram import Update
from telegram.ext import Application, CommandHandler, ContextTypes

TOKEN = os.getenv("BOT_TOKEN")

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Cześć! 👋 Jestem Blockchain Botem.\n\n"
        "Dostępne komendy:\n"
        "/info - ciekawostka o blockchainie\n"
        "/help - pomoc"
    )

async def info(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "📚 Ciekawostka!\n\n"
        "Blockchain to rodzaj cyfrowego rejestru, "
        "w którym informacje są zapisywane w połączonych blokach. "
        "Dzięki temu łatwo sprawdzić historię zapisanych danych."
    )

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Użyj /start, aby rozpocząć, albo /info, "
        "aby poznać ciekawostkę o blockchainie."
    )

def main():
    if not TOKEN:
        raise ValueError("Brakuje BOT_TOKEN w ustawieniach.")

    app = Application.builder().token(TOKEN).build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("info", info))
    app.add_handler(CommandHandler("help", help_command))
    app.run_polling()

if __name__ == "__main__":
    main()
