# Artem Chernushevich

---

## //Contacts:

**Location:** Minsk, Belarus<br>
**Phone:** +375 29 938 05 10<br>
**E-mail:** lomon3@gmail.com<br>
**GitHub:** [@lomon3](https://github.com/lomon3)<br>
**Telegram:** [@ArChernushevich](https://t.me/ArChernushevich)<br>
[LinkedIn](https://www.linkedin.com/in/artyom-chernushevich-39215917b/)<br>

---

## //About myself:
At the moment I work as the head of the sales department of toys and lifestyle products on the largest CIS marketplaces.

I realized that I want to develop in the field of programming.

## //Skills:

- HTML, CSS/SASS, JavaScript Basics

- Python3, Aiogram

- Git (Basic)

- Adobe Photoshop, CoralDraw

---

### //Code example:

**Telegram bot on python (aiogram).** [@FrazeologusBot](https://t.me/FrazeologusBot)
*A small piece of code of a periodically launched bot, which is constantly being completed and updated.*

```python
import asyncio
import logging

from aiogram import Bot, Dispatcher
from aiogram.types import BotCommand
from aiogram.contrib.fsm_storage.memory import MemoryStorage

from app.config_reader import load_config
from app.handlers.drinks import register_handlers_drinks
from app.handlers.starthelp import register_handlers_starthelp
from app.handlers.common import register_handlers_common
from data_base import sqlite_db
logger = logging.getLogger(__name__)


async def set_commands(bot: Bot):
    commands = [
        BotCommand(command="/start", description="Начать"),
        BotCommand(command="/help", description="Помощь"),
        BotCommand(command="/food", description="Заказать блюда"),
        BotCommand(command="/cancel", description="Отменить текущее действие")
    ]
    await bot.set_my_commands(commands)


async def main():
    # Настройка логирования в stdout
    logging.basicConfig(
        level=logging.INFO,
        format="%(asctime)s - %(levelname)s - %(name)s - %(message)s",
    )
    logger.error("Starting bot")

    # Парсинг файла конфигурации
    config = load_config("config/bot.ini")

    # Объявление и инициализация объектов бота и диспетчера
    bot = Bot(token=config.tg_bot.token)
    dp = Dispatcher(bot, storage=MemoryStorage())

    # Регистрация хэндлеров
    register_handlers_common(dp, config.tg_bot.admin_id)
    register_handlers_drinks(dp)
    register_handlers_starthelp(dp)

    # Установка команд бота
    await set_commands(bot)

    #DB start
    sqlite_db.sql_start()

    # Запуск поллинга
    await dp.skip_updates()  # пропуск накопившихся апдейтов (необязательно)
    await dp.start_polling()


if __name__ == '__main__':
    asyncio.run(main())
```

---

### //Education:

- **University:** _BSU. Faculty of Radiophysics and Computer Technologies (2013-2017)_
- **Cources:** _RS Schools Course «JavaScript/Front-end. Stage 0» (unfinished)_
- **Languages:**
 - _English - A2_
 - _Russian - Native_