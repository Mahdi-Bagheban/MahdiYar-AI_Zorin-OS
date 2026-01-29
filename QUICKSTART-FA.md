# 📦 Persian ASR v2.0 - Quick Start Guide

**بسم الله الرحمن الرحیم**

شامل تمام فایل‌های حرفه‌ای و مستندات کامل

---

## 📂 ساختار فایل‌ها

```
persian-asr-v2.0/
├── ai-installer-v2-enhanced.sh      # ✅ نصب‌کننده اصلی
├── README.md                         # ✅ راهنمای انگلیسی
├── README-FA.md                      # ✅ راهنمای فارسی (کامل)
├── INSTALLATION-GUIDE-FA.md          # ✅ راهنمای نصب مفصل
├── config.env.example                # ✅ نمونه پیکربندی
├── requirements.txt                  # ✅ وابستگی‌های Python
├── Dockerfile                        # ✅ فایل Docker
├── docker-compose.yml                # ✅ Docker Compose
├── troubleshoot.sh                   # ✅ ابزار عیب‌یابی
├── api-examples.sh                   # ✅ نمونه‌های API
└── QUICKSTART.md                     # 📄 این فایل

```

---

## 🚀 3 مرحله نصب سریع

### **مرحله 1: دانلود و اجازه**

```bash
cd /tmp
wget https://example.com/ai-installer-v2-enhanced.sh
chmod +x ai-installer-v2-enhanced.sh
```

### **مرحله 2: نصب**

```bash
sudo ./ai-installer-v2-enhanced.sh
```

✅ نصب خودکار تمام وابستگی‌ها (20-40 دقیقه)

### **مرحله 3: شروع و تست**

```bash
# شروع سرویس
sudo systemctl start persian-asr

# فعالسازی در boot
sudo systemctl enable persian-asr

# تست
curl http://localhost:7070/health | jq
```

---

## 📋 فایل‌ها و توضیحات

### 🔧 فایل‌های اصلی

| فایل | توضیح |
|------|--------|
| `ai-installer-v2-enhanced.sh` | **نصب‌کننده حرفه‌ای** - تمام چیز را خودکار نصب می‌کند |
| `requirements.txt` | وابستگی‌های Python برای پروژه |
| `Dockerfile` | برای اجرا در Docker |
| `docker-compose.yml` | برای اجرا با Docker Compose |

### 📚 فایل‌های مستندات

| فایل | توضیح |
|------|--------|
| `README.md` | راهنمای اصلی (انگلیسی) |
| `README-FA.md` | راهنمای کامل (فارسی) ⭐ **بخوانید!** |
| `INSTALLATION-GUIDE-FA.md` | راهنمای نصب گام‌به‌گام |
| `QUICKSTART.md` | این فایل - شروع سریع |

### ⚙️ فایل‌های پیکربندی

| فایل | توضیح |
|------|--------|
| `config.env.example` | نمونه متغیرهای محیطی - **کپی به `/opt/persian-asr/.env`** |

### 🛠️ فایل‌های ابزار

| فایل | توضیح |
|------|--------|
| `troubleshoot.sh` | ابزار خودکار عیب‌یابی |
| `api-examples.sh` | نمونه‌های استفاده از API |

---

## 📍 مسیرهای مهم

بعد از نصب:

```bash
# دایرکتوری نصب
/opt/persian-asr/
  ├── app.py                  # اپلیکیشن اصلی
  ├── .env                    # کلید API و تنظیمات
  ├── venv/                   # محیط مجازی Python
  └── README-FA.md            # راهنمای فارسی

# پیکربندی
/etc/persian-asr/
  └── config.env              # فایل پیکربندی

# لاگ‌ها
/var/log/persian-asr/
  ├── install.log             # لاگ نصب
  └── asr.log                 # لاگ اپلیکیشن

# کش
/var/cache/persian-asr/       # فایل‌های کش
```

---

## ⌨️ دستورات مهم

### شروع و متوقف کردن

```bash
# شروع
sudo systemctl start persian-asr

# توقف
sudo systemctl stop persian-asr

# بازراه‌اندازی
sudo systemctl restart persian-asr

# وضعیت
sudo systemctl status persian-asr
```

### مشاهده لاگ‌ها

```bash
# لاگ‌های live
sudo journalctl -u persian-asr -f

# ۵۰ خط آخر
sudo journalctl -u persian-asr -n 50

# فقط خطاها
sudo journalctl -u persian-asr -p err
```

### تست API

```bash
# بررسی سلامت
curl http://localhost:7070/health | jq

# اطلاعات سرویس
curl http://localhost:7070/ | jq

# تبدیل فایل
curl -X POST http://localhost:7070/transcribe \
  -F "file=@audio.wav" | jq '.text'
```

### دریافت API Key

```bash
grep ASR_API_KEY /opt/persian-asr/.env
```

---

## 🎯 اولین استفاده

### 1. تبدیل یک فایل صوتی

```bash
# یک فایل صوتی دارید؟
curl -X POST http://localhost:7070/transcribe \
  -F "file=@your-audio.wav"

# فقط متن می‌خواهید؟
curl -X POST http://localhost:7070/transcribe-simple \
  -F "file=@your-audio.wav" | jq '.text'
```

### 2. Python استفاده کنید

```python
import requests

with open('audio.wav', 'rb') as f:
    response = requests.post(
        'http://localhost:7070/transcribe',
        files={'file': f}
    )
    print(response.json()['text'])
```

