# 🍛 Amara: AI Support Bot for Mama's Kitchen

An intelligent, fully automated customer support and food ordering Telegram bot built using **n8n**, **LangChain**, and **LLaMA 3.3** (via Groq). 

This bot acts as a warm, friendly customer service agent named "Amara". It handles natural conversations, processes food orders based on a strict menu, calculates delivery fees, provides interactive payment options, and automatically logs leads and confirmed orders to Google Sheets.

## ✨ Features

- **Conversational AI**: Powered by LLaMA 3.3 70B (via Groq) for lightning-fast, human-like responses.
- **Strict Business Logic**: The agent is bound by strict prompt engineering to adhere to specific menus, pricing, opening hours, and delivery constraints.
- **Interactive UI Elements**: Seamlessly transitions from unstructured AI chat to structured Telegram inline keyboards for secure payment selection (Bank Transfer vs. Pay on Delivery).
- **Automated CRM**: Automatically syncs with Google Sheets:
  - **Leads Tracking**: Logs every new user interaction to track potential customers.
  - **Order Management**: Extracts structured data (Name, Order, Phone, Total Amount) from natural language and logs confirmed orders instantly.
- **Smart Logic Routing**: Uses invisible backend tags (`[SHOW_PAYMENT_OPTIONS]`, `[ORDER::...]`) to bridge the gap between unstructured LLM outputs and deterministic n8n logic.

## 🛠️ Architecture 

This project is a no-code/low-code workflow built in **n8n**. The core logic flows as follows:

1. **Telegram Trigger**: Listens for incoming messages or callback queries (button clicks).
2. **LangChain Agent**: Processes user input alongside a 50-message conversational memory buffer.
3. **Regex Interceptors**: n8n monitors the LLM's output for specific hidden triggers:
   - If the AI generates `[SHOW_PAYMENT_OPTIONS]`, n8n intercepts the message and presents Telegram Inline Buttons to the user.
   - If the AI generates an `[ORDER::...]` string, n8n extracts the data using regex and appends it to the Google Sheets database.
4. **Google Sheets Integration**: Handles database operations via Service Accounts.

## 🚀 Getting Started

### Prerequisites
To import and run this workflow, you will need:
- An active [n8n](https://n8n.io/) instance (Cloud or Self-Hosted).
- A **Telegram Bot Token** (via BotFather).
- A **Groq API Key** (for the LangChain chat model).
- A **Google Cloud Service Account** with access to the Google Sheets API.
- A blank Google Sheet with two tabs: `Leads` and `Orders` (ensure column headers match the workflow mapping).

### Installation
1. Download the `Business Support Bot.json` file.
2. Open your n8n workspace and click **Add Workflow**.
3. In the top right menu, select **Import from File** and select the downloaded JSON.
4. Set up your credentials:
   - Connect your Telegram Bot.
   - Connect your Groq account.
   - Connect your Google Sheets account.
5. Update the Google Sheets node with your specific Document ID.
6. Activate the workflow!

## 📝 Customization

To adapt this bot for your own business:
1. Open the **AI Agent** node.
2. Modify the **System Message** to reflect your business name, persona, menu/services, and pricing.
3. Ensure you maintain the exact formatting rules for the `[ORDER::]` and `[SHOW_PAYMENT_OPTIONS]` tags within your new prompt.
