---
name: ghl
description: "Manage your CRM from the vault — create contacts, send emails, trigger workflows, manage pipeline, and book appointments in GoHighLevel."
---

# /ghl — CRM Operations

Connects your vault context to GoHighLevel. Send emails that sound like you, manage your pipeline, trigger workflows, and keep your CRM clean — all from one command.

## Before Running

Read these files silently:
1. `00-Context/voice.md` — How you sound (all outbound comms must match this)
2. `00-Context/audience.md` — Who you serve (for qualifying and segmenting)
3. `00-Context/offer.md` — What you sell (for pipeline and opportunity values)

## What to Ask

"What do you need?"

Then route to the right action:

### Actions

#### 1. Add a Contact
"Tell me about this person — name, email, phone, and how you met them."

Then:
- Create the contact via GHL API
- Tag them based on context (e.g., "inbound", "referral", "event")
- If a nurture workflow exists, ask: "Want to add them to [workflow name]?"
- Log it: `01-Decisions/[YYYY-MM-DD]-new-contact-[name].md`

#### 2. Send an Email
"Who are you emailing and what's the purpose?"

Then:
- Look up the contact in GHL
- Draft the email using `voice.md` tone — no generic templates
- Pull relevant context from vault (if it's a follow-up, check `03-Outputs/` for previous comms)
- Show the draft for approval before sending
- NEVER send without explicit confirmation

#### 3. Nurture Sequence
"Who needs nurturing and what's the situation?"

Then:
- Search for the contact(s) by name, email, or tag
- List available workflows via `ghl_get_workflows`
- Recommend the best fit based on the contact's tags and stage
- Add them to the workflow on confirmation
- If no suitable workflow exists, say: "You don't have a workflow for this yet. I can draft the email sequence copy for you — you'd just need to paste it into a new GHL workflow. Want me to write it?"

#### 4. Pipeline Update
"What happened with [contact/deal]?"

Then:
- Search opportunities by contact
- Update status (open → won/lost/abandoned)
- Update monetary value if it changed
- If won: "Nice. Want me to draft a case study from this?" (links to `/case-study`)
- If lost: "Want to log why? I'll save it to Decisions so you spot patterns."
- Log status change: `01-Decisions/[YYYY-MM-DD]-deal-[name]-[status].md`

#### 5. Book a Meeting
"Who and when?"

Then:
- Look up the contact
- Check available calendar slots
- Create the appointment
- Ask: "Want me to send a confirmation email?"

#### 6. Quick Report
"How's my pipeline looking?"

Then:
- Pull all open opportunities
- Group by pipeline stage
- Show total value, count per stage, oldest deal
- Flag any deal with no activity in 14+ days
- Keep it brief — a snapshot, not a dashboard

## Writing Emails

Every email must:
- Match `voice.md` exactly — their words, their rhythm, their tone
- Be concise — business owners don't read walls of text
- Have a clear single ask or next step
- Never use filler ("I hope this email finds you well", "Just checking in", "Touching base")
- Pull specifics from vault context when relevant (their problem, their industry, previous conversations)

## Logging

All CRM actions get logged to `01-Decisions/` with frontmatter:

```yaml
---
type: decision
category: crm
date: [today]
contact: [name]
action: [contact-created | email-sent | workflow-added | deal-updated | meeting-booked]
---
```

One line summary of what was done and why.

## Safety Rules

- NEVER send an email or SMS without showing the draft and getting explicit "yes" or "send it"
- NEVER delete contacts without confirmation
- NEVER update deal status without confirmation
- If a contact search returns multiple results, ask which one
- If unsure about a workflow, list them and let the user pick

## Tone Rules

- No technical language — "your CRM", "your pipeline", not "GHL API" or "workflow ID"
- Treat this as their assistant handling admin — efficient, no fuss
- If something fails, explain in plain English and suggest a fix
