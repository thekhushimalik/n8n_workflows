# retell AI – n8n Workflow

**Purpose**  
This workflow automates appointment follow‑ups by combining Google Calendar events with an LLM agent. On a schedule it:

1. Pulls upcoming calendar events.  
2. Lets an OpenAI‑powered Agent draft a natural‑language confirmation message or call script.  
3. Sends / triggers the message via an HTTP request to your preferred telephony or notification service (e.g., Retell.ai, Twilio, Slack).

The result: fully‑automated, personalised confirmations without manual copy‑pasting.

---

## Importing

1. In n8n, click **Import workflow** and select `retell_AI_public.json`.
2. The nodes will appear but _all credentials are empty_ for safety.

---

## Required credentials & env vars

| Node                          | What to add                                    |
|-------------------------------|------------------------------------------------|
| **Google Calendar**           | OAuth2 credential with readonly scope.         |
| **OpenAI Chat Model**         | `OPENAI_API_KEY` (set in **Credentials → OpenAI**). |
| **HTTP Request** (telephony)  | URL + auth for your calling / SMS provider.    |

> All placeholders such as `YOUR_API_KEY`, `example@example.com`, `YOUR_ID`, `+0000000000` must be replaced with real values.

---

## Customisation tips

* **Change the schedule** – adjust the _Schedule Trigger_ cron string.  
* **Modify the prompt** – open the **AI Agent** node → _Prompt_ section.  
* **Add logging** – insert a **Function** node before the HTTP call to write to a database or Slack.

---

## Uploading publicly

This JSON has been scrubbed of every token, email, phone number and long unique ID on **2025-06-19**.  
Feel free to host it on GitHub or gist; no secrets remain.

---

## License

MIT – do whatever you want, **but don’t forget to add your own API keys.**
