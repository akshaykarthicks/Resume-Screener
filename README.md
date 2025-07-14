![ScreenRecording2025-07-14124821-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/c8473e0a-8cc0-4811-838d-fbdc013de19b)# 🤖 AI Resume Screening Workflow (n8n + GPT-4 + Google Drive)

This project automates the process of **analyzing candidate resumes** against job descriptions using AI and stores the evaluation in a **Google Sheet**.
<img width="1377" height="550" alt="image" src="https://github.com/user-attachments/assets/0b3f9359-6653-4a95-bb47-e2176c993869" />

## 🚀 Features

- Automatically receives resumes via Gmail.
- Supports PDF, DOCX, and TXT files.
- Uploads resumes to Google Drive.
- Extracts text from resumes.
- Pulls a predefined Job Description (JD) from Drive.
- Uses GPT-4.1-mini via OpenRouter to:
  - Evaluate the resume against the JD.
  - Score candidate fit (0–10).
  - Extract strengths, weaknesses, risk, and reward factors.
- Extracts candidate name and email.
- Stores all results in Google Sheets with a timestamp and resume link.

---

## 🔧 Tech Stack

- [n8n](https://n8n.io) – Workflow automation
- [Google Drive](https://drive.google.com) – File storage & retrieval
- [Gmail](https://gmail.com) – Resume intake
- [Google Sheets](https://sheets.google.com) – Evaluation dashboard
- [OpenRouter](https://openrouter.ai) – Free GPT API
- [LangChain](https://www.langchain.com) – AI integration

---

## 📂 Workflow Structure

### 1. Receive Resume
- Triggered via Gmail (poll every minute).
- Downloads resume attachment.

### 2. Upload & Identify File Type
- Resume is saved to Google Drive.
- File type (PDF, DOCX, TXT) is detected via Switch node.

### 3. Extract Resume Text
- Depending on file type:
  - PDF → Extract text
  - DOCX → Convert to Google Docs, then extract
  - TXT → Direct extract

### 4. Get Job Description
- Pulls a JD PDF from Drive and extracts its content.

### 5. Run AI Evaluation
- Sends both Resume + JD to GPT-4.1-mini.
- Uses LangChain agent with system instructions.
- Returns:
  - Candidate Strengths
  - Weaknesses
  - Risk & Reward Factors
  - Overall Fit Score (0–10)
  - Justification

### 6. Extract Candidate Info
- Parses resume text for:
  - First Name
  - Last Name
  - Email

### 7. Log to Google Sheet
- Appends:
  - Date
  - Resume Drive link
  - Name & Email
  - AI evaluation results

---



## 🛠 Setup Guide

1. **Import the Workflow** into your n8n instance.
2. Connect credentials:
   - Gmail
   - Google Drive
   - Google Sheets
   - OpenRouter GPT-4.1-mini
3. Update folder IDs and file links for:
   - Resume storage
   - JD file
   - Google Sheet
4. Activate the Gmail trigger and test by sending a resume.

---

## 📁 File Structure

```bash
My Resume Screener/
│
├── My workflow.json       # n8n full workflow
├── README.md              # Documentation

