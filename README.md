# Telegram News Bot

این یک ربات تلگرامی برای دریافت و مدیریت اخبار است.

## پیش‌نیازها

* پایتون ۳.۱۱ یا بالاتر
* یک توکن ربات از [@BotFather](https://t.me/BotFather)
* میتونید از @userinfobot آیدی خودتون رو بگیرین
* فایل config.json رو باز کنین و در صورت نیاز پرامپت هوش مصنوعی و موضوعات و لینک سایتای خبری رو عوض کنین.

## راه‌اندازی (لینوکس و ویندوز)

۱. مخزن را کلون کرده و وارد پوشه شوید:
```bash
git clone https://github.com/amirehp/telegram_news_bot.git
cd telegram_news_bot
```

۲. یک محیط مجازی (Virtual Environment) ایجاد و فعال کنید:
```bash
# در لینوکس:
python3 -m venv .venv
source .venv/bin/activate

# در ویندوز:
python -m venv .venv
.venv\Scripts\activate
```

۳. نیازمندی‌ها را نصب کنید:
```bash
pip install -r requirements.txt
```

۴. یک فایل با نام `.env` در ریشه پروژه ایجاد کرده و مقادیر زیر را در آن قرار دهید:
```env
TELEGRAM_TOKEN=your_telegram_bot_token_here
TELEGRAM_OWNER_ID=your_telegram_user_id_here
GEMINI_API_KEY=your_gemini_api_key
```
برای گرفتن API key gemini
https://aistudio.google.com/app/api-keys


## اجرای ربات

برای اجرای دستی:
```bash
python src/main.py
```

or

```bash
python3 src/main.py
```

## اجرای خودکار

### در لینوکس (Systemd)
برای اجرای خودکار ربات در اوبونتو/لینوکس، از یک فایل `service` استفاده کن :


1. فایل اجرایی رو اجرا پذیر کن
`chmod +x path/to/project/run.sh`


2. یک فایل سرویس بسازید: `sudo nano ~/.config/systemd/user/newsbot.service` 
3. محتوای زیر را در آن قرار دهید (مسیرها را اصلاح کنید):
```ini
[Unit]
Description=Telegram News Bot 

[Service] 
WorkingDirectory=/path/to/telegram_news_bot
ExecStart=/path/to/telegram_news_bot/.venv/bin/python src/main.py
Restart=always
```

4. Timer بساز
`nano ~/.config/systemd/user/newsbot.timer`

5. اینارو توی فایلش قرار بده
```ini
[Unit]
Description=Run newsbot every hour

[Timer]
OnBootSec=10min
OnUnitActiveSec=1h
Persistent=false

[Install]
WantedBy=timers.target
```


6. سرویس را فعال و اجرا کنید:
```bash
systemctl --user daemon-reload
systemctl --user enable --now newsbot.timer 
```

### در ویندوز (Task Scheduler) 

1. دستور زیر را در CMD (با دسترسی Administrator) اجرا کنید:

```cmd
schtasks /create /tn "NewsBot" /tr "\"C:\path\to\your\project\run.bat\"" /sc onlogon /rl highest
```

2. برای تنظیم تکرار (مثلاً هر ۲ ساعت)، `Task Scheduler` (با دستور `taskschd.msc`) را باز کنید و در تنظیمات `Trigger` ربات، تیک `Repeat task every` را روی `2 hours` و `Duration` را روی `Indefinitely` بگذارید.

Task Scheduler →  task NewsBot → Properties → Triggers → Edit →   Repeat task every: 2 hours → Duration: Indefinitely.


## مشارکت

خوشحال می‌شویم اگر پیشنهادی دارید، آن را به صورت Issue یا Pull Request ارسال کنید.


