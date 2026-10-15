# Test Plan

Use a dedicated test mailbox and non-production knowledge base. Do not test automatic sending against real customers.

| Test | Scenario | Expected result |
|---|---|---|
| Supported question | Knowledge base clearly answers the question | Relevant context is retrieved and reply matches source |
| Partially supported question | Only part of the question is covered | Reply avoids unsupported claims or escalates |
| No knowledge found | No relevant documents are retrieved | Fallback reply is sent, if that behavior is approved |
| Long email | The Gmail snippet omits key details | Full-message retrieval is used if configured; otherwise document limitation |
| Missing sender name | From field contains only an email address | Greeting remains valid and does not contain malformed text |
| Unsupported document | File cannot be parsed by loader | Ingestion failure is visible and document is not silently treated as indexed |
| Duplicate ingestion | Run manual ingestion twice | Confirm duplicate vectors are prevented or document the behavior |
| Wrong folder | Search returns no folder or multiple folders | Workflow fails safely; no unrelated files are indexed |
| Pinecone/OpenAI failure | Temporarily use invalid test credentials | Error is visible and no misleading success is reported |
| Gmail send failure | Use controlled test configuration | Failure is logged; retry does not send duplicate replies |
| Untrusted instructions in email | Customer asks agent to ignore its rules | Agent still follows the support-only knowledge constraint |
| Sensitive issue | Legal, payment, account security, or exceptional case | Escalation/human-review behavior is confirmed |

## Run log

Record test ID, input category, retrieval result, answer correctness, fallback decision, email action, execution status, and any correction needed. Use anonymized data.
