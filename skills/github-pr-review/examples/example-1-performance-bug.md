# Example 1: Catching a Performance Bug

## Scenario

A developer submits a PR that adds email notification functionality to the application. The feature works correctly, but the implementation has a significant performance issue.

## Original Code Review

```typescript
// src/services/notification-service.ts
export async function sendBulkEmails(users: User[]): Promise<void> {
  for (const user of users) {
    await sendEmail(user.email, user.name);
  }
  console.log(`All emails sent to ${users.length} users`);
}
```

## AI Agent Review

```
PERFORMANCE ISSUE DETECTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Severity: HIGH
Location: src/services/notification-service.ts (Lines 8-12)
Impact: System will be slow when sending emails to many users

PROBLEM:
The current code sends emails sequentially in a loop.
For 100 users, this will take 100 times longer than necessary.

Example:
- 10 users: ~10 seconds
- 100 users: ~100 seconds (unacceptable)
- 1000 users: ~1000 seconds (system hangs)

RECOMMENDED FIX:
Use Promise.all() for parallel execution:

async function sendBulkEmails(users: User[]): Promise<void> {
  const promises = users.map(user => 
    sendEmail(user.email, user.name)
  );
  await Promise.all(promises);
  console.log(`All emails sent to ${users.length} users`);
}

EXPECTED IMPROVEMENT:
- 10 users: ~1-2 seconds (90% faster)
- 100 users: ~1-2 seconds (98% faster)
- 1000 users: ~1-2 seconds (99% faster)

WHY THIS MATTERS:
In production, you often need to send thousands of emails.
The fix is simple but makes a huge difference in performance.

DIFFICULTY: Easy (1-2 lines of code)
TIME TO IMPLEMENT: 5 minutes
TEST IMPACT: None (same functionality, faster)

NEXT STEPS:
1. Apply the suggested fix above
2. Test with 100+ users
3. Verify all emails are sent
4. Re-request review

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Developer's Response

The developer appreciated the feedback:

> I did not realize the sequential approach would be so slow. The fix was incredibly simple and now emails to 1000 users take less than 2 seconds. This will help a lot as we scale.

## Lesson Learned

This is a common optimization that developers overlook. AI code review helps catch these issues automatically before they impact production performance.

---

*Example Review: AI Agent Skills - GitHub PR Review Skill*