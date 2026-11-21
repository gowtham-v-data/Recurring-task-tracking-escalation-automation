
# 🔄 Recurring Task Tracking, Pending Reports & Escalation Automation

An end-to-end operational task management and escalation automation system built using **n8n, Google Sheets, Gmail, and JavaScript**.

## 📌 Project Overview

This project automates recurring operational task generation, completion tracking, SLA monitoring, manager notifications, leadership escalation, and operational auditing.

It uses six interconnected n8n workflows to reduce manual tracking, prevent duplicate records, improve task accountability, and provide managers with centralized operational visibility.

## ⚠️ Problem Statement

Managing recurring operational tasks manually can lead to:

- Missed task deadlines and delayed follow-ups.
- Difficulty tracking employee task completion.
- Missing completion proof and accountability.
- Delayed manager notifications and leadership escalations.
- Duplicate task records and inconsistent reporting.
- Lack of centralized operational visibility.

## 💡 Proposed Solution

Developed a six-workflow automation system using n8n and Google Sheets.

The system automatically generates recurring tasks, validates completion records, monitors deadlines, sends email alerts, tracks manager acknowledgements, escalates unresolved issues, and audits operational data.

## ⚙️ Workflow Architecture

### 1️⃣ Recurring Task Generator

**Workflow Name:** AI Operations – 01 – Recurring Task Generator

**Purpose:** Automatically generates recurring operational tasks based on task frequency, first due date, and existing task completion status.

**Trigger:** Daily at 8:00 AM (Asia/Kolkata)

**Process:**
- Reads task configurations from `Task_Master`.
- Checks existing task cycles in `Employee_Workbench`.
- Calculates the next recurring task due date.
- Prevents duplicate task cycle generation.
- Creates new task records in the employee workbench.

**Output:** New recurring task records in `Employee_Workbench`.

![Recurring Task Generator](Screenshot%202026-11-21%20120122.png)

---

### 2️⃣ Completion Processor

**Workflow Name:** AI Operations – 02 – Completion Processor

**Purpose:** Validates employee task completion and records verified completion details.

**Trigger:** Every 2 minutes.

**Process:**
- Reads employee task completion status.
- Validates required completion proof.
- Checks ticket IDs for applicable portal tasks.
- Prevents duplicate completion records.
- Stores validated records in `Completion_Log`.

**Output:** Verified task completion records in `Completion_Log`.

![Recurring Task Generator](./Screenshot%202026-11-21%20120318.png)

---

### 3️⃣ SLA Monitor & Escalation

**Workflow Name:** AI Operations – 03 – SLA Monitor & Escalation

**Purpose:** Monitors task deadlines and automatically notifies managers about overdue tasks.

**Trigger:** Every 15 minutes.

**Process:**
- Reads pending tasks from `Employee_Workbench`.
- Identifies overdue tasks.
- Checks existing alerts to prevent duplicate notifications.
- Retrieves manager email details from `Task_Master`.
- Sends manager notification emails using Gmail.
- Records alerts in `Escalation_Log`.

**Output:** Manager email notifications and escalation records.

![Completion Processor](./Screenshot%202026-11-21%20120339.png)

---

### 4️⃣ Manager Acknowledgement Tracker

**Workflow Name:** AI Operations – 04 – Manager Acknowledgement Tracker

**Purpose:** Tracks manager acknowledgements and escalates unresolved alerts to leadership.

**Trigger:** Every 5 minutes.

**Process:**
- Checks manager acknowledgement status.
- Updates acknowledgement timestamps.
- Verifies whether the task is still pending.
- Identifies alerts that exceed the escalation threshold.
- Sends leadership escalation emails.
- Updates escalation records in `Escalation_Log`.

**Output:** Updated acknowledgement records and leadership escalation notifications.

![SLA Monitor & Escalation](./Screenshot%202026-11-21%20120403.png)

---

### 5️⃣ Manager Dashboard Sync

**Workflow Name:** AI Operations – 05 – Manager Dashboard Sync

**Purpose:** Automatically calculates employee task performance metrics and updates the manager dashboard.

**Trigger:** Every 5 minutes.

**Process:**
- Reads employee task records.
- Calculates total tasks.
- Counts pending, overdue, and completed tasks.
- Identifies the latest completion timestamp.
- Determines whether manager action is required.
- Updates `Manager_Dashboard`.

**Output:** Updated employee performance metrics in `Manager_Dashboard`.

![Manager Acknowledgement Tracker](./Screenshot%202026-11-21%20120425.png)

---

### 6️⃣ Operational Integrity Audit

**Workflow Name:** AI Operations – 06 – Operational Integrity Audit

**Purpose:** Audits operational records to identify duplicate entries and data validation issues.

