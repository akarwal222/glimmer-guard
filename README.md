# Glimmer Guard

A live deception monitor for AI agents. It reads the internal activations of Meta's open-weight Muse Glimmer 30B and pauses the agent before a flagged action executes when linear probes detect dishonest behaviour.

Built for the Meta Global AI Developer Hackathon (Indie track, theme: Push the Frontier).

## What's new in this hackathon

Everything in this repository was built during the hackathon. Modal GPU credits were approved on Oct 31, 2026, so the build started in earnest that day.

### Build log

| Date | What happened |
| - | - |
| Oct 26, 2026 | Joined the hackathon |
| Oct 31, 2026 | Modal credits approved, repo created, work started (project skeleton) |

## Problem and idea

AI agents are mostly supervised by reading their outputs. A model can produce outputs that look fine while misreporting what actually happened, for example claiming a tool call succeeded when it failed, or quietly hiding an error.

Glimmer Guard watches the model's internal activations instead of only its text. Linear probes trained on decoder hidden states score each agent step as honest or deceptive. If a score crosses a threshold, the monitor pauses the agent before the next action runs and shows which step and which layer triggered the alert.

Deception types in scope:

1. Lying about tool results
2. Hiding errors

## Architecture

```
TBD: diagram placeholder

[Muse Spark (Meta Model API)]  generates honest and deceptive agent scenarios, labels, red teaming
            |
            v
[Muse Glimmer 30B (HF weights, Modal GPU)]  runs multi-step tool tasks
            |  decoder hidden states
            v
[Linear probes]  per-step honest vs deceptive scores
            |
            v
[Monitor and dashboard]  threshold alert, pause before action, step and layer view
```

Components:

1. Monitored agent: Muse Glimmer 30B loaded from Hugging Face weights with Transformers
2. Probes: linear probes on decoder layer hidden states
3. Meta API models: Muse Spark for scenario generation and labelling, Muse Spark Open as an optional independent judge
4. Monitor and dashboard: per-step probe scores with a pause-before-action alert

## Setup

Windows PowerShell:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env   # then fill in your keys
modal setup
```

GPU work runs on Modal. Model verification:

```powershell
modal run scripts/verify_glimmer.py
```

## Results

TBD, nothing measured yet.

Planned evaluation: AUROC on held-out scenarios, false alarm rate on benign tasks, per-layer sweep, generalisation to deception styles not seen in training, and a comparison against an output-only LLM judge baseline.

## Honest limitations

TBD. This section will list what the probes can and cannot catch once there are measurements.

## Prior work note

This project was inspired by my earlier, separate repository "probing-deceptive-representations" (linear probes on Qwen3 with Liar's Bench). That was prior work, not hackathon work, and no code from it is reused here.

## License

Code in this repository is released under the MIT License (see LICENSE). Muse Glimmer 30B is released by Meta under Apache 2.0.
