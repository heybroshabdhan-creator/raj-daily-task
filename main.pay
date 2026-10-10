
import os
from telegram import Update, ReplyKeyboardMarkup
from telegram.ext import (
    Application,
    CommandHandler,
    MessageHandler,
    ContextTypes,
    filters
)

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    keyboard = [
        ["🖼️ ছবি দেখার কাজ"],
        ["❓ প্রশ্নের উত্তর", "📝 ছোট সার্ভে"],
        ["📋 কাজের নিয়ম"]
    ]
    await update.message.reply_text(
        "স্বাগতম Raj Daily Task-এ! 😊\nএকটি কাজ বেছে নাও:",
        reply_markup=ReplyKeyboardMarkup(keyboard, resize_keyboard=True)
    )

async def handle(update: Update, context: ContextTypes.DEFAULT_TYPE):
    text = update.message.text

    if text == "🖼️ ছবি দেখার কাজ":
        await update.message.reply_text("ছবি দেখার কাজ শিগগিরই যোগ করা হবে।")
    elif text == "❓ প্রশ্নের উত্তর":
        context.user_data["mode"] = "question"
        await update.message.reply_text("বাংলাদেশের রাজধানীর নাম কী?")
    elif text == "📝 ছোট সার্ভে":
        context.user_data["mode"] = "survey"
        await update.message.reply_text("তুমি কি মোবাইল দিয়ে কাজ করতে পছন্দ করো? হ্যাঁ অথবা না লেখো।")
    elif text == "📋 কাজের নিয়ম":
        await update.message.reply_text("একটি কাজ বেছে নাও এবং নির্দেশনা অনুসরণ করো।")
    elif context.user_data.get("mode") == "question":
        context.user_data.pop("mode", None)
        await update.message.reply_text("ধন্যবাদ! সঠিক উত্তর: ঢাকা।")
    elif context.user_data.get("mode") == "survey":
        context.user_data.pop("mode", None)
        await update.message.reply_text("তোমার উত্তর গ্রহণ করা হয়েছে। ধন্যবাদ!")
    else:
        await update.message.reply_text("নিচের মেনু থেকে একটি কাজ বেছে নাও।")

def main():
    token = os.environ.get("BOT_TOKEN")
    if not token:
        raise RuntimeError("BOT_TOKEN সেট করা হয়নি")

    app = Application.builder().token(token).build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle))
    app.run_polling()

if __name__ == "__main__":
    main()

