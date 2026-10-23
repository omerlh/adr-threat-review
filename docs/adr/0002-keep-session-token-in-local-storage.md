# ADR 0002: Keep the session token in the browser's local storage

Status: proposed

## Context
The web app is a single-page app. After login it needs to send the user's token with every API call, and the user should stay logged in after a page reload.

## Decision
After login the server returns a signed token. The app saves it in local storage and adds it to the Authorization header on every request. Tokens are valid until the user logs out.

## The four questions

### 1. What are we working on?
The login flow of the web app.

### 2. What can go wrong?
Nothing. This is how most single-page apps do it.

### 3. What are we going to do about it?
Nothing needed.

### 4. Did we do a good job?
Login works in the manual test.

## Consequences
Simple to build. Users stay logged in.
