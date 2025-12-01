# Bug Templates

> **Purpose**: Standardized templates for bug reports, bug audits, and bug fixes documentation.

---

## Bug Report Template

Use this template when reporting a new bug:

```markdown
## Bug: [Brief Description]

**Date**: [Date]
**Severity**: [CRITICAL | HIGH | MEDIUM | LOW]
**Status**: [Open | In Progress | Fixed | Won't Fix]

### Description
[Clear description of what the bug is]

### Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Step 3]

### Expected Behavior
[What should happen]

### Actual Behavior
[What actually happens]

### Environment
- Browser: [Browser and version]
- OS: [Operating system]
- Studio Plan: [Free | Creator | Agency]
- Number of Projects: [Number]

### Screenshots/Videos
[If applicable]

### Console Errors
[Any console errors or warnings]

### Related Files
- `[filepath]:[line]` - [Description]
- `[filepath]:[line]` - [Description]

### Root Cause
[If known, what causes the bug]

### Proposed Fix
[If you have a fix in mind]

### Related Bugs
- [Link to related bugs]
```

---

## Bug Fix Documentation Template

Use this template when documenting a bug fix in page-specific BUG_SOLUTIONS.md (e.g., `studio/BUG_SOLUTIONS.md`):

```markdown
**Attempt #[NUMBER]** - [Bug Title] ✅
- **Date**: [Date]
- **Root Cause**: 
  [Detailed explanation of why the bug exists]
- **Fix**: 
  [Detailed explanation of how the bug was fixed]
- **Lines**: [filepath]:[line-range] ([function/component name])
- **Pattern**: [Pattern learned from this fix]
```

**Example**:
```markdown
**Attempt #12** - Chat message goes to wrong project ✅
- **Date**: [Current]
- **Root Cause**: `handleSendMessage` gets correct project but `updateActiveChatHistory` uses `activeProjectRef.current` without verifying it matches. If user switches projects, message goes to wrong project.
- **Fix**: Verify `activeProjectRef.current?.id === targetProjectId` before using `updateActiveChatHistory`. If ref doesn't match, update project directly via `updateAndSyncProject`.
- **Lines**: `pages/StudioEditor/hooks/useImageProcessing.ts:646-649, 698-739` (`handleSendMessage`)
- **Pattern**: Always verify `activeProjectRef` matches target project before using it. When building chat history, ensure user messages added to ref are included even if project array hasn't updated yet.
```

**Note**: Add this to the relevant page-specific BUG_SOLUTIONS.md file (e.g., `studio/BUG_SOLUTIONS.md` for Studio bugs).

---

## Bug Audit Template

Use this template for systematic bug audits (see [BUG_AUDIT_TEMPLATE.md](../../BUG_AUDIT_TEMPLATE.md)):

```markdown
# Systematic Bug Audit Results - [FOLDER/PATH]

**Audit Date**: [DATE]
**Scope**: [DESCRIPTION OF SCOPE]
**Approach**: [NUMBER]-phase systematic audit
**Auditor**: [NAME/INITIALS]

## File Inventory
[List of files analyzed]

## Phase-by-Phase Findings
[Findings from each phase]

## Bugs Found
[Detailed list of bugs found]

## Summary
[Summary of bugs by category and severity]

## Recommended Fix Priority
[Prioritized list of fixes]
```

---

## Common Issue Template

Use this template when adding to [Common Issues](./common-issues.md):

```markdown
### Issue: [Brief Description]

**Symptoms**:
- [Symptom 1]
- [Symptom 2]
- [Symptom 3]

**Root Cause**: [What causes the issue]

**Solution**: [How to fix it]

**Example Fix**:
\`\`\`typescript
// ❌ WRONG
[Example of wrong code]

// ✅ CORRECT
[Example of correct code]
\`\`\`

**Reference**: [BUG_SOLUTIONS.md](../../BUG_SOLUTIONS.md) - "[Section Name]"
```

---

## Architecture Documentation Update Template

Use this template when updating architecture docs after a bug fix:

```markdown
### [Section Title]

**Pattern**: [Pattern description]

**Why**: [Why this pattern is important]

**Example**:
\`\`\`typescript
[Code example]
\`\`\`

**Reference**: See [BUG_SOLUTIONS.md](../../BUG_SOLUTIONS.md) - "[Section Name]"
```

## Bug Triage Template

Use this template when triaging bugs:

```markdown
## Bug Triage: [Bug ID]

**Reported**: [Date]
**Reporter**: [Name]
**Severity**: [CRITICAL | HIGH | MEDIUM | LOW]

### Impact Assessment
- **Users Affected**: [Estimate]
- **Frequency**: [Always | Often | Sometimes | Rare]
- **Workaround Available**: [Yes | No]

### Priority Assessment
- **Business Impact**: [High | Medium | Low]
- **Technical Debt**: [High | Medium | Low]
- **Fix Complexity**: [High | Medium | Low]

### Assignment
- **Assigned To**: [Name]
- **Target Fix Date**: [Date]
- **Dependencies**: [List]

### Notes
[Additional notes]
```

---

