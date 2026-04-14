# Contributing to AI Agent Skills

Thank you for your interest in contributing to AI Agent Skills! This project thrives on community contributions. Whether you are adding new skills, fixing bugs, or improving documentation, we appreciate your help.

## Ways to Contribute

### 1. Add a New Skill
Is there an AI agent skill that would be valuable to the community? Submit it.

### 2. Improve an Existing Skill
Found a bug or have an improvement? Let us know.

### 3. Fix Documentation
Help us improve guides, examples, and instructions.

### 4. Report Issues
Found a problem? Create a detailed issue report.

### 5. Share Ideas
Have ideas for new skills? Start a discussion.

## Guidelines

### Before You Start

- Check existing issues and pull requests to avoid duplicates
- Ensure your contribution aligns with the project scope
- Test your changes thoroughly
- Write clear, simple English (this helps everyone)

### Skill Submission Requirements

For new skills, please include:

1. **SKILL.md** - Complete documentation following the template
2. **examples/** - Folder with real-world examples
3. **Clear Description** - What the skill does and why it is valuable
4. **Model Compatibility** - Which AI models work best with this skill
5. **Use Cases** - When and how to use this skill
6. **Configuration Guide** - How to set up and customize the skill
7. **Troubleshooting** - Common issues and solutions

### Documentation Standards

- Write in clear, simple English
- Include examples for every feature
- Add code blocks where appropriate
- Use headings and formatting for readability
- Keep sentences short and clear

## Skill Template

Use this structure for new skills:

```
skills/your-skill-name/
├── SKILL.md              # Main documentation
├── examples/
│   ├── example1.md       # Real-world example
│   └── example2.md       # Another example
└── config/
    └── default.yaml      # Default configuration
```

### SKILL.md Outline

```markdown
# Skill Name

## What This Skill Does

## How It Works

## Getting Started

## Best For (Model Compatibility)

## Real-World Examples

## Configuration and Customization

## Troubleshooting

## Need Help?

## Next Steps
```

## Submission Process

### Step 1: Fork the Repository
```bash
git clone https://github.com/yourusername/ai-agent-skills.git
cd ai-agent-skills
```

### Step 2: Create a Branch
```bash
git checkout -b add/your-skill-name
# or
git checkout -b fix/bug-description
```

### Step 3: Make Your Changes

Add your new skill or improvements to the appropriate directory.

### Step 4: Test Everything

- Verify all examples work
- Check documentation clarity
- Test with multiple AI models if applicable
- Ensure proper formatting and structure

### Step 5: Submit a Pull Request

```bash
git add .
git commit -m "Add new GitHub PR Review skill"
git push origin your-branch-name
```

Then create a pull request on GitHub with:
- Clear title (e.g., "Add GitHub PR Review Skill")
- Detailed description of what you added
- Why this skill is valuable
- Any special setup instructions

## Code Style

### Markdown Guidelines

- Use clear, simple sentences
- Keep paragraphs short
- Use bullet points for lists
- Use code blocks for technical content
- Avoid adding emojis to text content

### Naming Conventions

- Skill names: lowercase, hyphen-separated (github-pr-review)
- File names: descriptive, lowercase (SKILL.md, not skill_doc.txt)
- Directories: skill-name format

## Writing Style

We value clear, accessible writing:

- **Simple** - Use common words, avoid jargon
- **Clear** - Short sentences, clear intent
- **Practical** - Include real examples
- **Helpful** - Focus on what readers need to know
- **Professional** - Maintain a helpful, respectful tone

## Review Process

1. **Submission** - You submit your pull request
2. **Initial Review** - We check it meets guidelines
3. **Feedback** - We provide suggestions if needed
4. **Revisions** - You make any requested changes
5. **Approval** - Once approved, we merge your contribution
6. **Release** - Your skill becomes available for everyone

## What We Do Not Accept

- Paid/commercial skills (we are open source and free)
- Skills that require expensive external APIs without open alternatives
- Content that violates copyright or licenses
- Misleading or false documentation
- Offensive or inappropriate content

## Quality Standards

Your contribution should:

- Be well-documented
- Include clear examples
- Work with multiple AI models
- Be tested and verified
- Follow the project structure
- Have clear, simple English
- Be useful to the community

## Questions?

- Read the README.md for project overview
- Join our GitHub Discussions for questions
- Create an Issue for specific problems
- Check existing PRs to see what is being worked on

## First-Time Contributors

Never contributed to open source before? Welcome! Here is what to know:

1. **Fork** - Create your own copy of the repository
2. **Branch** - Create a branch for your changes
3. **Commit** - Make your changes with clear commit messages
4. **Push** - Push to your fork
5. **Pull Request** - Submit a PR explaining what you did

Do not worry about making it perfect—our community will help you refine it.

## Recognition

Contributors are recognized in our:
- CONTRIBUTORS.md file
- Monthly community highlights
- GitHub contributors page

## License

By contributing to this project, you agree that your contributions will be licensed under the MIT License, same as the project.

## Code of Conduct

- Be respectful and inclusive
- Welcome diverse ideas and perspectives
- Provide constructive feedback
- Help each other learn and grow
- Report inappropriate behavior to project maintainers

---

**Thank you for contributing to AI Agent Skills!**

Together, we are building the best skill library for AI agents. Your contributions make this project better for everyone.

**Happy contributing!**