# discord.py-bot-per-tui
ساختن بات دیسکورد به زبان پایتون


تو این اموزش یاد میگیرید چطوری یک بات دیسکورد به زبان پایتون بنویسید

# پیش نیاز ها🤨
* [PyCharm](https://www.jetbrains.com/pycharm/download/)(**من خودم از پای چارم استفاده میکنم شما میتونین بجاش از ویژوال استودیو کد استفاده کنید!**)


* [or Visual Studio Code](https://code.visualstudio.com/download/)


* [python](https://www.python.org/downloads/)


* [discord devloper](https://discord.com/developers/applications)(**برایه ساخت بات**)


* [discord.py](https://discordpy.readthedocs.io/en/stable/)


# چگونه یک بات بسازیم برایه شروع؟

اول از همه میرسیم به راحت ترین بخش کار یعنی ساخت بات اول میرین تویه سایت discord devloper
<img width="404" alt="image" src="https://github.com/sersViu/discord.py-bot-pers/assets/133254907/7309309b-e5be-40de-b8b1-74591fccd328">
بعد که رفتید تو این سایت برین قسمت Applications 
<img width="1274" alt="image" src="https://github.com/sersViu/discord.py-bot-pers/assets/133254907/5a4fb4b7-dd97-44d8-86a5-530078d8a7b5">


رویه new application کلیک کنید بعد باتو بسازید که اموزشش اینجاست!


https://github.com/sersViu/discord.py-bot-per-tui/assets/133254907/722a3bdf-1039-44a4-9178-38b175082f76




* بعد میرسیم به اصل کاری یعنی ساخت بات و تیک هایی که باید زده بشه و پروفایل بات اموزش کلی این ویدیویه زیر💁



https://github.com/sersViu/discord.py-bot-per-tui/assets/133254907/183b305c-39b0-4ba6-84cf-b9462e69a389


* خب ما الان باتو ساختیم چطور اینوایتش بدیم به سرورمون؟
* باید اول پرمیشن هایه بات رو مشخص کنید سپس اون پاین یه لینکی بهتون میده میرین تو مرورگر میزنید باتتونو اینوایت میدین!
* به این شکل


<img width="922" alt="image" src="https://github.com/sersViu/discord.py-bot-per-tui/assets/133254907/b2b5b295-8b0f-4656-a371-75847b30d1c6">


* اول تیک باتو میزنید یه لیست اون پاین باز میشه که چیزایی که ما برایه باتمون باید فعال کنیم ایناس!


<img width="1015" alt="image" src="https://github.com/sersViu/discord.py-bot-per-tui/assets/133254907/bc099e5d-1920-4c18-886c-3da151516137">

* یا دیدین یکسری از بات ها add to server دارن پاین نیک نیمشون؟
* برید تویه جنرال و مراحل زیر رو انجام بدید توجه داشته باشید ادمیناستور نزنید و همون پرم هایه قبل رو بش بدید


<img width="994" alt="image" src="https://github.com/sersViu/discord.py-bot-per-tui/assets/133254907/785e5d97-2fb6-45fd-97c7-d7cb56f96094">



هورا الان بات ما به سرور اد شد و اد تو سرور هم داره!!!

<img width="492" alt="image" src="https://github.com/sersViu/discord.py-bot-per-tui/assets/133254907/89537b00-4f17-4f6d-9371-5813bb93aad3">

# انلاین کردن بات و استواتوس ها✨
**اینجا ما میرسیم به بخش مهم داستان یعنی انلاین کرد بات و تنظیم استاتوس ها**
* اول از همه به چندتا نکته باید توجه داشته باشین
* اول اینکه ما این اموزش رو به روش cogs که روش حرفه ای تری نسبت به روش معمولی تک فایلی و سریع تر بهتری است انجام میدیم 
* بنابرین لذا اگه شما کدی دارین که توش از روش تک فایلی استفاده کردید و میخاین تبدیل به cogs کن همینطوری نمیشه
* شما باید چندتا چیز رو تعریف کنید مثل slef و اینا و یسری چیزا پشتشون سلف بزارید
* بنابرین کدی که به روش تک فایلی نوشته شده رو همینجوری تبدیل به cogs نکنین!!


***اول شما در هر برنامیه ویرایش کدی هستید یک فایل بنام  `main.py`
***بسازید که معمولا خودش خودکار تو پای چارم انجام میشه
حالا وقتشه که کد ران بات رو بزنیم!!
```py

import discord
from discord.ext import commands 
from pathlib import Path
logging.basicConfig(level=logging.DEBUG)


# Load bot configuration from JSON file
with open("config.json") as f:
    config = json.load(f)

# Set up bot intents




# Command to generate an embed message containing information about a specified user
class Bot(commands.Bot):
    def __init__(self, config):
        super().__init__(
            command_prefix="!",
            help_command=None,
            intents=discord.Intents.all(),
            application_id=config["application-id"]


       )

        self.config = config




    async def setup_hook(self):
        for file in Path("cogs").glob("*.py"):
            cog_name = file.name.split(".")[0]
            await self.load_extension(f"cogs.{cog_name}")
            print("loaded extention:", file.name)

    async def on_ready(self):
        logging.info(f"{self.user.name} has connected to Discord!")
        print(f"Connected to {len(self.guilds)} guilds")
        activity = discord.Activity(name='fela heci', type=discord.ActivityType.watching)
        await self.change_presence(status=discord.Status.idle, activity=activity)


async def on_ready(self):
    logging.info(f"{bot.user.name} has connected to Discord!")
    print(f"Connected to {len(bot.guilds)} guilds")
    activity = discord.Activity(name='fela heci', type=discord.ActivityType.watching)
    await bot.change_presence(status=discord.Status.idle, activity=activity)





if __name__ == "__main__":
    config = json.loads(open("config.json").read())
bot = Bot(config)
```




