# TSV Format Progress Management Guide

## 📊 Overview

Standard guide for TSV (Tab Separated Values) format progress management.
Provides proven formats validated through real operational experience.

## 🎯 Basic Principles

### 1. **Importance of Chronological Order**
- **Required**: Record entries in chronological order
- **Reason**: To understand progress flow and cause-effect relationships
- **Implementation**: Place DateTime column at the beginning

### 2. **JST DateTime Standardization**
- **Format**: `YYYY-MM-DDTHH:MM:SS+09:00`
- **Example**: `2025-09-11T16:32:28+09:00`
- **Reason**: Consistency for Japanese teams and sortability

### 3. **Status Management**
```
PENDING     : Not started
INPROGRESS  : In progress
DONE        : Completed
ERROR       : Error occurred
BLOCKED     : Blocked (dependencies, etc.)
READY       : Ready (waiting for review, etc.)
```

## 📋 Standard Format

### Header Row
```
DateTime	ServiceName	Environment	Status	DevPR	ProdPR	Notes
```

### Entry Examples
```
2025-09-11T16:32:28+09:00	example-service	production	DONE		https://github.com/org/repo/pull/12345	CI SUCCESS: All checks passed after provider fix
2025-09-11T14:15:30+09:00	example-service	development	DONE	https://github.com/org/repo/pull/12340		PR merged successfully
2025-09-11T12:30:15+09:00	example-service	development	INPROGRESS	https://github.com/org/repo/pull/12340		Slack review request posted
```

## 🗂️ File Management

### Naming Convention
- **Pattern**: `{project_name}_results_{YYYY-MM-DD}.tsv`
- **Example**: `spanner_kit_upgrade_results_2025-09-11.tsv`

### Daily Splitting
- **Recommended**: Create new file when date changes
- **Reason**: File size management and improved searchability
- **Retention**: Keep latest 30 files

## 💡 Best Practices

### 1. **Detailed Notes Recording**
```
Good example:
"CI SUCCESS AFTER PROVIDER FIX: Google Provider upgraded to v6.3 to support 'edition' attribute"

Avoid:
"Success"
```

### 2. **Multi-Environment Tracking**
- Clearly separate development and production environments
- Document dependencies in Notes

### 3. **Detailed Error Information**
```
Error example:
"ERROR: Google Provider version conflict - 'edition' attribute not supported in v5.37. Needs v6.3+ upgrade"
```

### 4. **Clear Blocking Situations**
```
Blocking example:
"BLOCKED: Dev env CI failed with Azure Resource Provider error. Waiting for service owner fix."
```

## 🔄 Update Patterns

### Status Transitions
1. `PENDING` → `INPROGRESS` (Work started)
2. `INPROGRESS` → `DONE` (Normal completion)
3. `INPROGRESS` → `ERROR` (Error occurred)
4. `ERROR` → `INPROGRESS` (Resumed after fix)
5. `INPROGRESS` → `BLOCKED` (Waiting for dependencies)
6. `BLOCKED` → `READY` (Ready for action)

### History Preservation
- **Important**: Don't modify past entries, add new entries instead
- **Reason**: Preserve work history and learning

## 📈 Utilization Benefits

### Quantitative Effects
- **Searchability**: Identify cause-effect relationships through chronological order
- **Traceability**: Direct access to detailed information via PR URLs
- **Analytics**: Efficiency analysis through status statistics

### Qualitative Effects
- **Transparency**: Progress visibility for entire team
- **Learning**: Accumulation of error patterns and solutions
- **Quality**: Improved work quality through detailed recording

## 🛠️ Tool Integration

### Excel/Google Sheets
- TSV format can be directly imported
- Utilize filtering and sorting functions

### Git Management
- Progress files are also version controlled
- Integration with branch work

### CI/CD Integration
- Automatic CI status checking from PR URLs
- Possible automation of status updates

---

**This guide is created based on actual operational experience and is continuously improved.**
