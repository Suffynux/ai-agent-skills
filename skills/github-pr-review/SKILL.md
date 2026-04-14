# GitHub PR Review Skill

**Automated, intelligent code review for every pull request**

## What This Skill Does

The GitHub PR Review skill enables AI agents to analyze pull requests, identify issues, suggest improvements, and provide architectural feedback. This skill automates the code review process while maintaining quality standards and catching bugs before they reach production.

### Key Capabilities

- **Deep Code Analysis** - Examine code logic, performance, and security
- **Bug Detection** - Catch potential bugs and edge cases
- **Best Practices Review** - Ensure code follows industry standards
- **Architecture Assessment** - Evaluate system design and scalability
- **Security Review** - Identify security vulnerabilities and risks
- **Performance Analysis** - Spot performance bottlenecks
- **Testing Coverage** - Recommend test coverage improvements
- **Documentation Check** - Verify code is well-documented

---

## Agent Capabilities: What Can AI Agents Do?

### What Agents CAN Do During PR Review

1. **Analyze Code** - Read and understand code logic and patterns
2. **Identify Issues** - Find bugs, inefficiencies, and potential problems
3. **Suggest Improvements** - Propose better approaches and solutions
4. **Request Changes** - Comment with detailed feedback and requirements
5. **Ask Questions** - Clarify unclear code or logic
6. **Recommend Best Practices** - Suggest industry standards and patterns
7. **Check Compliance** - Verify code meets project standards
8. **Provide Examples** - Show correct implementations or alternatives
9. **Schedule Reviews** - Trigger reviews automatically
10. **Generate Reports** - Create summary reports of findings

### What Agents CANNOT Do (By Default)

1. **Modify Code** - Cannot directly commit changes without approval
2. **Merge PRs** - Cannot merge pull requests (requires human approval)
3. **Access External Systems** - Cannot reach systems outside your configuration
4. **Make Breaking Changes** - Cannot change functionality without review
5. **Override Security** - Cannot bypass security policies or reviews

### Advanced: Semi-Automated Mode (Optional)

Some teams configure agents in **Semi-Automated Mode** where:
- Agents can suggest code changes in comments
- Developers review and approve before changes are committed
- Provides speed-up without losing control
- Requires proper safeguards and approval workflows

> **Note:** Default configuration is Review and Suggest (agent provides feedback only)

---

## Getting Started

### Installation

1. **Copy the skill to your project:**
```bash
cp -r skills/github-pr-review /path/to/your/project/.agent-skills/
```

2. **Add to your VS Code configuration:**

Create or edit `.instructions.md` in your project root:

```markdown
# AI Agent Instructions

You have access to the following skills:

## GitHub PR Review Skill
Location: .agent-skills/github-pr-review/SKILL.md

When a developer opens a pull request:
1. Analyze the code changes
2. Check for bugs and issues
3. Verify best practices compliance
4. Provide constructive feedback
5. Suggest improvements where applicable

Remember: You provide feedback and suggestions only. You do NOT commit code changes.
```

3. **Configure your AI agent** to use this skill in your workflow.

---

## How to Use This Skill

### For Developers

**Step 1:** Open a pull request in GitHub  
**Step 2:** The AI agent automatically reviews the code  
**Step 3:** Read the agent's feedback and suggestions  
**Step 4:** Make improvements based on feedback  
**Step 5:** Re-request review after changes  

### For Teams

**Setup Instructions:**

```yaml
# In your AI Agent Configuration
skills:
  - name: github-pr-review
    location: .agent-skills/github-pr-review
    trigger: on_pull_request_opened
    config:
      review_type: comprehensive
      auto_comment: true
      suggest_improvements: true
      check_security: true
      check_performance: true
```

### For CI/CD Integration

```bash
# Add to your CI/CD pipeline
ai-agent review-pr \
  --skill github-pr-review \
  --pr-number $PR_NUMBER \
  --repo $REPO_NAME
```

---

## Best For (Model Compatibility)

This skill works seamlessly with:

| Model | Support | Notes |
|-------|---------|-------|
| **Claude (Anthropic)** | Excellent | Best for nuanced analysis |
| **OpenAI GPT-4** | Excellent | Best for complex architecture review |
| **OpenAI GPT-3.5** | Good | Fast and cost-effective |
| **GitHub Copilot** | Good | Integrated GitHub workflow |
| **Cohere** | Good | Great for large codebases |
| **LLaMA (Open Source)** | Good | For self-hosted setups |
| **Mistral** | Good | High-quality analysis |
| **Any LLM API** | Compatible | Works with any model |

> **Recommendation:** For best results, use Claude or GPT-4—they provide the most accurate architectural analysis and catch the most edge cases.

---

## Real-World Examples

### Example 1: Catching a Performance Bug

**PR:** Added email notification feature

**Agent Review:**
```
Issue Found: Performance Problem
File: src/notifications/email-service.ts (Lines 45-52)

Current Code:
for (const user of users) {
  await sendEmail(user); // Sequential - slow!
}

Suggestion:
Use Promise.all() for parallel execution:
const emailPromises = users.map(user => sendEmail(user));
await Promise.all(emailPromises);

Impact: 10x faster for large user lists
Difficulty: Easy fix
```

### Example 2: Security Vulnerability Detection

**PR:** Added user authentication

**Agent Review:**
```
SECURITY ISSUE: Sensitive Data Exposure
File: src/auth/login.ts (Line 28)

Problem:
Password is logged to console in error message:
console.error(`Login failed: ${password}`);

Fix:
console.error(`Login failed for user: ${email}`);

Risk Level: HIGH - Credentials exposed in logs
```

