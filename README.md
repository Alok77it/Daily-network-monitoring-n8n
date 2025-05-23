# 🚀 Daily Network Report Automation with n8n

This project automates a daily network report using [n8n](https://n8n.io), combining ping results, web interface screenshots, email reporting, and Telegram alerts for error handling.

## 📌 What This Workflow Does

✅ Pings multiple IPs (local and public)  
✅ Captures screenshots from password-protected web UIs  
✅ Sends a daily email with ping results and screenshots  
✅ Handles errors using IF nodes  
✅ Sends fallback Telegram alerts if email fails

---

## 📂 Workflow Overview

![Workflow Diagram](Daily-network-monitoring-n8n/assets/workflow-screenshot.png) 

### 🔁 Trigger

- **Cron Node**: Runs the workflow daily at `08:00 AM`

### ⚙️ Core Operations

1. **Ping Devices**  
   - IPs like `192.168.1.84`, `192.168.1.192`, `8.8.8.8`, etc., are pinged via `Execute Command` node.
   - Output is saved (stdout/stderr/exitCode).

2. **Capture Screenshots**  
   - Two HTTP Request nodes capture screenshots of:
     - `192.168.4.1`
     - `192.168.4.15`
   - URLs use embedded credentials (`http://user:pass@ip`).
   - Screenshot API is used: [`screenshotapi.net`](https://screenshotapi.net)

3. **Format Output (Code Node)**  
   - Combine ping and screenshot responses into a structured format.

4. **Send Email**  
   - Uses SMTP or Gmail node.
   - Email includes:
     - Ping results in the body
     - Screenshots as attachments

---
⚠️ Error Handling
 - An IF Node is used to check the result of the command.

 - The condition checks if the command output is empty:

  - ✅ Empty Output (True) → This means something went wrong → A Telegram alert is sent via bot.

  - ❌ Non-Empty Output (False) → This means the command worked fine → An Email with the result is sent.

This helps ensure you’re notified instantly if a command fails or returns nothing.

---

## 🛠️ Setup Instructions

### 1️⃣ Email Setup

See [`docs/email_setup.md`](Daily-network-monitoring-n8n/docs/email_setup.md)

### 2️⃣ Telegram Bot Setup

See [`docs/telegram_bot_setup.md`](Daily-network-monitoring-n8n/docs/telegram_bot_setup.md)

---

## 💡 Technologies Used

- [n8n.io](https://n8n.io)
- Screenshot API
- Gmail/SMTP
- Telegram Bot
- Bash/Command Line Utilities

---

## 🧑‍💻 Author

**Alok Trivedi**  
🔗 [GitHub](https://github.com/Alok77it)  
🔗 [LinkedIn](https://www.linkedin.com/in/alok-trivedi-27279a34b/)

---

## ⭐️ Star this repo if you find it helpful!
