# Frequently Asked Questions (FAQ)

## General Questions

### What is AI Agent Skills?

AI Agent Skills is an open-source library of ready-to-use skills for AI agents. Think of skills as specialized capabilities that enable AI agents to perform complex tasks like code review, architecture design, frontend optimization, and more. Simply copy a skill into your project and your AI agent can use it immediately.

### How much does it cost?

AI Agent Skills is completely free and open source under the MIT License. You can use it anywhere, modify it, and distribute it without any cost.

### Do I need to pay for AI models?

No, but you can use it with paid or free models:
- **Free Models** - Use with free APIs (Claude free tier, OpenAI free credits)
- **Paid Models** - Use with paid APIs (OpenAI, Anthropic, Cohere)
- **Open Source** - Use self-hosted models like LLaMA for free

### Is this for beginners or experts?

Both. The skills are designed to be:
- **Easy to start** - Beginners can get started quickly
- **Deep enough** - Experts can customize everything
- **Well documented** - Clear explanations for everyone

---

## Technical Questions

### Which AI models work with these skills?

All of them. Skills are model-agnostic and work with:
- Claude (Anthropic)
- OpenAI (GPT-4, GPT-3.5, etc.)
- GitHub Copilot
- Cohere
- LLaMA and open-source models
- Any LLM with an API

### What programming languages are supported?

Skills work with all programming languages:
- JavaScript/TypeScript
- Python
- Java
- C#
- Go
- Rust
- PHP
- And everything else

### Can I modify the skills?

Absolutely. Each skill is fully customizable. You can:
- Adjust parameters and settings
- Add custom rules and checks
- Modify the skill's behavior
- Combine multiple skills
- Create new variations

### How do I integrate skills into my project?

It is simple:

1. Clone or download the repository
2. Copy the skill folder to your project
3. Add it to your AI agent configuration
4. Use it immediately

Most skills are plug-and-play with minimal setup.

### Do I need to host anything?

No. Skills are just files that your AI agent reads. No server or backend required for most skills. Just add them to your project.

---

## AI Agent and Code Changes

### Can AI agents actually code while reviewing?

By default, no. The agent provides feedback and suggestions, but cannot modify code without explicit approval. This gives you complete control.

### Can I enable auto-fix mode?

Many teams do. In advanced configurations:
- Agent suggests fixes in comments
- Developer reviews and approves
- Changes are committed automatically
- This requires proper safeguards

Check each skill's documentation for configuration options.

### Will the agent break my code?

No. By default, agents only analyze and suggest. They do not modify production code. You maintain full control over what changes are made.

### What if I do not like the agent's suggestions?

That is fine. You review all suggestions from the agent and decide:
- Accept and implement
- Reject and skip
- Modify and improve
- Ask for clarification

The agent is an assistant, not a decision-maker.

---

## Setup and Configuration

### How long does setup take?

Most skills take 5-10 minutes to set up:
1. Copy the skill folder (1 minute)
2. Add to your configuration (2 minutes)
3. Configure preferences (2-5 minutes)
4. Test with your first task (2 minutes)

### Do I need administrator access?

Usually no. Most skills work on individual projects. Some organization-wide features might need admin access for GitHub/GitLab integration.

### Can I use multiple skills together?

Yes. Skills are designed to work together. You can enable:
- GitHub PR Review plus AI Code Review
- Architecture Design plus Code Review
- Frontend Design plus Performance Review

Just add multiple skills to your configuration.

### What if something breaks?

Check our Troubleshooting section in each skill or:
1. Review the skill's documentation
2. Check GitHub Issues for similar problems
3. Create a new issue with details
4. Ask in GitHub Discussions

---

## Performance and Costs

### Will this slow down my workflow?

No, it speeds it up. Skills run in the background:
- No impact on your development speed
- Reviews happen automatically
- You get results when you need them

### How much will this cost with APIs?

Costs depend on your model:
- **OpenAI:** ~$0.01-0.30 per PR review (depends on PR size and model)
- **Claude:** ~$0.01-0.20 per PR review
- **Free Models:** $0 (but might be slower)

