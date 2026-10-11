---
name: linkednav
description: Run LinkedIn outreach on the user's own LinkedNav account through the LinkedNav MCP server. Use when the user wants their outreach audited, a campaign created, launched, paused or diagnosed, leads found from buying signals, outreach messages written, replies read or answered, contacts enriched, or results reviewed, and the linkednav tools are available.
---

# LinkedNav: LinkedIn outreach on the user's own account

The tools come from the MCP server `linkednav` at `https://mcp.linkednav.com/`. They run inside the user's own LinkedNav account and respect their active AI setup. LinkedNav is an independent service; it is not made by or affiliated with LinkedIn.

## Before the first call

- If the tools are missing or a call says a key is required, ask the user to sign in to the `linkednav` server from their app's MCP or plugin settings. The sign-in opens LinkedNav's connect page, where they paste their API key (made at https://www.linkednav.com/app/api-keys). Never ask for a key, a password or a LinkedIn cookie in the chat.
- `get_account_status` checks the connection and shows the plan, credits, limits and LinkedIn senders.
- No LinkedIn account connected: run `start_linkedin_connect` and give the user the private link it returns. Prefer it over the cookie and credentials tools.

## Ask before anything is sent or changed

Reading needs no permission: the `get_*`, `analyze_*`, `audit_*`, `diagnose_campaign`, `full_audit` and `preview_*` tools. Read the real state with them before you change anything.

Before any call that sends something on LinkedIn or changes the account, show the user exactly what will happen and to whom, and wait for a yes. That covers:

- **Sending.** `activate_campaign`, `send_unibox_reply`, `approve_pending_reply`, `approve_pending_comment`.
- **Changing.** Every `create_*`, `update_*` and `set_*` tool, `pause_campaign`, `duplicate_campaign`, adding or removing campaign leads, `track_*` and `untrack_*`, and running a signal agent.
- **Spending credits.** The `enrich_*` tools. For `enrich_profiles`, call it with `confirm: false` first, tell the user the estimate, then call it with `confirm: true`.
- **Things that cannot be undone.** Every `delete_*` tool, `bulk_delete_contacts`, `clear_signal_agent_results` and `withdraw_connections` (run `preview_withdraw_connections` first). Say that it cannot be undone when you ask.

A yes covers what was shown, nothing more.

## Common tasks

Take every id and link from the answer of an earlier call. Do not guess one, and do not invent a tool or a parameter.

- **Audit everything.** `full_audit` returns one prioritized `fixPlan` across delivery, setup, performance and pipeline. Walk it from the top.
- **A campaign will not start, or stopped sending.** `diagnose_campaign` gives the blockers, the warnings and the next send.
- **How is it going.** `analyze_performance` compares the funnel with benchmarks and names the bottleneck. Do not state a benchmark the tool did not return.
- **Who to follow up with.** `analyze_pipeline` ranks the real people: opportunities, who is waiting on the user, who is going quiet.
- **Write the messages.** `generate_message_templates` returns a full sequence and the exact `update_prompt` call. It does not save. Review the draft with the user, then save it.
- **Review the setup.** `audit_setup` scores it and lists each gap with its fix.
- **Find leads from buying signals.** `run_intent_agent`, `run_influencer_agent` or `run_competitor_agent`, then `get_agent_run_status` until it is completed, then `get_signal_leads`.
- **Launch a campaign.** `create_campaign`, add people with `add_leads_bulk_to_campaign` or `link_list_to_campaign`, then `activate_campaign`. If it returns `blockers[]`, fix those first.
- **Handle replies.** `get_unibox` and `get_pending_replies` show what is waiting. Edit a draft with `update_pending_reply`, then `approve_pending_reply` or `deny_pending_reply`, or answer directly with `send_unibox_reply`.

## Background jobs

Some tools start work in the background and return a `runId`, `jobId` or `taskId`. The job is not done until its status tool says so: `get_agent_run_status`, `get_discovery_status`, `get_enrichment_status`, `get_phone_enrichment_status`, `get_social_listening_auto_import_task`, `get_unibox_task_status`, or `get_tasks`.

## Relay, do not guess

Report what a tool returned, not what you expected it to return. Never make up account data, contacts or numbers. If a tool says a feature needs a different plan, tell the user that.

## More

The complete playbooks (strategy, copywriting, prospecting, launch, inbox and analysis, with the full tool reference) are in the open-source LinkedIn Outreach OS skill: https://github.com/linglistack/linkedin-outreach-os
