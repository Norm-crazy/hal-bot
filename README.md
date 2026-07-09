Otacon

A personal AI assistant built from scratch on the Claude API — persistent memory, multi-channel access, and real task execution, with safety rails designed in from day one.

Live demo — codec-style interface, real footage, no live model calls.


What this is

Otacon (codename: HAL) started as a Discord bot and grew into a full assistant reachable through chat, a web UI, and email — all backed by a single interface-agnostic core. This repo is the public portfolio version: a static, scripted shell that shows the architecture and a real recorded demo, with no live model access, no memory, and no personal or career data. The private, fully-functional version (hal-bot) runs separately and is not public.

What it does


Persistent memory — short- and long-term context that survives across conversations
Gmail integration — OAuth2-scoped inbox reading and search, with CDT timezone-aware summaries
Document generation — PDF, Word, and plain-text output on request
Custom web interface — an MGS-style codec UI: reactive portraits, emotion tags, codec sounds
Discord-native — the original interface, still fully supported
Cost-aware routing — cheaper models handle casual messages, stronger models handle complex ones, with prompt caching to cut repeated-context cost


Architecture

One core function (hal.py) handles every request and returns a reply, an emotional state, and any generated document. Every interface — Discord, web, voice (in progress) — is a thin adapter that calls the same brain. New interfaces plug in without touching the logic underneath.

Discord ─┐
Web UI   ─┼──▶  hal.py (core brain)  ──▶  Claude API
Voice*   ─┘            │
                        ├── memory store
                        ├── Gmail (OAuth2, read/draft-scoped)
                        └── document generator (PDF/Word/TXT)

*in progress

Safety model

Read, summarize, and draft actions happen autonomously. Anything irreversible — sending an email, deleting a file, spending money — waits for explicit approval. Secrets live in .env (never committed), OAuth scopes are least-privilege, and every data access is logged.

Tech stack

Python · FastAPI · discord.py · Claude API · Google OAuth2 · reportlab / python-docx · WSL Ubuntu

Roadmap

StatusPhase✅Discord bot foundation✅Short- and long-term memory✅Claude-backed reasoning + personality✅Codec-style web UI✅Gmail integration🟡Document generation — built, wiring into live chat🔴Voice mode (ElevenLabs + Whisper)🔴Hybrid local/cloud inference (Ollama)🔴Dedicated home server + always-on access

About this repo vs. the private assistant

otacon-bot (this repo)hal-bot (private)PurposePortfolio showcasePersonal assistantModel accessNone — scripted responses onlyLive Claude APIMemoryNoneFull persistent memoryDataNo personal/career dataFull email, calendar, Discord access


Built solo, end to end — API integration, system design, memory architecture, and public/private environment separation.