For a typical team doing 20 PR reviews per day with Claude, you would spend ~$6-10 per month.

### Can I use local/offline models?

Yes. You can:
- Use LLaMA or Mistral locally
- Configure skills to use your local API
- Run completely offline (if you have enough resources)

---

## Security and Privacy

### Is my code private?

Yes. By default:
- Code stays in your repository
- Nothing is uploaded unless you configure it
- Skills process code locally
- Your data is yours only

### What if I send code to an external API?

Always review the API provider's privacy policy:
- **OpenAI:** See their data usage policy
- **Claude:** See Anthropic's privacy policy
- **Self-hosted:** Nothing leaves your system

### Can I trust these skills?

The project is open source—you can see exactly what each skill does. Review the code, verify it matches the documentation, and report issues.

---

## Customization and Advanced

### Can I create my own custom skill?

Absolutely. The project structure makes it easy. Check the CONTRIBUTING.md guide:
1. Create a new skill folder
2. Write your SKILL.md documentation
3. Add examples
4. Test it out
5. Share with the community

### Can I use skills in production?

Yes, millions of AI-powered systems use similar skills. Just:
- Test thoroughly first
- Have approval workflows
- Monitor results
- Be ready to disable if issues arise

### How do I handle errors from the agent?

Each skill includes error handling guidance. General best practices:
- Log all reviews and feedback
- Monitor for unusual patterns
- Have manual review fallback
- Alert when issues detected

### Can I run skills offline?

It depends on the model:
- **Local models (LLaMA):** Yes, completely offline
- **API-based models:** No, requires internet
- **Hybrid:** Review locally, summarize with API

---

## Community and Support

### How do I report a bug?

1. Go to GitHub Issues
2. Search for similar issues
3. Create a new issue with:
   - Skill name
   - What went wrong
   - Steps to reproduce
   - Expected versus actual behavior
   - Your setup details

### How do I request a new skill?

Create a GitHub Discussion or Issue titled "Feature Request: [Skill Name]" with:
- What the skill should do
- Why it is valuable
- Your use case
- Any relevant links or examples

### Can I contribute a skill?

Yes. Check CONTRIBUTING.md for guidelines. We welcome:
- New skills
- Improvements to existing skills
- Better documentation
- Bug fixes
- Examples and use cases

### Where can I get help?

Multiple places:
- Check the README and FAQ
- GitHub Discussions (community help)
- GitHub Issues (bug reports)
- Check if maintainers list email
- Star the repo to stay updated

---

## Common Issues

### "Skill not found" error

**Solution:** Make sure the skill folder is in the correct location and your configuration has the right path.

### Agent responses are too long or too short

**Solution:** Adjust the verbosity setting in your skill configuration:
```yaml
verbosity: low  # shorter responses
# or
verbosity: high  # more detailed
```

### Reviews take too long

**Solution:** Use a faster model or limit the review scope:
```yaml
ai_model: "gpt-3.5-turbo"  # Faster than GPT-4
check_performance: false   # Skip if not needed
```

### Cost is too high

**Solution:**
1. Use a cheaper model (GPT-3.5 instead of GPT-4)
2. Use a self-hosted model (free but slower)
3. Limit review scope and frequency
4. Use Claude (costs less than GPT-4)

### Agent is making mistakes

**Solution:**
1. Use a better model (GPT-4 is better than GPT-3.5)
2. Provide better PR descriptions
3. Include clearer code comments
4. Check your configuration settings

---

## Before You Ask

Please check these first:
- README.md - Project overview
- Skill's own documentation - Each skill has detailed guides
- GitHub Issues - Your question might be answered
- GitHub Discussions - Ask community members
- This FAQ - Covers common questions

---

## Still Have Questions?

We would love to help.

1. **Check GitHub Discussions** - Join the community
2. **Read the Full Skill Documentation** - Most questions are answered there
3. **Create an Issue** - For bugs or specific problems
4. **Check Back Later** - We update this FAQ regularly

---

**Last Updated:** April 14, 2026  
**Version:** 1.0

---

*Thank you for using AI Agent Skills. We are constantly improving based on your feedback.*