# discordbot

import discord
import random
import time

# Список токенов для авторизации
TOKENS = ['token1', 'token2', 'token3']
# Список фраз для отправки
PHRASES = ['Фраза 1', 'Фраза 2', 'Фраза 3', 'Фраза 4']
# Временной промежуток между отправкой сообщений (в секундах)
TIME_INTERVAL = (10, 60)  # Отправка сообщений происходит через 10-60 секунд

class DiscordBot(discord.Client):
    def __init__(self, token):
        super().__init__()
        self.token = token

    async def on_ready(self):
        print(f'Logged in as {self.user.name} ({self.user.id})')

    async def send_message(self):
        await self.wait_until_ready()
        while not self.is_closed():
            channel = self.get_channel(channel_id)  # Замените channel_id на ID нужного вам текстового канала

            if channel is not None:
                random_phrase = random.choice(PHRASES)
                await channel.send(random_phrase)

            # Генерация случайной задержки перед отправкой следующего сообщения
            delay = random.randint(*TIME_INTERVAL)
            await asyncio.sleep(delay)
    

# Создание и запуск ботов
bots = []
for token in TOKENS:
    bot = DiscordBot(token)
    bots.append(bot)
    bot.loop.create_task(bot.send_message())

for bot in bots:
    bot.run(bot.token)
