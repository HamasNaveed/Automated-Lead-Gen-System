🔗 n8n LinkedIn & Email Outreach Automation
📌 Overview
This n8n workflow automates personalized cold outreach by:

Reading lead data from Google Sheets

Using OpenAI to generate personalized LinkedIn and email messages

Sending:

LinkedIn messages via Airtop.io

Emails via Gmail (if email is available)

⚠️ Disclaimer: This automation is for educational and research purposes only. Automated LinkedIn messaging (especially through third-party tools like Airtop) can violate LinkedIn’s Terms of Service. Use responsibly and at your own risk.

🧩 Prerequisites
🔧 n8n installed and running

🧠 OpenAI API Key

📄 Google Sheets connected (using OAuth credentials)

📬 Gmail account connected

🛜 Airtop.io profile (optional)

🔗 Lead data in Google Sheets with:

Creator Name

Startup Title

LinkedIn URL

Email (optional)

📁 Sheet Format
Creator Name	Startup Title	LinkedIn URL	Email
Jane Doe	EcoBattery Innovations	https://linkedin.com/in/janedoe	jane@ecobatt.com
John Smith	AI Healthwatch	https://linkedin.com/in/jsmith	(leave blank if none)

🔄 Workflow Steps
1. Read Leads from Google Sheet
Use Google Sheets Node

Pull rows with fields like Creator Name, Startup Title, LinkedIn URL, Email

2. Generate Personalized Message (OpenAI)
Use AI Agent Node

System prompt:

You are a helpful marketing assistant. Generate a short, warm, and personalized cold message for LinkedIn or email. Use under 500 characters for LinkedIn messages. Return valid JSON.

Output Parser JSON:

json
Copy
Edit
{
  "type": "object",
  "properties": {
    "email_subject": {
      "type": "string",
      "description": "Subject line for cold email"
    },
    "email_body": {
      "type": "string",
      "description": "Full body of email"
    },
    "linkedin_message": {
      "type": "string",
      "description": "Short, warm message for LinkedIn DM"
    }
  },
  "required": ["email_subject", "email_body", "linkedin_message"]
}
3. Send Message
If Email is available:

Use Gmail Node to send email with subject & body

If LinkedIn URL exists:

Use Airtop API or HTTP Request Node to send message

Add delay (15–60s) to reduce risk of detection

Warn in logs about LinkedIn ToS

⚠️ Important Notes on LinkedIn Messaging
LinkedIn strongly discourages automation.

Using tools like Airtop or Apify for messaging can:

Lead to account warnings

Result in temporary or permanent bans

If you proceed:

Limit message frequency (5–10/day max)

Rotate LinkedIn accounts

Add random delays between actions

✅ Optional Features
Webhook trigger for real-time sheet monitoring

Add to Airtable or Notion for logging

Email verification (e.g., NeverBounce API)

CRM integration (e.g., HubSpot)

📌 Summary
Step	Tool	Description
1	Google Sheets	Read data from sheets
2	OpenAI Agent	Generate personalized message
3a	Gmail	Send cold email
3b	Airtop.io	Send LinkedIn message (optional)

📢 Final Warning
Automated messaging on LinkedIn is against their terms. This system is meant for research purposes, to learn how lead generation workflows work using free and open tools like n8n and OpenAI.
