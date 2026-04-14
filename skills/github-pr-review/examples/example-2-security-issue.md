# Example 2: Detecting a Security Vulnerability

## Scenario

A developer implements a user login feature. The functionality works, but the implementation accidentally exposes sensitive information in error messages and logs.

## Original Code Review

```typescript
// src/auth/login-controller.ts
export async function login(email: string, password: string): Promise<LoginResponse> {
  try {
    const user = await User.findByEmail(email);
    if (!user) {
      console.error(`Login failed: User not found with email: ${email}`);
      throw new Error(`Login failed: User not found with email: ${email}`);
    }

    const isPasswordValid = await bcrypt.compare(password, user.password);
    if (!isPasswordValid) {
      console.error(`Login failed: Wrong password for ${email}: ${password}`);
      throw new Error(`Login failed: Wrong password for user ${email}`);
    }

    return { success: true, token: generateToken(user) };
  } catch (error) {
    console.error(`Login error: ${error.message}`);
    throw error;
  }
}
```

## AI Agent Review

```
CRITICAL SECURITY ISSUE DETECTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Severity: CRITICAL
Location: src/auth/login-controller.ts
Issue: Sensitive Data Exposure in Logs

VULNERABILITY:
The password is logged in plain text on line 13.

Line 13 (DANGEROUS):
console.error(`Login failed: Wrong password for ${email}: ${password}`);
                                                          ^^^^^^^^^^
                                                      PASSWORD EXPOSED

ATTACK SCENARIO:
1. Attacker submits wrong password intentionally
2. Login fails, error is logged
3. Logs are stored in:
   - Error tracking systems (Sentry, etc.)
   - Server logs
   - Aggregation systems (ELK, CloudWatch, etc.)
4. Attacker accesses logs and reads passwords
5. Attacker uses password to access user accounts

SECURITY FIX:

// Line 13 - BEFORE (INSECURE):
console.error(`Login failed: Wrong password for ${email}: ${password}`);

// Line 13 - AFTER (SECURE):
console.error(`Login failed: Invalid credentials for ${email}`);

Also fix line 8:
// BEFORE:
console.error(`Login failed: User not found with email: ${email}`);

// AFTER:
console.error(`Attempted login for non-existent user`);

ALSO CHECK:
- Email addresses should not identify users in logs
- Consider using generic messages for security

RECOMMENDED CHANGES:

export async function login(email: string, password: string): Promise<LoginResponse> {
  try {
    const user = await User.findByEmail(email);
    if (!user) {
      // Generic message - don't reveal whether email exists
      logger.warn('Login attempt for non-existent account');
      throw new Error('Invalid email or password');
    }

    const isPasswordValid = await bcrypt.compare(password, user.password);
    if (!isPasswordValid) {
      // Generic message - don't expose password
      logger.warn('Invalid password attempt', { userId: user.id });
      throw new Error('Invalid email or password');
    }

    logger.info('Successful login', { userId: user.id });
    return { success: true, token: generateToken(user) };
  } catch (error) {
    logger.error('Login error occurred');
    throw error;
  }
}

IMPROVEMENTS:
- No passwords logged
- No email existence information leaked
- Clearer logging for debugging
- Better for security audits
- Follows OWASP guidelines

IMPACT: HIGH
This is a serious security issue that could expose user credentials.

TIME TO FIX: 5 minutes
RISK IF NOT FIXED: User account compromise

NEXT STEPS:
1. Fix the logging immediately
2. Review existing logs for exposed passwords
3. Clean up any logs that contain sensitive data
4. Re-request review after fixing

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Developer's Response

The developer was grateful for the catch:

> I did not realize the password was being logged. That is a serious security issue. Thank you for catching this before it went to production. I have updated the code and will implement proper error logging throughout the app.

## Security Best Practices Added

After this review, the team added to their guidelines:
- Never log passwords or secrets
- Use generic error messages for auth failures
- Regular security reviews of logging
- Use structured logging with security in mind

## Lesson Learned

Security vulnerabilities are often hidden in plain sight in logging and error handling. AI code review helps catch these before they become security incidents.

---

*Example Review: AI Agent Skills - GitHub PR Review Skill*