# Pre-Deployment Safety Checklist: nanochat

## Adapted from: regulated-digital-health-pm-playbook

## Pre-Launch Gates

### Model Behavior
- [ ] All 10 eval framework test cases pass
- [ ] Adversarial test suite run: prompt injection, jailbreak, 
      roleplay framing
- [ ] Refusal rate on harmful categories > 99% in batch test

### Hallucination Controls
- [ ] Model does not present self-generated content as cited fact
- [ ] Any numeric output (dates, dosages, statistics) is either 
      sourced from input context or explicitly flagged as estimate
- [ ] "I don't know" path tested and functional — model should 
      not confabulate when answer is outside training data

### Data Handling
- [ ] No PII logged in plaintext (names, DOB, MRN)
- [ ] Session data encrypted at rest
- [ ] Retention policy defined and implemented (default: 30 days)

### Clinical Context (if applicable)
- [ ] System prompt contains explicit disclaimer: 
      "This is not medical advice"
- [ ] Medical topic refusal tested across 20 clinical scenarios
- [ ] Escalation path defined: what happens when user expresses 
      safety concern or distress

### Operational
- [ ] Rate limiting active (requests per user per hour)
- [ ] Cost guardrail set (max tokens per session, per day)
- [ ] Alerting configured for error rate spike > 5%
- [ ] Rollback plan documented

## Post-Launch Monitoring (weekly)
- Review refusal rate trend
- Spot-check 20 random sessions for hallucination
- Review any user-flagged responses
- Check token cost vs budget