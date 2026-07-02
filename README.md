# 📧 Visto. An AI Telegram Email Assistant

An automated Telegram bot built on Make.com that acts as a smart bridge between your inbox and an AI model. It reads incoming emails, processes them with situational awareness, and delivers concise summaries and responses directly to your Telegram chat.

[https://true-acknowledgment-792318.framer.app/
](url)

## 🏗 Architecture & Stack
* **Frontend/UI:** Telegram Bot API
* **Integration Engine:** Make.com (No-Code Blueprints)
* **Authentication:** Manual Credential Provisioning via Make.com native connections
* **Intelligence:** [Make AI] 

## 🧠 Core Engineering Decisions

### 1. Smart Memory Compression (Token Optimization)
Instead of passing the entire raw email history to the AI—which causes token costs to snowball exponentially—this architecture relies on a **sliding window of context**.
* The database stores a `text` variable containing only the AI's *previous summaries*.
* When a new email arrives, the prompt fed to the AI is strictly: `[previous_text_summary] + [new_raw_email]`.
* The AI returns an updated situational summary, which overwrites the database. The raw email is discarded.

### 2. The 8:00 AM Daily Reset & Digest
To prevent the loss of late-night communications while maintaining a clean context window:
* At 8:00 AM, a scheduled scenario checks the database.
* If there is accumulated context from the night before, it delivers a "Morning Digest" to the user on Telegram.
* Immediately after delivery, the database text field is wiped clean to start the new workday fresh.

## 📂 Repository Contents
* `/blueprints`: Contains the `.json` exports of the Make.com scenarios. You can import these directly into your Make account to replicate the visual architecture.

## 🗄️ Database Structure (Make Data Store)
To run these blueprints, you must create a Data Store in Make.com with the following exact structure:
* `chat_id` (Primary Key / String) - *Maps to the Telegram User ID.*
* `text` (Text) - *Updated dynamically by the AI (Daily Memory).*
* `date` (Date) - *Timestamp (Inactive/For future iteration usage).*

## 🚀 Quick Setup
1. Import the `.json` blueprints into Make.com.
2. Create the Make Data Store using the structure above.
3. Link your Telegram Bot token via BotFather.
4. Connect your Mail in the respective module (Gmail/Outlook native Make connection).
