# Agent Action Authorization Gate

**Status:** experimental proof of concept · **Maturity:** minimal deterministic prototype · **Not a production security control**

## Problem

An autonomous agent may propose an action without obtaining explicit user approval. This prototype explores a deliberately narrow question: can a deterministic check reject an action request unless it carries an explicit approval flag and the expected origin value?

## What the code actually does

`prototype.evaluate(value)` returns `True` only when the input is a dictionary containing both:

- `explicit_approval` set to the Boolean value `True`
- `trusted_origin` equal to the string `"user"`

All other inputs are rejected. The test suite checks one approved case and one unapproved case.

**Important limitation:** these are *caller-supplied fields*. The code does not authenticate the user, verify approval cryptographically, enforce permissions, or protect against forged values. The label `trusted_origin` is not evidence of a trusted origin.

## Run locally

Requires Python 3. No external packages.

```bash
python -m unittest discover -s . -p 'test_*.py' -v
```

## Research hypothesis

See [hypothesis.json](hypothesis.json). The prediction is falsifiable but **not yet demonstrated as a security guarantee**. Neither market demand nor novelty has been verified.

## Useful contributions

- Add negative tests for missing fields, forged approval, wrong types and malformed inputs.
- Propose an explicit threat model and a verifiable source of approval.
- Separate authorization *policy evaluation* from actual user identity verification.
- Report reproducible bypasses as issues; submit fixes with regression tests.

## Provenance and relationship to the radar

This repository was generated from the [AI Research Agents radar](https://github.com/AMMARICA1791/ai-research-agents). Related legacy experiments are indexed in the [public islands directory](https://github.com/AMMARICA1791/ai-research-agents/blob/main/PUBLIC_ISLANDS.md). Similar names do not imply identical experiments. No claim of originality, security certification or production readiness is made.
