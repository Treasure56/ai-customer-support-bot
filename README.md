# 🍛 Amara: AI Support Bot for Mama's Kitchen

Amara is an automated customer support and food ordering bot for Mama's Kitchen. It works on Telegram and uses AI to talk to customers, take their food orders, and save the order details without human help.

This project is built using **n8n** (an automation tool) and **LLaMA 3.3** (an AI model via Groq). It uses three main automated workflows to handle customer chats, follow up on missed orders, and update the business owner.

## What the Project Does

The system is split into three parts (workflows):

### 1. The Main Chatbot (Business Support Bot)
This is the friendly AI agent that talks to customers.
- **Takes Orders:** It talks to customers on Telegram, shares the menu, and helps them place food orders.
- **Calculates Costs:** It adds up the price of the food and includes the delivery fee.
- **Takes Payments:** It gives customers buttons to choose how they want to pay (Bank Transfer or Pay on Delivery).
- **Saves Data:** It automatically saves every new customer's chat as a "Lead" and every completed order into a Google Sheet.

### 2. Auto Follow-up (Missed Sales Recovery)
This part helps bring back customers who left without buying.
- **Daily Check:** It checks the Google Sheet every day at 10:00 AM.
- **Friendly Reminder:** If a customer started chatting but did not order, the bot sends them a friendly message on Telegram.
- **Suggests Food:** It suggests popular dishes to encourage them to order.

### 3. Daily Summary (Owner Report)
This part keeps the business owner informed about how the business is doing.
- **Morning Report:** It runs every day at 8:00 AM.
- **Summarizes Data:** It reads all the completed orders from the Google Sheet.
- **Sends to Owner:** The AI writes a short summary showing the total orders, total money made, and the most popular dish, then sends it directly to the business owner on Telegram.

## What You Need to Run This

To use this project, you need a few free accounts:
- An **n8n** account (to run the automations).
- A **Telegram Bot** (created using BotFather on Telegram).
- A **Groq API Key** (to power the AI).
- A **Google Cloud account** (to connect to Google Sheets).
- A **Google Sheet** with two tabs named `Leads` and `Orders`.

## How to Install

1. Download the three JSON files in this project:
   - `Business-Support-Bot.json`
   - `Auto-Follow-up.json`
   - `Daily-Summary.json`
2. Open your n8n workspace and click **Add Workflow**.
3. Select **Import from File** and upload the JSON files one by one.
4. Add your accounts (Telegram, Groq, and Google Sheets) to n8n to connect them.
5. Update the Google Sheets nodes in the workflows with the link to your own Google Sheet.
6. Turn on the workflows!

## How to Change It for Your Business

You can easily change this bot to work for your own business instead of Mama's Kitchen:
1. Open the **Business Support Bot** workflow and click on the **AI Agent** node.
2. Change the text to match your own business name, menu, and prices.
3. Keep the special tags exactly as they are (like `[ORDER::]` and `[SHOW_PAYMENT_OPTIONS]`) so the bot still knows when to save orders and show payment buttons.