**Trigger:** Daily at 9:00 AM (Asia/Kolkata).

**Process:**
- Reads employee task records.
- Checks completion records.
- Checks escalation records.
- Identifies duplicate task cycles.
- Identifies duplicate completion records.
- Identifies duplicate escalation alerts.
- Validates required completion proof.
- Generates an operational audit summary.

**Output:** Operational integrity summary and final audit status.

![Manager Dashboard Sync](./Screenshot%202026-11-21%20120443.png)

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and orchestration |
| Google Sheets | Centralized operational data management |
| Gmail | Automated manager and leadership notifications |
| JavaScript | Data processing, validation, and business logic |

## 📊 Google Sheets Structure

The project uses one Google Sheets workbook with six tabs:

| Sheet Name | Purpose |
|---|---|
| `Task_Master` | Stores task configuration, frequency, assignments, and email details |
| `Employee_Workbench` | Tracks recurring task cycles and employee completion status |
| `Manager_Dashboard` | Displays employee task performance metrics |
| `Completion_Log` | Stores validated task completion records |
| `Escalation_Log` | Tracks manager alerts and leadership escalations |
| `Settings` | Stores project configuration and SLA settings |

## 🔁 How It Works

1. The Recurring Task Generator creates task cycles based on configured frequencies.
2. Employees update their task status and submit the required completion proof.
3. The Completion Processor validates and records completed tasks.
4. The SLA Monitor identifies overdue tasks and sends manager notifications.
5. The Manager Acknowledgement Tracker monitors responses and escalates unresolved alerts.
6. The Manager Dashboard Sync updates operational performance metrics.
7. The Operational Integrity Audit checks records for duplicates and missing proof.

## 🧪 Testing & Validation

All six workflows were tested using controlled test data.

| Test Scenario | Result |
|---|---|
| Recurring task generation | ✅ Passed |
| Completion validation | ✅ Passed |
| Duplicate completion prevention | ✅ Passed |
| Manager overdue notifications | ✅ Passed |
| Manager acknowledgement tracking | ✅ Passed |
| Leadership escalation | ✅ Passed |
| Dashboard synchronization | ✅ Passed |
| Operational integrity audit | ✅ Passed |

### 📈 Operational Audit Results

| Audit Metric | Result |
|---|---:|
| Task Cycle Records | 7 |
| Completion Records | 3 |
| Escalation Records | 3 |
| Duplicate Task Cycles | 0 |
| Duplicate Completions | 0 |
| Duplicate Escalation Alerts | 0 |
| Acknowledged Alerts | 1 |
| Leadership Escalated Alerts | 2 |
| Final Audit Status | ✅ COMPLETED |

**Note:** These results are from controlled testing. The workflows were saved and exported but left inactive after testing. They have not been represented as a live production deployment.

## 📁 Repository Structure

```text
recurring-task-tracking-escalation-automation/
│
├── README.md
│
├── 01_Recurring_Task_Generator.json
├── 02_Completion_Processor.json
├── 03_SLA_Monitor_Escalation.json
├── 04_Manager_Acknowledgement_Tracker.json
├── 05_Manager_Dashboard_Sync.json
├── 06_Operational_Integrity_Audit.json
│
├── workflow-01-recurring-task-generator.png
├── workflow-02-completion-processor.png
├── workflow-03-sla-monitor-escalation.png
├── workflow-04-manager-acknowledgement.png
├── workflow-05-manager-dashboard.png
└── workflow-06-integrity-audit.png
```

## 🚀 Setup Instructions

1. Install or access an n8n instance.
2. Import the six workflow JSON files into n8n.
3. Connect your Google Sheets account.
4. Configure Gmail credentials for email notifications.
5. Update the Google Sheets document and required sheet references.
6. Verify workflow settings, schedules, and credentials.
7. Execute controlled tests before activating workflows.

**🔐 Security Note:** Configure your own credentials and spreadsheet references. Never upload OAuth tokens, passwords, or private employee information to GitHub.

## 🔗 Project Resources

**Google Drive – Project Deliverables**

[📂 Access Project Files](https://drive.google.com/drive/folders/1Nneaixp0u-IJbBWH7NIzI8XvrRD-1Qwc?usp=sharing)

## 🔮 Future Enhancements

- Real-time employee notifications.
- Advanced analytics and reporting.
- Role-based access control.
- Automated weekly and monthly reports.
- Integration with additional task management platforms.

## 👨‍💻 Author

**Gowtham V**

- 📧 **Email:** viji29783@gmail.com
- 📱 **Phone:** 6380194774

---

**⭐ Built with n8n, Google Sheets, Gmail, and JavaScript.**
