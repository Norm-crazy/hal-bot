# HAL // Otacon

A personal AI assistant I designed and built myself. HAL runs on a small computer in my house, reads my email and calendar, searches my notes, writes documents, runs daily briefings, and talks back through a personality called Otacon, by text or by voice.

**[View the demo page →](https://norm-crazy.github.io/hal-bot/otacon_demo.html)**

## About this repo

This is the public portfolio page only: a static HTML page and a short recorded demo. There's no live model, no memory, and no personal data here. The working assistant runs privately at home and its code is not public.

## What HAL can do

- **Real tool use**: the model reads each request, picks the tools it needs and chains them, instead of following keyword rules
- **Layered memory**: recent conversation, a stable profile, and semantic search across notes and documents, with embeddings running locally
- **Email, calendar and Drive**: reads, searches and drafts on request
- **Voice**: push-to-talk codec interface with an avatar that reacts to the conversation
- **Background jobs**: daily inbox and calendar briefings, marked delivered only once they actually arrive
- **Nothing saved without a yes**: changes to stored notes are shown word for word and wait for approval
- **Swappable brains**: Claude by default, a local model in Decryption Mode, or the paid API only when chosen manually; Otacon's personality stays the same

## Architecture

```
  web · voice · chat
          │
   ┌─────────── HAL core ───────────┐
   │ memory · tools · safety rules  │
   └───────────────┬────────────────┘
                   │ same prompt, same tools
   ┌──────── brain adapter ─────────┐
   │ Claude │ local model │ paid API │
   └────────────────────────────────┘
          Otacon, the personality
```

Every interface is a thin doorway into one core function. The model doing the thinking is a plug: switching it can't change Otacon's personality, memory, tools or permissions.

## Safety

- Reading, searching and drafting happen on request; anything permanent waits for explicit approval
- The paid API never kicks in silently; HAL asks before switching
- Secrets stay in `.env` and are never committed
- Every change is made on a branch with a tagged checkpoint and has to pass behavior tests before it ships

## Tech stack

Python · FastAPI · Claude API · Ollama · Google OAuth2 · local embeddings · WSL Ubuntu on an Intel NUC

## What's next

- Moving HAL's tools into a standard tool layer (MCP) so any brain can use them
- A local model that acts like a real agent, not a script
- A phone app, and secure remote access over a private VPN
- A voice-only smart mirror

---

Built by **Norman Higgs** · [LinkedIn](https://www.linkedin.com/in/norm-higgs) · [GitHub](https://github.com/Norm-crazy) · [Email](mailto:nhiggsit@gmail.com)
