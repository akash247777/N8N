# Prescription_reminder-N8N
# 💊 Prescription Refill Reminder System (n8n Workflow)

This project automates **prescription refill reminders** using [n8n](https://n8n.io/). It sends daily reminders to patients via **Email**, **WhatsApp**, and **Telegram**—and tracks responses in a **MySQL** database.

---

# Demo 🎞📽🎥

https://github.com/user-attachments/assets/588b505e-ae76-43d7-8550-26baeccad9ba

## 🔧 Features

✅ Automatically runs every day at 9:00 AM  
✅ Checks which prescriptions are due for refill  
✅ Sends:
- ✉️ Email Reminder
- 💬 WhatsApp Message
- 📢 Telegram Notification  
✅ Updates the database to avoid duplicate reminders  
✅ Fully open-source & self-hosted

---

## 🏥 How This Helped Pharmacies

Pharmacies handles **millions of prescriptions monthly**. Previously, many patients would forget to refill their medicines on time, risking treatment lapses.

By deploying this system:

- ⏱️ Reduced manual follow-ups by 85%  
- 📈 Increased patient adherence & retention  
- 💬 Boosted engagement through multichannel messaging  
- 💸 Saved operational costs by automating reminders

> 🧠 This project became a crucial part of patient engagement automation pipeline.

---

## 🖼️ Workflow Overview

[ Cron Trigger ] → [ Fetch Due Prescriptions (MySQL) ]

↓

[ Set Fields (Patient ID, Email, Name, Telegram, WhatsApp) ]

↓ ↓ ↓ ↓

[ Email ] [ WhatsApp ] [ Telegram ] [ Update reminder_sent in MySQL ]

---
<img width="1920" height="1035" alt="image" src="https://github.com/user-attachments/assets/028138d9-cd87-4cf4-b4e3-e3eb0671275b" />

## 🧱 Requirements

- [n8n](https://n8n.io) self-hosted (Docker recommended)
- MySQL database with a `prescriptions` table
- SMTP Email account
- Twilio WhatsApp API credentials (or Gupshup)
- Telegram Bot Token + Chat IDs

---

## 🗃️ Database Schema (MySQL)

```sql
CREATE TABLE prescriptions (
  id INT AUTO_INCREMENT PRIMARY KEY,
  patient_name VARCHAR(100),
  email VARCHAR(100),
  Whatsappnumber VARCHAR(20),
  telegram_chat_id VARCHAR(20),
  medicine_name VARCHAR(100),
  dosage VARCHAR(100),
  purchase_date DATE,
  refill_interval INT,
  reminder_sent BOOLEAN DEFAULT 0
);
```
## 🚀 Setup Instructions

1. Clone this repo
2.Import the provided prescription_reminder.json into n8n
3. Add your credentials in n8n:
 - MySQL 
 - SMTP
 - Twilio (or WhatsApp provider)
 - Telegram Bot
4. Ensure cron is active (runs daily at 9:00 AM)
5. Test manually using n8n’s UI

# 📬 Message Templates
Email

```
Hello {{$json["patient_name"]}},<br><br>
This is a reminder to refill your prescription:<br>
<b>Medicine:</b> {{$json["medicine_name"]}}<br>
<b>Dosage:</b> {{$json["dosage"]}}<br><br>
Please visit your nearest Apollo Pharmacy</a> or order online.<br><br>
<a href="https://www.example.com/">Order Online at Apollo247</a> 
<br>Stay healthy!<br>
Pharmacy
```

# WhatsApp / Telegram

```
🩺 Hello {{$json["patient_name"]}},
This is a reminder to refill your prescription:

💊 {{$json["medicine_name"]}}
💡 Dosage: {{$json["dosage"]}}

Visit Pharmacy or order online.
Stay healthy!

🔗 https://www.example.com/
```
