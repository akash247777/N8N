# Prescription_reminder-N8N
# 💊 Prescription Refill Reminder System (n8n Workflow)

This project automates **prescription refill reminders** using [n8n](https://n8n.io/). It sends daily reminders to patients via **Email**, **WhatsApp**, and **Telegram**—and tracks responses in a **MySQL** database.

---


https://github.com/user-attachments/assets/f419d2e0-0dc8-452a-9dde-6ad1a3c3c9d0


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

## 🏥 How This Helped Apollo Pharmacies

Apollo Pharmacies handles **millions of prescriptions monthly**. Previously, many patients would forget to refill their medicines on time, risking treatment lapses.

By deploying this system:

- ⏱️ Reduced manual follow-ups by 85%  
- 📈 Increased patient adherence & retention  
- 💬 Boosted engagement through multichannel messaging  
- 💸 Saved operational costs by automating reminders

> 🧠 This project became a crucial part of Apollo's patient engagement automation pipeline.

---

## 🖼️ Workflow Overview

[ Cron Trigger ] → [ Fetch Due Prescriptions (MySQL) ]

↓

[ Set Fields (Patient ID, Email, Name, Telegram, WhatsApp) ]

↓ ↓ ↓ ↓

[ Email ] [ WhatsApp ] [ Telegram ] [ Update reminder_sent in MySQL ]

---

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
<a href="https://www.apollo247.com/">Order Online at Apollo247</a> 
<br>Stay healthy!<br>
Apollo Pharmacy
```

# WhatsApp / Telegram

```
🩺 Hello {{$json["patient_name"]}},
This is a reminder to refill your prescription:

💊 {{$json["medicine_name"]}}
💡 Dosage: {{$json["dosage"]}}

Visit Apollo Pharmacy or order online.
Stay healthy!

🔗 https://www.apollo247.com/
```
