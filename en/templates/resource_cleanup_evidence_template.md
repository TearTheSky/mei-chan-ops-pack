# 🗑️ Resource Cleanup Results for {SERVICE_NAME}-{ENVIRONMENT}

**Date**: {TIMESTAMP}  
**Service**: {SERVICE_NAME}  
**Environment**: {ENVIRONMENT}  
**PR Reference**: {PR_URL}

## ✅ Successfully Deleted Resources:

**📦 Backups:**
{BACKUP_LIST}

**🔄 Standby Instance:**
{STANDBY_LIST}

**🗄️ Metadata Database:**
{METADATA_LIST}

**🪣 GCS Bucket:**
{BUCKET_LIST}

### 📝 Verified Resources (No Action Required):
{VERIFIED_RESOURCES}

### ⏱️ Execution Details:
- **🕐 Duration**: {DURATION}
- **🔐 Permissions**: {PERMISSION_METHOD}
- **🌐 Authentication**: {AUTH_METHOD}
- **✅ Status**: {FINAL_STATUS}
- **🎯 Result**: {RESULT_SUMMARY}

### 📋 Notes:
{ADDITIONAL_NOTES}

**🎉 Resource cleanup completed successfully! {SERVICE_NAME} {ENVIRONMENT} environment is ready for upgrade!**

---

## 📊 Usage Instructions:

### For AI Agents:
1. Replace all `{PLACEHOLDER}` values with actual data
2. Use this template for consistent evidence generation
3. Ensure all technical details are included
4. Format for easy copying and pasting

### For Team Sharing:
```
Copy-paste ready format:
- Service: {SERVICE_NAME}
- Environment: {ENVIRONMENT}
- Status: Cleanup completed successfully
- Duration: {DURATION}
- Next Step: Ready for upgrade
```

### Integration Points:
- **TSV Update**: Status → DONE, Notes → "Resource cleanup completed"
- **PR Comment**: Post this evidence as PR comment
- **Slack Notification**: Share summary with team
- **Documentation**: Archive in project documentation
