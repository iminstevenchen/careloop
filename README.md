# CareLoop

**Care that follows you home.** An AI voice agent that follows up with patients in the 30 days after hospital discharge, and a care-team app that turns every call into a ranked worklist.

> Showcase repository for our HackTN26 entry (Oracle × Hackathons International, Health Access, Equity & Experience). The source code is in the team's private repository; this page documents the project and my part in it. The demo uses synthetic patients only.

Live demos (hackathon VM, may be offline): [Care-team workspace](https://147-224-146-119.sslip.io/dashboard/provider/) (my build: overview, review queue, patient pages, desktop/phone/widget views) · [Compact care-team view](https://147-224-146-119.sslip.io/dashboard/) · [Slides](https://lnkd.in/edHzPF7b)

## Project description

Most avoidable hospital readmissions happen in the 30 days after discharge, and calling every patient takes enormous nurse time and manpower, so follow-up ends up slow, uneven, and costly. CareLoop is an AI voice agent that calls patients in their own language, checks on symptoms, reinforces care instructions, and surfaces barriers like unaffordable medications. Urgent symptoms trigger an immediate escalation. Every call becomes structured findings that rank patients on a nurse worklist, so the care team's time goes to the patients who need a person. Built on Oracle Cloud Infrastructure with OCI Generative AI and OCI Speech.

## Who it helps

- **Patients:** timely follow-up in their own language, so problems are caught early.
- **Medical providers:** relief from routine calling, so nurses focus on the patients the worklist says need a human.
- **Hospitals and care institutions:** staff time, call timing, and cost used where they matter most, with fewer avoidable readmissions as the goal.

We have not measured readmission outcomes. The hackathon demo runs on synthetic patients.

## My part: the care-team app

I built the app the care team sees after Ava, the voice agent, makes a call.

- **Overview:** counts of follow-ups needing review, open follow-ups, and patients not reached, plus Ava's live call activity.
- **Needs-review queue:** each card shows the concern type (medicines, symptom, transportation, and more), the patient's own quote, language, LACE risk, and next follow-up, with a review action.
- **Quote and transcript view:** the source behind every flag, so nurses can check what the patient said.
- **Call outcomes:** patients reached, calls completed, follow-ups resolved, needing nurse review, and unanswered attempts.
- **Patient pages:** recovery day, 30-day call plan, and care plan with the quotes behind each flag.
- **Agent page:** Ava's recent actions, upcoming calls, reasons for schedule changes, and call outcomes. This is where the learning loop is meant to live (see Next).
- **Layouts:** desktop, phone, and widget previews, plus presenter controls for the live demo.

## Team (Team Sequel)

| Name | Role |
| --- | --- |
| Rohit Venkat | Voice agent |
| I-Min Steven Chen | Care-team app |
| Stephen Senft | Data layer, OCI |
| Jerry Xiao | Product, research, pitch |

## Built with

Oracle Cloud Infrastructure (Compute, Speech, Generative AI), Cohere Command A, Kokoro text-to-speech, FastAPI, and Caddy. The care-team app is a static web front end served by the team's FastAPI backend.

## What ran in the hackathon build

- **Voice agent:** OCI Speech, then Command A on OCI Generative AI, then Kokoro. English and Spanish. Every call discloses it is an AI, offers a person at any time, confirms date of birth before health questions, and stops on emergency phrases with a 911 script.
- **Care-team app and data layer:** the app above, backed by a SQLite store and API on one OCI VM.

**Not yet:** real phone calls through Twilio (built, not exercised), Autonomous Database, FHIR intake and computed LACE scores (patients and scores are seeded from a file), and a rules-based scheduler that sets call timing from risk (the demo runs a fixed plan).

## Next: a learning loop

Use call outcomes (which concerns nurses confirmed, which flags they dismissed, which calls went unanswered) to suggest how to improve Ava's questions and hand-off rules, with a nurse reviewing every change. Not built yet: today the Agent page shows activity and outcomes only.

## Responsible AI

CareLoop organizes information for human review. It does not diagnose, change treatment, or decide anything clinical; nurses and care coordinators make the decisions. It is a hackathon demo with synthetic data and is not intended for use with real patients.
