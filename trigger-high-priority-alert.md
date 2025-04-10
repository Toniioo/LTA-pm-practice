## Cloud Function Spec - triggerHighPriorityAlert

## Function Name: 
triggerHighPriorityAlert

### Trigger Type: 
Firestore (on document create)

### Source Collection: 
FeatureRequests

### Trigger Conditions: 
- Priority = High
- Reviewed = false


### Function Logic :
1. Watch FeatureRequests for new documents.
2. When document added: 
IF Priority = High AND Reviewed = FALSE
- THEN send POST request to Slack Webhook. 
-PAYLOAD = Title, SubmittedBy, Department

## Response Behavior:
-Log result into cloud logging:
Success = ' ALert sent successfully ' 
Failure = ' Error Sending Alert to Slack ' 


### Owner: 
Antonio - Product Coordinator


### Constraints: 
- Max 10 Triggers (Slack rate-limit protection)
- Logs retained for 7 days (Audit purposes)

### Monitoring 
- Use GCP -> Operations -> Log Explorer
-Alert DevOps if function fails 3x in 24 hours















