# QA Case Study: Login + Failed Attempts + Time-Based Lockout

## Overview
This case study presents a risk-based QA approach to testing a login flow.
The process is treated as a stateful system where failed attempts affect
authentication behavior.

The focus is on balancing:
- Security risks (brute-force, abuse)
- Business/UX risks (user frustration, lockout impact)

## Scope
- Login attempts (success / failure)
- Failed attempts counting
- Time-based delay (lockout) after failures
- Messaging behavior during lockout

## Start Event
User submits login credentials (email/username + password) and clicks "Login".

## Core Process (Process-Aware View)
1. User submits credentials.
2. System performs basic validation.
3. System authenticates credentials.
4. On authentication failure:
   - Failed attempt counter is incremented.
   - Time-based delay may be enforced based on system sensitivity.
5. On authentication success:
   - Access is granted.

## Key Gateways
### Gateway A: Are credentials valid?
- Yes → Login success
- No  → Failed attempt flow

### Gateway B: Sensitivity policy
Different systems apply different thresholds and delay strategies.

- **High-security systems**
  - N = 1 failed attempt
  - X = 2 minutes delay after each failure

- **Standard systems**
  - N = 3 failed attempts (example)
  - X = 2 minutes delay once threshold is reached

## End States
- Successful login
- Temporary lockout (delay active)
- Retry allowed after delay expires

## Key Risks Identified
### Security Risks
- Brute-force or credential-stuffing attacks
- User enumeration via error messages

### Business / UX Risks
- User frustration due to strict lockout
- Increased support load
- Potential user drop-off

## QA Insight
Lockout thresholds and delay duration are context-dependent.
QA responsibility is to verify correct behavior and make
security vs UX trade-offs visible for decision-making.

