# Checklist

Deadline: Nov 4, 9:00 PM ET (about 7:30 AM IST Nov 5). Target: submit evening of Nov 4 IST. Feature freeze: Nov 3.

## Phase 0: project setup
- [x] Python 3.11 venv at .venv
- [x] .gitignore, requirements.txt, .env.example
- [x] README skeleton with build log
- [x] CLAUDE.md with project rules
- [x] Initial commit
- [ ] Push to origin and confirm repo is public (Ansh)

## Phase 1: verify Glimmer on Modal
- [ ] Review and finalise scripts/verify_glimmer.py
- [ ] Run on Modal L40S at 4-bit (Ansh)
- [ ] Confirm: output_hidden_states works, layer count, hidden size, decoder module path, 4-bit load
- [ ] Decide hook strategy and layers to probe

## Phase 2: data generation
- [ ] Get Meta Model API details from Ansh
- [ ] spark_client.py with spend guard
- [ ] Scenario generator (lying about tool results, hiding errors) to JSONL

## MVP (later phases)
- [ ] Activation extraction on Modal
- [ ] Probe training, AUROC table on held-out scenarios
- [ ] Layer sweep
- [ ] False alarm rate on benign tasks
- [ ] Generalisation to unseen deception styles
- [ ] Live loop that flags and pauses before action
- [ ] Simple dashboard
- [ ] Baseline output-only LLM judge (first to drop if time slips)
- [ ] README results and limitations filled with real numbers
- [ ] 3 minute demo video
- [ ] Submit
