# Supabase Vector‑Store Ingestion & Chat – n8n Workflow

**Purpose**  
Automatically ingest new documents from Google Drive into a Supabase‑backed vector store and enable RAG (Retrieval‑Augmented Generation) chat over the content.

Pipeline:

1. **Google Drive Trigger** – fires on new / updated files.  
2. **Google Drive** – downloads the file.  
3. **Extract from File** – pulls raw text (PDF, DOCX, TXT).  
4. **Character Text Splitter** – chunks long text.  
5. **OpenAI Embeddings** – converts chunks to vectors.  
6. **Supabase Vector Store** – upserts embeddings (+ metadata).  
7. **Chat Trigger** + **AI Agent** – answers user questions by retrieving relevant chunks and forwarding them to the LLM.

---

## Importing

1. Import `vector_store_public.json` into n8n.
2. Fill in credentials (see below).

---

## Required credentials & env vars

| Node / Service               | What you need                              |
|------------------------------|--------------------------------------------|
| **Google Drive**             | OAuth2 credentials with `drive.readonly`.  |
| **Supabase Vector Store**    | `SUPABASE_URL`, `SUPABASE_SERVICE_KEY`.    |
| **OpenAI Embeddings**        | `OPENAI_API_KEY`.                          |

All placeholders like `YOUR_API_KEY` / `YOUR_ID` must be replaced.

---

## Supabase table schema (quick reference)

```sql
create table match (
  id uuid primary key default uuid_generate_v4(),
  content text,
  metadata jsonb,
  embedding vector(1536)
);
```
You can adapt to your own naming; just match the node parameters.

---

## Testing locally

* Drop a file into the watched Drive folder – the workflow ingests it in seconds.  
* Send a chat message (e.g., via the built‑in webhook) – it should answer using the stored knowledge.

---

## Security

This public JSON **contains no secrets** (scrubbed on 2025-06-19).  
Keep your API keys in n8n credentials, not hard‑coded.

---

## License

MIT
