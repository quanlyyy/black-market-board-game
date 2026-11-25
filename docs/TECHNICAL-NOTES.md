# Technical notes

## Production shape
The same Node process serves the built Vite application and the Socket.IO endpoint. The host-provided PORT is used. Vite's development server proxies WebSocket traffic to localhost:3001. Render blueprint config is in render.yaml.

## Game state
The current authoritative state is in process memory. Room codes are six hex characters; reconnect credentials are player UUID + game UUID stored in browser localStorage. This is suitable for a private prototype only. It is not durable across server restarts or safe as a public competitive service.

## Before a public launch
- Persist games and events in PostgreSQL; add atomic versioned commands.
- Replace bearer UUID reconnect with expiring signed tokens and account identity.
- Add host controls, player kick/rejoin, lobby timeout, rate limits, spam protection, and server-side room cleanup.
- Implement remaining GDD rules: event effects, contracts, negotiation/escrow, character abilities, threat-10 penalty, scoring details and tie breakers.
- Add automated rules tests and a deployment smoke test.
