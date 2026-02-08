# Test Scenarios – Login & Lockout

## A) Happy Path
- Valid credentials → access granted

## B) Validation
- Empty username or password
- Invalid input format

## C) Failed Authentication
- Wrong password increments failed attempt counter
- Counter persists across attempts

## D) High-Security Policy (N=1, X=2 min)
- Single failure triggers delay
- Login blocked during delay
- Login allowed after delay expires

## E) Standard Policy (N=3, X=2 min)
- First and second failures allow retry
- Third failure triggers delay
- Retry blocked during delay

## F) Messaging & Security
- Error messages do not reveal account existence
- Lockout message is clear but not overly detailed

## G) Post-Success
- Successful login resets failed attempt counter (if required)
