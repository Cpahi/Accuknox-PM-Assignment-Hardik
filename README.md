# Product Management Assignment: Cloud Security Alert Triage
**Submitted by:** Hardik Tiwari
**Role:** Product Management Trainee Applicant

## 👉👉 [Click Here to View Live Figma Prototype](https://log-plot-89847175.figma.site) 👈👈

---

## 1. Problem Statement & User Persona

### The Problem: Alert Fatigue & Context Switching
Security teams today suffer from massive "Alert Fatigue." Engineers receive hundreds of alerts daily, many of which are low-fidelity. They waste critical minutes switching context between the security dashboard and the AWS/Azure console just to verify if an alert is real ("Is this server actually in production?"). This delay increases the "Mean Time to Remediate" (MTTR) for genuine threats.

### User Persona: "DevOps Dave"
* **Role:** Security Operations Engineer
* **Goal:** Protect infrastructure by identifying and extinguishing "fires" quickly.
* **Frustrations:** Fear of breaking production systems with accidental clicks; being overwhelmed by noise (false positives).
* **Needs:** Immediate context (metadata), safety guardrails for destructive actions, and proof (logs) before taking action.

---

## 2. Proposed Solution: The "Verify & Fix" Workflow

I designed a 4-step linear workflow that prioritizes **Safety** and **Evidence** over raw speed.

### Phase 1: Context-First Dashboard (Overview Tab)
Instead of a generic list, the Detail Panel immediately surfaces key Metadata (Environment: Production, Owner: DevOps). I utilized visual hierarchy—changing the **"Remediate" button to Red**—to signal urgency for High-Severity alerts, helping Dave prioritize his attention instantly.

### Phase 2: Evidence-Based Verification (Raw Evidence Tab)
Engineers rarely trust a summary blindly. I added a **"Raw Evidence" tab** that displays the actual JSON logs (e.g., `user: root`, `action: ConsoleLogin`). This allows users to validate the threat without logging into AWS CloudTrail, significantly reducing investigation time.

### Phase 3: The "Safety" Modal (Key Guardrail)
Automated remediation is risky. I introduced a **Confirmation Modal** that acts as a "speed bump," preventing accidental clicks. It clearly states the consequence ("Detaching root keys") before execution, preventing Type-1 errors (breaking valid systems).

### Phase 4: Positive Closure
A clear **Success Toast** confirms the script ran successfully, and the alert status updates to "Resolved" automatically. This closes the feedback loop and gives the user confidence that the threat is neutralized.

---

## 3. Wireframes

*(Note: Click the "Live Prototype" link at the top for the interactive experience.)*

### Step 1: Context-First Dashboard
**The Trigger:** The "Overview" tab surfaces critical tags (Production, DevOps) and uses a **Red Button** to signal high severity/urgency immediately.
<img width="1919" height="921" alt="image" src="https://github.com/user-attachments/assets/b480c377-0fc5-4b49-8a27-5c53c3153557" />

![Main Dashboard](dashboard.png)

### Step 2: Evidence-Based Verification
**The Investigation:** The "Raw Evidence" tab allows engineers to verify the actual JSON logs without leaving the platform to check CloudTrail.
<img width="1918" height="919" alt="image" src="https://github.com/user-attachments/assets/dc8f8696-8242-4b11-8b02-2f98118c7731" />

![Evidence Tab](evidence.png)

### Step 3: The Safety Guardrail
**The Guardrail:** A destructive action (Remediation) triggers a mandatory safety check to prevent accidental outages.
<img width="1919" height="921" alt="image" src="https://github.com/user-attachments/assets/2ab22259-c58e-49a5-a762-2c578821a370" />

![Confirmation Modal](modal.png)

### Step 4: The Success State
**The Resolution:** Instant feedback confirms the script executed successfully and updates the alert status.
<img width="1919" height="920" alt="image" src="https://github.com/user-attachments/assets/b1179d78-3828-4bc1-89c4-80e670238ffa" />

![Success State](success.png)

---

## 4. Prioritization & Success Metrics

### Prioritization Logic (RICE Framework)
1.  **Contextual Enrichment (Priority: High):** Showing tags/JSON logs has the highest **Impact** because it solves the "verification" bottleneck with low development **Effort**.
2.  **Safe Remediation (Priority: High):** Automated fixing is the core value, but I prioritized the **Safety Modal** over speed to ensure trust. If we break production once, users will never use the auto-fix again.
3.  **Visual Urgency (Priority: Medium):** Dynamic button colors (Red vs. Blue) improve the UX but are less critical than data accuracy.

### Success Metrics
* **Primary Metric:** **MTTR (Mean Time to Remediate)** – Target reduction from 15 mins (manual console work) to <2 mins (assisted workflow).
* **Secondary Metric:** **Safety Score** – % of remediations executed without rollback/error (Goal: 100%).
* **Adoption Metric:** % of users toggling the "Raw Evidence" tab (validates if the feature is useful).

---

## 5. (Bonus) Development Action Items

To ensure this design is feasible, I identified these key technical considerations for the engineering team:

1.  **Audit Logging (Compliance):**
    * *Requirement:* The backend must log the specific User ID, Timestamp, and "Action Type" when the "Confirm" button is clicked. This is mandatory for SOC2/ISO compliance.
2.  **API Latency & States:**
    * *Requirement:* If the AWS API takes >3 seconds to execute the fix, the "Remediate" button must enter a `Loading/Spinner` state to prevent double-clicks.
    * *Edge Case:* If the API fails, show a "Retry" error message instead of the Success Toast.
3.  **RBAC (Role-Based Access Control):**
    * *Requirement:* Ensure the "Remediate" button is **Disabled/Grayed out** for users with "Read-Only" permissions.

---

## About the Creator
**Hardik Tiwari** | Final Year B.Tech (CSE & Cybersecurity)
* **Experience:** Product Analyst Intern @ Dhwani Rural Information Systems.
* **Focus:** Bridging the gap between complex security infrastructure and intuitive user experience.
* **Contact:** https://www.linkedin.com/in/hardiktiwaricpahi/ | iamhardiktiwari@gmail.com | www.caphi.in
