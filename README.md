Week 1: Email Management Automation

Project Overview

I built an AI-powered email management workflow for Adaeze Consulting, a solo SME growth strategist who provides paid 1:1 strategy sessions.

The goal was to automate the first stage of email handling. Instead of manually checking every incoming message, the workflow uses AI to understand the email, assign a category and priority, recommend an action, organize the message in Gmail, log it in Google Sheets, and alert Adaeze in Slack when an email requires prompt attention.

The Problem

Adaeze Consulting receives different types of emails, including client enquiries, complaints, billing messages, newsletters, promotional emails, and other general communications.

Manually reviewing and sorting these emails can take time, especially when important enquiries or complaints are mixed in with less important messages.

I designed the workflow to handle the initial triage automatically while still keeping the final decision with the business owner.

How I Built It

The workflow starts when a new email enters the Gmail inbox.

The email data is extracted and passed to Gemini for classification. The AI returns the email category, priority, and recommended action.

The workflow then uses those results to:

1. Prepare the email record.
2. Match the AI category to the appropriate Gmail label.
3. Retrieve the available Gmail labels.
4. Apply the correct label to the email.
5. Log the email details in Google Sheets.
6. Check whether the email is high priority.
7. Send a Slack notification when human attention is required.

This gives the workflow a simple path from incoming email to classification, organization, tracking, and notification.

AI Email Classification

I used Google Gemini to classify each email into one of five categories:

Category| Used for
Enquiry| Potential or existing clients asking about services, pricing, availability, consultations, or working with Adaeze
Complaint| Customer dissatisfaction, service problems, refund requests caused by a problem, or formal complaints
Invoice/Billing| Invoices, receipts, payments, charges, and other billing-related messages
Spam/Newsletter| Newsletters, promotional emails, unsolicited marketing, cold pitches, sales messages, and subscription emails
Other| Emails that do not clearly fit the other categories

The AI also assigns a priority:

- High: requires prompt human attention
- Low: does not require immediate attention

The workflow also asks Gemini to recommend an appropriate next action:

- Respond & Schedule
- Respond to Client
- Review & Resolve
- Process Payment/Billing
- Archive/Ignore
- Review Manually

Gmail Organization

After classification, the workflow maps the AI category to a Gmail label.

Enquiry          → Auto/Enquiry
Complaint        → Auto/Complaint
Invoice/Billing  → Auto/Invoice
Spam/Newsletter  → Auto/Spam
Other            → Auto/Other

This means emails can be organized automatically without manually assigning labels to each message.

"Gmail Auto Label" (./gmail-auto-label.png.png)

Google Sheets Email Log

I created a Google Sheets tracker to keep a record of processed emails.

Each entry contains:

- Timestamp
- Sender
- Subject
- Category
- Priority
- Recommended Action
- Status
- View Email

The View Email field contains a direct link to the original Gmail message, making it easier to go from the tracker back to the actual email.

"Google Sheets Email Log" (./google-sheets-email-log.png.png)

"Google Sheets Log Output" (./google-sheets-log-output.png.png)

Slack Notifications

Not every email needs an immediate notification, so I added a priority-based routing step.

When an email is classified as High priority, the workflow sends an alert to Slack containing relevant information such as:

- Priority
- Category
- Sender
- Subject

Low-priority emails are not sent to Slack. They are still labelled in Gmail and recorded in Google Sheets.

"Slack Email Alert" (./slack-email-alert.png.png)

Error Handling

I also connected a separate error-handling workflow to the main automation.

If the main workflow encounters an execution error, the error workflow is triggered and sends a Slack notification.

Main Workflow Error
        ↓
Error Trigger
        ↓
Slack Alert

The alert provides information about the failed execution and node, making it easier to identify where the problem occurred.

"Slack Error Alert" (./slack-error-alert.png.png)

Tools Used

- n8n for workflow automation
- Gmail for email intake and organization
- Google Gemini for AI classification
- Google Sheets for email logging
- Slack for notifications and error alerts

Project Files

The repository contains a sanitized n8n workflow export:

"WEEK 1 — EMAIL MANAGEMENT AUTOMATION - GITHUB SAFE.json"

Credentials and private account configuration were removed before uploading the workflow to GitHub.

Screenshots

Complete Workflow

"Email Management Workflow" (./email-management-workflow.png.png)

AI Classification Node

"AI Classification Node" (./ai-classify-email-node.png.png)

Google Sheets Email Logging

"Google Sheets Email Log" (./google-sheets-email-log.png.png)

Slack Email Alert

"Slack Email Alert" (./slack-email-alert.png.png)

Error Handling

"Slack Error Alert" (./slack-error-alert.png.png)

Google Sheets Output

"Google Sheets Log Output" (./google-sheets-log-output.png.png)

Project Type

AI Automation | Email Management | Workflow Automation | Business Process Automation

Built as part of my practical AI Automation portfolio.
