import os
from aiohttp import web
from aiogram import Bot, Dispatcher, types
from aiogram.filters import CommandStart

TOKEN = "8746874369:AAHsPG3lsRYOE0D43xrwUim9gpDwRTHW2AI"
dp = Dispatcher()
bot = Bot(token=TOKEN)

async def handle(request):
    return web.Response(text="Bot is alive!")

@dp.message(CommandStart())
async def cmd_start(message: types.Message):
    val = message.text.split()
    if len(val) > 1:
        await message.answer(f"Ссылка получена! Скоро тут будет ключ.")
    else:
        await message.answer("Привет! Отправь мне ссылку.")

async def web_server():
    app = web.Application()
    app.add_routes([web.get("/", handle)])
    runner = web.AppRunner(app)
    await runner.setup()
    port = int(os.environ.get("PORT", 10000))
    site = web.TCPSite(runner, "0.0.0.0", port)
    await site.start()

async def main():
    await web_server()
    print("Веб-сервер запущен, запускаем бота...")
    await dp.start_polling(bot)

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
