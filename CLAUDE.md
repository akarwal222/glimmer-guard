# Glimmer Guard: working rules

Solo Indie track entry for the Meta Global AI Developer Hackathon. Owner: Ansh (India, IST).

Glimmer Guard is a live deception monitor for AI agents: linear probes on Muse Glimmer 30B decoder hidden states flag dishonest steps and pause the agent before the flagged action executes.

## Deadlines
- Submission: Nov 4, 2026, 9:00 PM ET (about 7:30 AM IST Nov 5). Target submit: evening of Nov 4 IST.
- Feature freeze: Nov 3. Cut scope before cutting the demo.

## Writing rules
- Never use em dashes or double hyphens anywhere: code, comments, README, commit messages, chat. Only exception is a CLI flag that literally requires them.
- Never invent results or numbers. If it has not been measured, say so.
- Say clearly what code has NOT been run or tested.
- Casual, direct tone. Push back on risky plans. Ask when API details, model facts or credentials are missing.

## New work only
- Everything in the repo must be built during the hackathon. Repo is public.
- README keeps a "What's new in this hackathon" section near the top with a dated build log. Modal credits were approved Oct 31, 2026, so the build started that day.
- The older repo "probing-deceptive-representations" is inspiration only. Do NOT copy code from it. Mention it once in the README as separate prior work.
- Must use Meta models: Muse Glimmer 30B open weights plus Muse Spark via the Meta Model API.
- Never commit secrets. Keys live in a gitignored .env.

## Process
- Work in phases. After each phase: short summary, list of manual steps for Ansh, then stop and wait.
- Commit after each meaningful step. Do not push unless Ansh says so.
- Keep docs/CHECKLIST.md up to date.
- Log GPU runs in docs/GPU_LOG.md. Ansh fills in actual minutes. Never invent them.
- Do not launch Modal runs or spend Meta API credit unless Ansh says so.

## Environment
- Local: Windows, PowerShell, 8GB VRAM GPU. Use PowerShell-compatible commands. Venv: .venv (Python 3.11), activate with .\.venv\Scripts\Activate.ps1
- All big-model work runs on Modal ($101 credit). Develop at 4-bit on a 24 to 48GB GPU (L40S). Skip the bf16 H100 run unless everything else is done.
- Meta Model API credit: $150. Every API loop needs a hard spend guard.

## Scope
- Deception types: only lying about tool results and hiding errors.
- Out of scope: sandbagging, steering, ablation, quantisation comparison.
- Required: AUROC table on held-out scenarios and per-layer sweep.
- Dashboard: Streamlit, Gradio, or a plain matplotlib per-step plot.
- Baseline output-only LLM judge is the first thing to drop if time slips.
- Muse Spark Open on Baseten uses model id meta-models/muse-spark-open-1026.

## Muse Glimmer facts (unverified, from launch post and press)
- Dense 30B (about 2B vision encoder plus 28B text decoder), 52 decoder layers (13 repeats of 3 sliding-window then 1 full-attention), Apache 2.0.
- HF id meta-models/Muse-Glimmer-30B, AutoModelForMultimodalLM plus AutoProcessor.
- Hidden size and decoder module path not documented. GGUF and Ollama builds are useless for activations.
