# Automated Candidate Screening Workflow

## Overview
This n8n workflow automates the candidate screening process for AI Engineer positions. It monitors Gmail for incoming applications, analyzes resumes using keyword matching, and automatically responds to candidates based on their qualifications.

## Components

### Triggers
- **Gmail Trigger**: Monitors emails with subject "AI Engineer" containing attachments
- Polls every minute for new applications

### Processing Nodes
- **Extract from File**: Extracts text content from resume PDF attachments
- **Edit Fields**: Extracts candidate information (name, email, body) from emails
- **Code in JavaScript**: Matches resume against keywords ('mid-level', 'python', 'genai')
- **IF Match**: Routes candidates based on keyword matching criteria
- **Gmail: Mark a message as read**

### Actions
- **Google Sheets**: Adds candidates to appropriate spreadsheets
  - *Candidate Tracker*: Qualified candidates (match ≥ 2 keywords)
  - *Rejected Applications*: Unqualified candidates
- **Gmail**: Sends automated responses
  - Acceptance email to qualified candidates
  - Rejection email to unqualified candidates
- **Gmail: Mark a message as read**

## Workflow Logic
1. Receives email with resume attachment
2. Extracts resume text content
3. Checks for presence of predefined keywords
4. If 2 or more keywords match, candidate is considered qualified
5. Adds candidate to appropriate Google Sheet
6. Sends automated response email based on qualification status

## Configuration Required
- Gmail OAuth2 credentials
- Google Sheets OAuth2 credentials
- Target Google Spreadsheet IDs
- Keywords for resume matching (currently: 'mid-level', 'python', 'genai')

## Dependencies
- Gmail account with API access
- Google Sheets document for tracking candidates