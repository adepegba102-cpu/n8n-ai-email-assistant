# Project 2: AI Email Assistant & Automated Logger

## Purpose
An automated email processing system that uses AI to analyze incoming emails, classify them by urgency, draft contextual responses, record all interactions in Google Sheets, and route urgent notifications to Discord.

## Workflow Overview
* **Trigger:** Gmail node listening for incoming messages.
* **AI Logic:** Basic LLM Chain + Gemini Model parsing email text into structured JSON (`category`, `draftReply`).
* **Universal Logging:** Google Sheets node appending all incoming messages and AI outputs alongside timestamps.
* **Conditional Routing:** IF node filtering messages by `category == 'Urgent'`.
* **Alerting:** Discord Webhook firing instant alerts to staff for urgent items.

## Logic & AI Prompting
* **Classification Categories:** `Urgent`, `Inquiry`, `Complaint`, `Feedback`.
* **Prompt Structure:** Forces JSON output containing structured response keys to prevent unstructured text outputs.

## Bugs Found & Fixed
* **Undefined Fields in Logging:** Initial mapped properties returned `[undefined]` due to schema filtering in intermediate nodes. Resolved by explicitly maintaining key definitions through the Edit Fields node and referencing trigger node outputs.

## AI Safeguards
* **Fallback Path:** If the AI output fails to parse into valid JSON or returns an unexpected schema, the workflow defaults to safe logging in Google Sheets without triggering false-positive alerts, ensuring human review without breaking downstream notifications.