### Example 3: Architecture Recommendation

**PR:** Added database caching layer

**Agent Review:**
```
Architecture Improvement Suggested:
Current approach has potential race condition.

Consider adding:
1. Distributed locking (Redis)
2. Cache invalidation strategy
3. Fallback handling

This ensures consistency in high-traffic scenarios.
Estimated implementation time: 4 hours
```

---

## Configuration and Customization

### Review Scope

Control what the agent reviews:

```yaml
review_config:
  check_code_quality: true
  check_security: true
  check_performance: true
  check_testing: true
  check_documentation: true
  check_best_practices: true
  max_comments: 10  # Limit feedback volume
```

### Custom Rules

Define project-specific review rules:

```yaml
custom_rules:
  - name: "TypeScript Strict Mode"
    description: "Ensure TypeScript strict mode is enabled"
    severity: high
  
  - name: "Test Coverage"
    description: "New code must have 80%+ test coverage"
    severity: medium
  
  - name: "Documentation"
    description: "Public functions must be documented"
    severity: medium
```

### Model Selection

```yaml
ai_model: "claude-3-opus"  # Best for PR review
# or
ai_model: "gpt-4"          # Alternative
# or
ai_model: "gpt-3.5-turbo"  # Budget option
```

---

## Review Report Template

Each review generates a report:

```
═══════════════════════════════════════════════════════════
PR REVIEW REPORT - PR #123
═══════════════════════════════════════════════════════════

SUMMARY
- Lines Changed: 245
- Files Modified: 6
- Review Status: APPROVED WITH SUGGESTIONS

CODE QUALITY
- Issues Found: 3
- Performance Issues: 1
- Security Issues: 0

APPROVED ASPECTS
- Good error handling
- Clear variable naming
- Proper function decomposition

SUGGESTIONS FOR IMPROVEMENT
1. Consider using async/await instead of callbacks
2. Add more test coverage for edge cases
3. Document the authentication flow

NEXT STEPS
- Address the 3 suggestions above
- Re-request review when ready

═══════════════════════════════════════════════════════════
```

---

## Best Practices for PR Review

### For Maximum Effectiveness

1. **Include Clear Commit Messages** - Helps the agent understand intent
2. **Add PR Description** - Context about what and why changes were made
3. **Link to Issues** - References to issues improve understanding
4. **Include Tests** - Test code helps validate implementation
5. **Follow Project Conventions** - Agent can better assess consistency
6. **Reasonable PR Size** - Smaller PRs get better reviews

### For Developers Receiving Reviews

1. **Read Carefully** - Review all agent suggestions thoughtfully
2. **Ask Questions** - If a suggestion is not clear, ask for clarification
3. **Do Not Ignore Security Warnings** - Always address security issues
4. **Consider Performance Notes** - Performance matters for scale
5. **Improve Iteratively** - Use feedback to improve your coding skills

---

## Advanced Features

### Batch PR Review

Review multiple PRs at once:

```bash
ai-agent review-batch \
  --skill github-pr-review \
  --repo my-project \
  --filter "state=open"
```

### Scheduled Reviews

Automatically review PRs on a schedule:

```yaml
schedule:
  - cron: "0 9 * * 1"  # Monday 9 AM
    action: review_open_prs
    skill: github-pr-review
```

### Integration with Slack

Get PR review notifications in Slack:

```yaml
notifications:
  - channel: #code-reviews
    trigger: review_complete
    include: high_priority_issues
```

---

## Troubleshooting

### Issue: Agent is too verbose

**Solution:** Adjust configuration:
```yaml
review_config:
  verbosity: low
  max_comments: 5
```

### Issue: Agent is not catching issues

**Solution:** Use a more capable model:
```yaml
ai_model: "claude-3-opus"  # Better than GPT-3.5
```

### Issue: Reviews take too long

**Solution:** Limit scope:
```yaml
review_config:
  check_security: true
  check_performance: false  # Skip if not needed
```

---

## Integration Examples

### GitHub Actions Workflow

```yaml
name: AI Code Review
on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run AI Review
        env:
          AI_API_KEY: ${{ secrets.AI_API_KEY }}
        run: |
          ai-agent review-pr \
            --skill github-pr-review \
            --pr-number ${{ github.event.number }}
```

### GitLab CI Integration

```yaml
ai_review:
  stage: review
  script:
    - ai-agent review-pr 
      --skill github-pr-review 
      --mr-number $CI_MERGE_REQUEST_IID
  only:
    - merge_requests
```

---

## Contributing

Found a bug or have an improvement? Help us improve this skill:

1. Open an issue describing the problem
2. Submit a pull request with your improvement
3. Include examples of the issue or improvement
4. Follow the project's contribution guidelines

---

## License

This skill is part of the AI Agent Skills project and is licensed under the MIT License.

---

## Need Help?

- **Read the Full Guide** - Check our documentation
- **Ask in Discussions** - Community members can help
- **Report Issues** - Found a bug? Create a GitHub issue
- **Request Features** - Suggest improvements

---

## Next Steps

1. **Install the skill** - Copy to your project
2. **Configure it** - Set up your preferences
3. **Try your first review** - Open a PR and see it in action
4. **Customize it** - Adjust settings for your team's needs
5. **Share it** - Tell your team about this tool

---

Happy reviewing! Let AI agents handle the code review while you focus on what matters.

---

*Last Updated: April 14, 2026*  
*Version: 1.0*  
*Maintained by: AI Agent Skills Community*