### 3. مستندات API

```bash
# در مرورگر
firefox http://localhost:7070/docs
```

---

## ⚙️ تنظیمات اساسی

### تغییر مدل Whisper

```bash
# ویرایش
sudo nano /etc/persian-asr/config.env

# تغییر مدل (tiny/base/small/medium/large)
WHISPER_MODEL=medium

# بازراه‌اندازی
sudo systemctl restart persian-asr
```

### تغییر پورت

```bash
# پیش‌فرض: 7070
sudo nano /etc/persian-asr/config.env
ASR_PORT=8080

sudo systemctl restart persian-asr
```

### دسترسی از دستگاه‌های دیگر

⚠️ **هشدار**: فقط اگر امن باشد!

```bash
sudo nano /etc/persian-asr/config.env
ASR_HOST=0.0.0.0

sudo systemctl restart persian-asr
```

---

## 🐛 عیب‌یابی سریع

### سرویس شروع نمی‌شود

```bash
# لاگ‌ها را ببینید
sudo journalctl -u persian-asr -n 20

# یا استفاده کنید از:
sudo bash /opt/persian-asr/troubleshoot.sh
```

### API پاسخ نمی‌دهد

```bash
# بررسی پورت
sudo lsof -i :7070

# بررسی سرویس
systemctl status persian-asr

# بازراه‌اندازی
sudo systemctl restart persian-asr
sleep 5
curl http://localhost:7070/health
```

### خطای حافظه

```bash
# بررسی RAM
free -h

# مدل کوچک‌تر استفاده کنید
sudo nano /etc/persian-asr/config.env
WHISPER_MODEL=small
sudo systemctl restart persian-asr
```

---

## 🐳 Docker استفاده

### با Docker Compose

```bash
# شروع
docker-compose up -d

# لاگ‌ها
docker-compose logs -f persian-asr

# توقف
docker-compose down
```

### دستی

```bash
# ساخت
docker build -t persian-asr:v2.0 .

# اجرا
docker run -d \
  -p 7070:7070 \
  --name persian-asr \
  persian-asr:v2.0

# لاگ‌ها
docker logs -f persian-asr
```

---

## 📚 مستندات بیشتر

**الزام است بخوانید:**

1. **مستندات فارسی کامل**:
   ```bash
   cat README-FA.md
   ```

2. **راهنمای نصب مفصل**:
   ```bash
   cat INSTALLATION-GUIDE-FA.md
   ```

3. **API Interactive**:
   ```bash
   # در مرورگر
   http://localhost:7070/docs
   ```

---

## 💡 نکات مهم

### 1️⃣ مدل موصیه شده

برای Zorin OS:
```
WHISPER_MODEL=medium ⭐
```

- تعادل خوب
- ~5GB RAM
- سرعت معقول

### 2️⃣ API Key

```bash
# حفاظت کنید!
grep ASR_API_KEY /opt/persian-asr/.env

# جای امن ذخیره کنید
```

### 3️⃣ نظارت

```bash
# سلامت سرویس
watch -n 5 'systemctl status persian-asr'

# استفاده از منابع
watch -n 5 'free -h && top -b -n 1 | head -15'
```

---

## 📞 کمک و پشتیبانی

### لاگ‌ها

```bash
# مشاهده لاگ‌های فوری
sudo journalctl -u persian-asr -f

# ذخیره لاگ‌ها
sudo journalctl -u persian-asr > logs.txt
```

### سوالات متداول

**س**: چرا سریع نیست؟
**ج**: مدل `large` استفاده می‌کنید؟ به `small` یا `medium` تغییر دهید.

**س**: خطای حافظه می‌دهد؟
**ج**: `free -h` را اجرا کنید. اگر کم است، مدل کوچک‌تر استفاده کنید.

**س**: API به درستی کار نمی‌کند؟
**ج**: لاگ‌ها را بررسی کنید و اتصال را تست کنید.

---

## ✅ چک‌لیست نصب

بعد از نصب بررسی کنید:

- [ ] سرویس اجرا می‌شود: `systemctl status persian-asr`
- [ ] API پاسخ می‌دهد: `curl http://localhost:7070/health`
- [ ] لاگ‌ها در `/var/log/persian-asr/` هستند
- [ ] `/opt/persian-asr/.env` وجود دارد
- [ ] مدل Whisper دانلود شده است
- [ ] می‌توانید فایل صوتی تبدیل کنید

---

## 🎯 مرحله‌ی بعد

1. ✅ **راهنما را بخوانید** - `README-FA.md` را مطالعه کنید
2. ✅ **نصب کنید** - نصب‌کننده را اجرا کنید
3. ✅ **تست کنید** - API را تست کنید
4. ✅ **پیکربندی کنید** - تنظیمات را حسب نیاز تغییر دهید
5. ✅ **استفاده کنید** - در اپلیکیشن‌های خود یکپارچه کنید

---

## 📄 فایل‌های مهم

**اگر فقط 2 فایل بخوانید:**

1. **README-FA.md** - مستندات کامل فارسی
2. **INSTALLATION-GUIDE-FA.md** - نصب مفصل

---

**خدا خیر! 🙏**

**نسخه**: 2.0 Enhanced  
**تاریخ**: ۲۹ ژانویه ۲۰۲۶  
**نویسنده**: مهدی باغبان‌پور  
**وضعیت**: ✅ تولید آماده
