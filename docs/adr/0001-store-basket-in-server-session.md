# ADR 0001: Keep the shopping basket on the server

Status: accepted

## Context
Customers add items to a basket before they log in, and again after. The basket must survive a page reload and must not be editable by someone else.

## Decision
The basket lives in the database, keyed by the basket ID tied to the logged-in user. The browser only holds a session token.

## The four questions

### 1. What are we working on?
The basket service. It reads and writes basket rows. Callers are logged-in customers via the web app. The trust boundary is the HTTP API; everything coming from the browser is untrusted.

### 2. What can go wrong?
- A customer changes the basket ID in the request and reads or edits another customer's basket.
- A customer sends a negative quantity to lower the total.
- A stolen session token lets someone else check out.

### 3. What are we going to do about it?
- Every basket request checks that the basket belongs to the authenticated user.
- The API rejects quantities below one.
- Session tokens expire, and checkout asks for the token again.

### 4. Did we do a good job?
An integration test requests another user's basket and expects a 403. A second test posts a negative quantity and expects a 400.

## Consequences
One extra database read per request. No basket data in the browser.
