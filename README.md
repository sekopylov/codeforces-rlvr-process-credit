# Codeforces RLVR process-credit study

## Question

In Codeforces RLVR, the final C++ program receives a verifier outcome, while the preceding reasoning trace may contain both useful decisions and mistakes. Can an evaluator with access to an editorial help locate useful reasoning steps without giving that privileged information to the student?

## What I tested

- A sparse privileged on-policy distillation teacher on student-generated trajectories. It learned some accepted-versus-rejected ranking, but held-out quality and local credit assignments were not reliable enough to claim a useful student-training signal.
- A scalar prefix-value teacher trained from final verifier labels. On a balanced random-trajectory validation view, giving this teacher editorial context improved prediction of final acceptance compared with a public-prompt ablation.
- Manual audits of value changes on reasoning fragments, followed by a 20-trajectory span-label benchmark. The value trace sometimes highlighted useful algorithmic decisions, but value-only rules were too inaccurate to serve as automatic process-credit labels.

**Scope:** These are teacher-evaluation results. This project did not demonstrate an improvement in the student model from using the proposed process-credit signal. The main value-teacher comparison is on held-out trajectories, not a demonstrated problem-disjoint generalization result.

## Evidence

- [English research report](codeforces-process-credit-report.pdf) — the June 2026 project report, including methods, figures, and a technical appendix.
- [Evaluation log](evaluation-log.md) — a public summary of the measured value-teacher ablation and the later span-label audit, including negative results omitted from the original report.

The report is an archive of the June 2026 study. Its literature review and novelty discussion reflect that date; for related subsequent work, see [Le Critique: Privileged Value Functions for LLM Reinforcement Learning](https://arxiv.org/abs/2608.16739). This repository does not contain the private training infrastructure, raw student trajectories, or annotated benchmark rows, so the published files document results rather than provide a fully reproducible release.

