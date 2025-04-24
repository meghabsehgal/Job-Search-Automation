# Automating Job Search Based on Company List in Google Sheets

This guide outlines a process to automate job searching for companies listed in a Google Sheet, using Make.com (formerly Integromat), Google's Custom Search API, and Google Sheets. The end goal is to find relevant job openings and send personalized cold emails with your resume to HR contacts.

---

## 🔧 Prerequisites

- A Google Sheet with a list of company names
- A list of HR contacts (email IDs) — preferably verified
- Google Custom Search Engine (CSE) key and CX (Search Engine ID)
- Make.com account
- Gmail account connected to Make.com
- Resume ready in Google Drive (public or shareable link)

---

## 🗂 Step-by-step Workflow

### 1. **Setup Google Sheet**

- Create a Google Sheet named `Job Search Tracker`
- First column: `Company Name`
- Additional columns (optional): Status, Applied On, Notes

### 2. **Create Custom Search Engine (CSE)**

- Go to [Programmable Search Engine](https://programmablesearchengine.google.com/)
- Create a new CSE
- Restrict search to: `linkedin.com/jobs`
- Note down your `CX` and `API Key`

### 3. **Make Scenario in Make.com**

### Modules Required:

- Google Sheets > Watch Rows
- Iterator
- HTTP > Make a request (Google Search API)
- JSON > Parse JSON
- Iterator (for search results)
- Tools > Text Aggregator (optional)
- Google Sheets > Add Row
- Gmail > Send Email

### 4. **Detailed Scenario Steps**

### a. Google Sheets > Watch Rows

- Select the sheet and worksheet.
- Trigger on new rows or periodically (e.g., every 6 hrs).

### b. Iterator

- Iterate through each row (company name).

### c. HTTP > Make a Request

- URL:
    
    ```
    https://www.googleapis.com/customsearch/v1?q={{1.Company Name}}+jobs+site:linkedin.com/jobs&key=YOUR_API_KEY&cx=YOUR_CX&num=3
    
    ```
    
- Method: GET

### d. Parse JSON

- Extract the array of search results from the HTTP response.

### e. Iterator (Job Results)

- Iterate through each job listing result.

### f. Tools > Text Aggregator

- Create a string like `{{title}} - {{link}}`
- Group results by company
- Row separator: New row
- Output: text

### g. Google Sheets > Add Row (Optional)

- Write job title and URL back to the original sheet in new columns (e.g., `Job Title`, `Job URL`)

### h. Gmail > Send Email

- To: HR email address (from your cold email list)
- Subject: Application for [Role] at [Company Name]
- Body:
    
    ```
    Hi [Name],
    
    I came across a recent opening for [Role] at [Company]. I’ve attached my resume and would be keen to contribute with my experience in [short pitch].
    
    Resume: [Link to Drive or attachment]
    
    Thanks,
    Megha Sehgal
    
    ```
    

---

## 🔁 Loop and Track

- Ensure each email or job URL processed is marked in the sheet to avoid duplicates.
- Add timestamp/logging.

---

## ✅ Outcome

You now have:

- Jobs fetched in real-time from LinkedIn based on your company list
- Emails automatically sent to HRs from your Gmail
- All actions tracked in a single Google Sheet

---

## 💡 Tips

- Rotate company list every week
- Experiment with job role keywords in the query
- Use Google Sheets formulas to filter for fresh rows

---

## 📎 Resources

- [Make.com](https://www.make.com/)
- [Google Programmable Search Engine](https://programmablesearchengine.google.com/)
- [Google Sheets API](https://developers.google.com/sheets/api)

---

This automation empowers proactive outreach in your job search — saving time and expanding reach. Contributions welcome!
