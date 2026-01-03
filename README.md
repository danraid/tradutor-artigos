# Scientific Article Translator (Azure OpenAI)

A small, production-minded reference project that fetches a scientific/technical article from a URL, extracts clean text, and translates it using **Azure OpenAI**.

This repository is designed for **GitHub portfolio** presentation: it follows clean-code practices (PEP 8), includes lightweight tests, and demonstrates safe configuration via environment variables.

---

## Features

- **URL → Clean Text**: HTML fetching with timeouts + user-agent and robust text extraction (removes script/style/noscript).
- **Chunked Translation**: Splits long articles into chunks to fit LLM context windows.
- **Azure OpenAI (Chat Completions)**: Uses the official `openai` Python SDK configured for Azure.
- **Lightweight Tests**: Basic function validation without network calls (safe to run anywhere).
- **Security-minded**: No secrets in code. Credentials are loaded from environment variables.

---

## Tech Stack

- Python 3.10+
- Azure OpenAI (Chat Completions)
- `openai` Python SDK
- `requests`, `beautifulsoup4`

---

## Repository Structure

```
.
├── tradutor_de_arquivo_refatorado.ipynb   # Main notebook (clean, PEP 8, tests)
└── README.md
```

---

## Quick Start

### 1) Clone the repository

```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

### 2) Create a virtual environment (recommended)

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```

### 3) Install dependencies

```bash
pip install -U "openai>=1.40.0" requests beautifulsoup4 python-dotenv
```

> If you are using Azure ML / Databricks / Colab, install inside the notebook (first cell).

---

## Azure OpenAI Configuration

Create environment variables (recommended via a local `.env` file that you **do not commit**):

### Required

- `AZURE_OPENAI_ENDPOINT`  
  Example: `https://<your-resource-name>.openai.azure.com`

- `AZURE_OPENAI_API_KEY`  
  Your Azure OpenAI key

- `AZURE_OPENAI_DEPLOYMENT`  
  The **deployment name** of your chat model (for example, a `gpt-4o-mini` or similar deployment)

### Optional

- `AZURE_OPENAI_API_VERSION`  
  Defaults to `2024-02-15-preview` in the notebook. You may set another supported version used in your Azure resource.

Example `.env`:

```env
AZURE_OPENAI_ENDPOINT="https://my-resource.openai.azure.com"
AZURE_OPENAI_API_KEY="YOUR_KEY"
AZURE_OPENAI_DEPLOYMENT="gpt-4o-mini"
AZURE_OPENAI_API_VERSION="2024-02-15-preview"
```

---

## How to Run

Open and run the notebook:

- `tradutor_de_arquivo_refatorado.ipynb`

The notebook is divided into:

1. **Core functions** (fetch, extract, chunk, prompt)
2. **Local tests** (no Azure / no network)
3. **End-to-end pipeline** (requires internet access + Azure credentials)

To run the full pipeline, uncomment the end-to-end section:

- `text = extract_text_from_url(url)`
- `config = AzureOpenAIConfig.from_env()`
- `translated = translator.translate(text, target_language="pt-BR")`

---

## Testing

The notebook includes lightweight tests with `assert` statements for:

- HTML extraction (ensures scripts/styles are removed)
- Chunking logic
- Prompt building

Run the “Lightweight tests” cell and confirm:

```
All local tests passed.
```

---

## Notes & Limitations

- **Web scraping**: Some sites block automated requests; you may need to adjust headers or use an allowed source.
- **Token limits**: Chunking is character-based; for stricter control, you may integrate tokenization (e.g., `tiktoken`) as an enhancement.
- **Formatting**: Translation preserves headings and paragraphs best-effort; complex PDFs or heavily scripted pages may require a different extraction approach.

---

## Security

- Do **not** commit `.env` files, API keys, or endpoints that reveal sensitive details.
- Consider setting up Azure Key Vault for production deployments.

---

## License

Choose a license for your repo (MIT is common for portfolio projects). If you add one, mention it here.

---

## Acknowledgements

- Azure OpenAI Service
- OpenAI Python SDK
- BeautifulSoup (HTML parsing)
