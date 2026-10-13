# Klisten FailBox for Cursor — candidate v0.1.0

NOT SUBMITTED. Native Cursor installation and conversation are NOT VERIFIED. Historical backend evidence below is not a Cursor client acceptance test.

## Cursor setup and removal

Use your own dedicated key from https://klisten.co.kr/app with: `failbox:session`, `failbox:step`. Configure `KLISTEN_API_KEY` through Cursor plugin configuration; never put the key in a prompt, source file or tool argument. API-key authentication is included; no OAuth account-linking is claimed by this package.

For a local test, copy this package directory under `~/.cursor/plugins/local/klisten-failbox` without overwriting any existing plugin or global MCP configuration. Reload Cursor and inspect the detected tools. If this client/account cannot configure the variable, stop and report it; do not hardcode a credential. Remove only this local package directory to uninstall. Revoke its dedicated key separately. Uninstalling does not delete hosted data.

Official format and variables: https://cursor.com/docs/reference/plugins

Expected tools: `failbox_create_session`, `failbox_step`, `failbox_read`, `failbox_replay`, `failbox_delete_session`. Existing owner policies, records or grants described below are required. Missing prerequisites are not a successful demo. Do not perform paid scans, transfers or new license agreements merely to test this installation.

## Actual service contract and prior backend evidence

# Klisten FailBox — free limited beta

Private, persistent simulations of customer-supplied integer balances. Simulate rate limits, expired credentials and timeout-after-commit; retry with the same idempotency key and replay recorded transitions. This is not a proxy, real financial ledger or infrastructure fault injector.

Requires a dedicated Klisten API key with `failbox:session` and `failbox:step`. The authenticated endpoint is https://api.klisten.co.kr/mcp/failbox. Production backend calls and key revocation were verified on 2026-10-11. Browser sign-in was not part of that backend smoke test.

Limits: 30 requests/minute/organization, 100 active sessions/organization, 500 recorded steps/session, 2–100 accounts, session lifetime 60–86400 seconds. Expired sessions are inaccessible; deletion of expired rows currently occurs when the organization next creates a session. Backup retention remains governed by platform policy.

Tools: failbox_create_session, failbox_step, failbox_read, failbox_replay, failbox_delete_session. Create/step require a caller-selected idempotency_key. Never put real credentials or personal data into simulated account names. No payments or wallet charges are implemented in this release.

Support: klisteninc@gmail.com. Publication and official submission require approval.

## Install after repository publication

## Reviewer example

Call `failbox_create_session` with:
```json
{"balances":{"alice":100,"bob":0},"ttl_seconds":3600,"idempotency_key":"review-create-001"}
```
Use its returned UUID in `failbox_step`:
```json
{"id":"RETURNED_UUID","operation":{"from":"alice","to":"bob","amount":10,"fault":"timeout_after_commit"},"idempotency_key":"review-step-001"}
```
Expect committed=true and client_observed=timeout. Repeat exactly: no second transfer. Call read and replay with {"id":"RETURNED_UUID"}; expect balances 90/10 and verified=true. Call delete using the same id. No real money moves.

FailBox-specific data and retention disclosures are at https://klisten.co.kr/failbox.html, alongside the linked platform privacy policy. Synthetic account names and steps are stored; do not use personal data.


Cursor review status: local candidate only. No Cursor approval or publication is claimed.
