# Bug Solutions & Lessons Learned

> **Purpose**: This document serves as an overview and index to page-specific bug solutions. Use this to navigate to granular solutions for specific pages/features, and reference general patterns that apply across all pages.

---

## Bug Fixing Workflow

When handling bugs:
0. **CRITICAL: Clean up console logs** - Remove all white noise console logs. Only keep logs specific to the bug being investigated. This ensures clean, focused debugging output.
1. Read page-specific BUG_SOLUTIONS.md (e.g., docs/troubleshoot/studio/BUG_SOLUTIONS.md for Studio)
2. Search for similar bugs - check all relevant entries for the feature (projects, chat, analysis, etc.)
3. Propose fix using documented patterns from BUG_SOLUTIONS.md
4. Wait for user to test and report results
5. If fix fails, try different strategy - check BUG_SOLUTIONS.md again for alternatives
6. Document successful fixes in page-specific BUG_SOLUTIONS.md

Key: Always use established patterns from BUG_SOLUTIONS.md, don't invent new approaches.

### Console Log Cleanup Policy

**Before starting any bug investigation:**
- **Remove/comment out** all console logs that are not directly related to the bug
- **Keep only** logs that help diagnose the specific bug being investigated
- **Add new logs** only if they provide specific insight into the bug's root cause
- **Remove logs** after the bug is fixed (unless they're needed for ongoing monitoring)

**Rationale**: White noise logs make it harder to spot the actual issue. Clean, focused logs make debugging faster and more effective.

---

## Document Maintenance Policy

**Condensing Policy**: Bug logs older than 2 days are condensed to focus on solutions:
- ✅ **Keep**: Bug name, **Fix/Solution** (what was done), Files/Lines, Pattern
- ❌ **Remove**: Detailed root cause explanations, step-by-step problem descriptions
- **Rationale**: Solution details are critical for troubleshooting similar bugs. Root cause analysis is less needed once the pattern is established.

**Condensation Marker**: Entries that have been condensed are marked with `[CONDENSED]` tag in the title. **Do not re-condense entries that already have this marker.**

**Current Date Reference**: Use current date to determine which entries to condense (entries older than 2 days from current date)

**When Condensing**:
1. Check if entry already has `[CONDENSED]` tag → Skip if present
2. Check if entry date is older than 2 days → Condense if yes
3. Remove "Root Cause" section entirely
4. Keep all "Fix" details (what was done, all steps)
5. Keep Files/Lines and Pattern sections
6. Add `[CONDENSED]` tag to title: `**Attempt #[N]** - [Title] ✅ [CONDENSED]`

---

## Navigation: Page-Specific Solutions

For bugs related to specific pages, see the page-specific solutions:

- **[Studio Editor](./studio/BUG_SOLUTIONS.md)** - Studio Editor specific bugs and solutions
- **[Settings](./settings/BUG_SOLUTIONS.md)** - Settings page bugs (to be filled when encountered)
- **[Landing](./landing/BUG_SOLUTIONS.md)** - Landing page bugs (to be filled when encountered)

---

## Quick Reference: General Bugs & Fixes

| Bug | Root Cause | Fix | File(s) |
|-----|------------|-----|---------|
| Infinite loops | State in `useEffect` deps causing re-renders | Remove state from deps, use refs for comparison | Various hooks |

> **Note**: Most bugs are page-specific. See page-specific solutions above for detailed bug fixes.

---

## Critical Patterns & Anti-Patterns

These patterns apply across all pages and should be followed universally:

### ✅ What Works (Always Do This)

1. **Use refs for latest data, React state for UI** - Refs update synchronously, state updates asynchronously
2. **Check for changes before updating in useEffect** - Prevents unnecessary updates and infinite loops
3. **Always clean up resources in useEffect** - AbortControllers, timeouts, event listeners should be cleaned up
4. **Include all dependencies in dependency arrays** - Prevents stale closures
5. **Capture values at start of effects** - Prevents race conditions

### ❌ What Doesn't Work (Never Do This)

1. **Using refs inside React updaters** - Breaks React's reactivity and batching
2. **Relying on React state for latest data in async operations** - Use refs instead
3. **Missing dependencies in dependency arrays** - Causes stale closures
4. **Not cleaning up resources** - Causes memory leaks and unexpected behavior
5. **Complex conditional logic when simple inverse works** - Keep it simple

### 🔑 Critical Patterns

- **Race Conditions**: Always read from refs for latest data in async operations, not React state
- **Async Operations**: Store IDs/values at start of operation, use them throughout (don't rely on refs that might change)
- **State Sync**: Use `useEffect` to sync UI state with data, but check for changes before updating
- **Cleanup**: Always clean up resources (AbortControllers, timeouts, event listeners) in component unmount cleanup
- **Dependency Arrays**: Always include all values used in callbacks/effects in dependency arrays

---

## Page-Specific Patterns

### Studio Editor Patterns

See [Studio Editor BUG_SOLUTIONS.md](./studio/BUG_SOLUTIONS.md) for Studio-specific patterns including:
- Ref verification pattern
- Latest collection ref pattern
- History index defaults
- Chat images source of truth
- Flush after bulk operations
- Cross-project isolation

---

## How to Use This Document

1. **For page-specific bugs**: Navigate to the relevant page-specific solution (e.g., [Studio Editor](./studio/BUG_SOLUTIONS.md))
2. **For general patterns**: Reference the "Critical Patterns & Anti-Patterns" section above
3. **When fixing a bug**: 
   - If it's page-specific, add it to the page-specific BUG_SOLUTIONS.md
   - If it's a general pattern, add it here
4. **When reviewing code**: Check both this document and the relevant page-specific document

---

## Related Documentation

- **[Common Issues](./common-issues.md)** - Frequently encountered bugs and solutions
- **[Debugging Guide](./debugging-guide.md)** - Step-by-step debugging process
- **[Troubleshooting Checklist](./troubleshooting-checklist.md)** - Systematic debugging checklist
- **[Bug Templates](./bug-templates.md)** - Templates for bug reports and audits
- **[Architecture Documentation](../architecture/README.md)** - Architecture documentation
