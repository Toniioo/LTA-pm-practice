## Deployment Plan – Critical Bug Slack Alert Function

---

### 🧠 Feature Summary:
Deploying an automated Cloud Function to monitor Firestore's `bugReports` collection for any new document where:
- severity = high
- reviewed = false


When triggered, it sends a Slack message to the `#bug-triage` channel, improving QA-to-Engineering response times.

---

### 📦 Deployment Owner:
** Antonio - Junior Product Coordinator **

---

### 🚀 Release Date:
**[Planned Release Date – e.g. April 10, 2025]**

---

### 🔁 Rollout Plan:
| Step | Action | Owner |
|------|--------|-------|
| 1 | Final code review + PR merge | Dev |
| 2 | Cloud Build auto-triggers deployment | GCP |
| 3 | PM monitors Cloud Logs for success | Antonio |
| 4 | Submit test bug report (QA) | QA Team |
| 5 | Confirm Slack message fires | Antonio |
| 6 | Set `reviewed = true` to stop alert | QA Team |

---

### ✅ Success Criteria:
- Slack alert posts to the correct channel
- Alert contains correct fields: title, submittedBy, platform
- Function logs show `status: success`
- Trigger does not activate for non-critical or already reviewed bugs

---

### 🧪 Test Plan:
- Add a new Firestore doc with `severity: Critical`
- Watch for Slack alert in `#bug-triage`
- Check Logs Explorer for function execution status
- Modify doc to `reviewed: true` → function should not trigger again

---

### ⚠️ Risk Factors:
- Function fails silently (no log or alert)
- Incorrect Slack config (alert doesn’t post)
- Trigger fires multiple times (spamming Slack)

---

### 🔁 Rollback Plan:
- Disable function temporarily in GCP Console
- Update Firestore to avoid matching conditions
- Alert DevOps to remove faulty deployment

---

### 🗣️ Stakeholder Notifications:
- Slack update to `#product-alerts` post-launch
- Email to QA + Engineering with release summary

---

### 📊 Monitoring:
- GCP Logs Explorer → filter by function name
- Slack channel logs (for success/failure visibility)

---

### ✅ Final Go/No-Go Decision:
- Will be made after test run and log verification
- PM + QA lead must sign off before production deployment
