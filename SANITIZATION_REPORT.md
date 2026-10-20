# Sanitization report

Review date: 20 October 2026 (Asia/Manila).

Scope: local Codex review of the supplied n8n JSON export. During that review, no workflow execution, external service requests, actual n8n import, Git commit, GitHub upload, or live-workflow change was performed. Developer-reported runtime testing of the original working workflow is documented separately below.

## Original integrity

- Source: `P03 - Yo-Chi Guest Feedback Automation.json`, outside this publication folder.
- Original size: 22,519 bytes.
- Original SHA-256 before and after: `adb5079818935b50c7b789295775b525f75d2b70bb72b6e3da4db2f090710da0`.
- Output: `P03 - Yo-Chi Guest Feedback Automation.sanitized.json`.

The original was read only and its byte hash remained unchanged.

## Complete semantic change inventory

JSON Pointer paths refer to the original node order. Original secret values, account labels, URLs, and identifiers are deliberately omitted.

| JSON path | Change |
| --- | --- |
| `/id` | Removed source workflow/instance metadata (including credential-setup metadata in meta). |
| `/versionId` | Removed source workflow/instance metadata (including credential-setup metadata in meta). |
| `/meta` | Removed source workflow/instance metadata (including credential-setup metadata in meta). |
| `/nodes/0/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/0/webhookId` | Replaced source form webhook UUID with a fresh UUID. |
| `/nodes/1/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/2/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/2/credentials` | Removed entire Google Sheets OAuth reference, including credential ID and account name. |
| `/nodes/2/parameters/documentId` | Replaced private spreadsheet ID with REPLACE_WITH_YOUR_SPREADSHEET_ID; changed mode list to id; removed cached document title and URL. |
| `/nodes/2/parameters/sheetName` | Replaced source tab ID with generic Feedback_Log in name mode; removed cached tab title and URL. |
| `/nodes/3/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/3/credentials` | Removed entire Google Sheets OAuth reference, including credential ID and account name. |
| `/nodes/3/parameters/documentId` | Replaced private spreadsheet ID with REPLACE_WITH_YOUR_SPREADSHEET_ID; changed mode list to id; removed cached document title and URL. |
| `/nodes/3/parameters/sheetName` | Replaced source tab ID with generic Feedback_Log in name mode; removed cached tab title and URL. |
| `/nodes/4/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/4/parameters/conditions/conditions/0/id` | Replaced source condition UUID with a fresh UUID; comparison logic unchanged. |
| `/nodes/5/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/5/parameters/rules/values/0/conditions/conditions/0/id` | Replaced source condition UUID with a fresh UUID; comparison logic unchanged. |
| `/nodes/5/parameters/rules/values/1/conditions/conditions/0/id` | Replaced source condition UUID with a fresh UUID; comparison logic unchanged. |
| `/nodes/5/parameters/rules/values/2/conditions/conditions/0/id` | Replaced source condition UUID with a fresh UUID; comparison logic unchanged. |
| `/nodes/6/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/6/parameters/url` | Replaced complete Discord webhook URL (ID and secret token) with a nonfunctional example.invalid placeholder. |
| `/nodes/7/id` | Replaced source node UUID with a fresh UUID; name-based connections unchanged. |
| `/nodes/7/parameters/url` | Replaced complete Discord webhook URL (ID and secret token) with a nonfunctional example.invalid placeholder. |

Formatting changed to two-space JSON indentation with a final newline. `README.md` and this report were added. No other workflow fields changed.

## Data review

- Both complete Discord webhook URLs were replaced, removing their webhook IDs and secret tokens. The new distinct HTTPS `example.invalid` placeholders are nonfunctional and contain no replacement secrets.
- Both Google Sheets nodes referenced the same private document and OAuth credential. Complete credential references, including credential IDs and account names, were removed. Spreadsheet IDs, cached document titles, document URLs, and tab URLs were removed. The tab is now specified by the generic setup name `Feedback_Log`, with no original tab ID.
- Workflow ID, version ID, and the entire `meta` object were removed. This removes the instance ID and credential-setup flag. Eight node UUIDs, one form webhook UUID, and four condition UUIDs were regenerated locally and no longer identify the source export.
- `pinData` was already `{}` and remains empty. No execution records, `staticData`, binary payloads, submitted guest records, contact details, or personal names were found. No example submissions were added or retained.
- `example@example.com` remains as the form's fictional email placeholder. `Guest Name` and `Guest Email` are field labels and expression references, not stored guest information. Generic team names and portfolio wording remain.
- Empty tags/node groups, inactive state, execution settings, positions, node types/versions, and the form's independent-demo disclaimer were preserved.

