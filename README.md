# Automated TXT File Processing Pipeline with n8n  
*(Google Drive → Google Sheets → Gmail)*

## 📌 Overview
This project provides an **n8n Cloud workflow** that automates the processing of short text documents.  
The workflow:  
1. Watches a Google Drive folder for new `.txt` files  
2. Downloads the files and extracts key keywords/phrases  
3. Appends the results (filename, text, keywords) to a Google Sheet  
4. Sends a summary email via Gmail with extracted data  

A simple, reusable pipeline for lightweight document automation.

---

## ⚡ Features
- Automated ingestion of `.txt` files from Google Drive  
- Customizable keyword extraction logic (Regex in Code node)  
- Google Sheets integration for structured storage  
- Gmail summary reports for quick insights  
- Runs fully in **n8n Cloud** (no servers required)

---

## 🛠️ Setup Instructions

### 1. Prerequisites
- n8n Cloud account → [app.n8n.cloud](https://app.n8n.cloud)  
- Google account with access to:
  - Google Drive (for `.txt` storage)  
  - Google Sheets (for output storage)  
  - Gmail (for sending email reports)  
- A target Google Sheet with columns: `Filename | Text | Keywords`

---

### 2. Import the Workflow
1. Clone/download this repo  
2. Open n8n Cloud → **Workflows** → **Import from File**  
3. Upload `workflow.json` from this repo

---

### 3. Configure Google Credentials
- In n8n, create new credentials for **Google Drive**, **Google Sheets**, and **Gmail**  
- Use the **“Sign in with Google”** option in each node for easy setup  
- Update the following in the workflow:
  - **Google Drive Trigger:** set your Drive folder ID  
  - **Google Sheets:** set your spreadsheet ID and range (default: `Sheet1!A:C`)  
  - **Gmail Node:** set your recipient email

---

### 4. Run the Workflow
1. Upload `.txt` files into the watched Drive folder  
2. Click **Execute Workflow** in n8n to test  
3. Once confirmed, toggle **Active** to run automatically

---

## 📊 Example Output

### Google Sheet
| Filename   | Text (excerpt)        | Keywords       |
|------------|-----------------------|----------------|
| notes1.txt | "...AI is booming..." | ai             |

### Gmail Summary
