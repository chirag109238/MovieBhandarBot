from telethon import TelegramClient, events
import asyncio
import os

api_id = int(os.getenv("API_ID"))
api_hash = os.getenv("API_HASH")
bot_token = os.getenv("BOT_TOKEN")

client = TelegramClient('bot', api_id, api_hash).start(bot_token=bot_token)

# Command to send the movie
@client.on(events.NewMessage(pattern='/movie'))
async def send_movie(event):
    chat_id = event.chat_id
    message = await client.send_file(chat_id, 'movie.mp4', caption="🎬 Here's your movie! \n⏳ Auto-delete in 10 minutes.")

    # Delete the movie after 10 minutes
    await asyncio.sleep(600)
    await message.delete()

# Start the bot
client.run_until_disconnected()