## Preserved functionality

All eight nodes and eight connection edges remain. Comparisons confirmed the JavaScript source, keyword lists and precedence, submission-ID construction, Sheets duplicate lookup, IF logic, Switch rules/routes, all 15 append mappings and schemas, and both Discord message templates are unchanged. Only the documented service locators, credential references, metadata, and UUIDs changed. Condition comparisons excluded regenerated IDs.

Classification is rule-based JavaScript using fixed keyword/rating rules and precedence, not an AI classification model.

## Live Development Workflow Testing

The developer reported successful manual node tests and a complete single-run suggestion test on the **original working n8n workflow** during development. These results concern the configured development workflow; Codex did not execute or independently reproduce those tests. No additional scenario results, performance metrics, or screenshots are claimed.

These live development results are distinct from the offline structural checks of the sanitized export below. They do not establish runtime validation of the sanitized JSON.

## Offline checks

| Check | Result |
| --- | --- |
| Strict JSON parse after writing | PASS |
| n8n export envelope and node parameter structure | PASS, static check |
| Unique names/IDs and retained types/versions | PASS |
| Connection references and main input indexes | PASS: eight nodes, eight edges, no dangling references |
| Original versus sanitized functional fields | PASS: only documented changes |
| Removed source private values across publication files | PASS: absent |
| Live Discord/Sheets URLs and credential-reference objects | PASS: absent |
| Email-address scan | PASS: fictional example addresses only |
| Pinned, execution, and static data | PASS: empty or absent |
| Activation state | PASS: false |
| Original byte hash | PASS: unchanged |
| Actual n8n import and runtime tests of the sanitized export during Codex review | NOT RUN |

This is an n8n-shaped export prepared for import, retaining built-in node types and original type versions. The **sanitized JSON was not imported into n8n or runtime-tested during the Codex review**, so actual importer acceptance, version compatibility, expression resolution, and service behavior remain unverified for this copy. This describes the scope of the review, not n8n availability in the developer's environment. Review an import as a new inactive workflow in a separate instance before any authorized run. Static checks are not an end-to-end test or evidence of business outcomes.

## Remaining risks

1. **Original export:** it intentionally remains unsanitized and contains live-looking secrets/private references. Publish only this folder after review, never the parent folder or original JSON. Earlier sharing and Git history are outside this review. If original webhooks were exposed elsewhere, their owner should rotate/revoke them; validity was not checked and credentials were not changed.
2. **Execution:** inactive/unconfigured does not make the workflow a sandbox. Replacing placeholders and executing nodes can write to Sheets and post to Discord. Keep it inactive until destinations and fictional inputs are reviewed. Placeholder URLs do not replace network isolation.
3. **Privacy:** a deployed form can collect real names, emails, dates, and free text despite its disclaimer. Restrict test access and use fictional input. Review retention and permissions before real use. Future credentials, logs, pins, screenshots, or exports can reintroduce sensitive data.
4. **Spreadsheet input:** formula-like guest input requires review for spreadsheet/CSV formula injection before real use. Original mappings and input logic were intentionally preserved.
5. **Discord:** templates omit names, emails, and raw feedback, but disclose classification and rating metadata. Channel permissions and future template edits require review.
6. **Duplicate handling:** numeric timestamp/index IDs are not content hashes or transactional uniqueness guarantees. Missing/repeated timestamps can collide; new timestamps can bypass detection; concurrent checks can race. Alerts that fail after an append may be skipped on retry.
7. **Classification:** substring rules can miss concerns, match negated phrases, and depend on fixed precedence. This demonstration is not a reliable operational food-safety escalation system.
8. **Routing/batches:** compliments and general feedback have no Switch notification fallback. Suggestions and community engagement share marketing. Append mappings use `.first()` and assume one form submission per execution.
9. **Operational gaps:** the Codex review did not runtime-test the sanitized export's error handling, delivery, rate limits, abuse controls, form authentication, service permissions, or current n8n compatibility. The reported development tests do not establish coverage of all these behaviors. Those behaviors were not changed.
10. **Branding:** public Yo-Chi labels remain for portfolio context. This is independent work, not an official Yo-Chi Singapore project or an endorsement.

## Review boundary

Files are prepared for owner review. No push, publication, live import, credential change, or live-workflow update is authorized by this preparation.
