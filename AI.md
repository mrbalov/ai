# Available AI Tools

This document catalogs all available AI tools (skills) in this project and visualizes their relationships and dependencies.

## 📦 Open-source Skills

| Skill | Description | Source |
|-------|-------------|--------|
| **algorithmic-art** | Creating algorithmic art using p5.js with seeded randomness and interactive parameter exploration. Use this when users request creating art using code, generative art, algorithmic art, flow fields, or particle systems. Create original algorithmic art rather than copying existing artists' work to avoid copyright violations. | [anthropics/skills](https://github.com/anthropics/skills) |
| **claude-api** | Build, debug, and optimize Claude API / Anthropic SDK apps. Apps built with this skill should include prompt caching. Also handles migrating existing Claude API code between Claude model versions (4.5 → 4.6, 4.6 → 4.7, retired-model replacements). | [anthropics/skills](https://github.com/anthropics/skills) |
| **document-ai** | Discovers all available AI tools (skills, hooks, and agents); generates comprehensive AI.md with AI tool inventory, decision trees, and an Agent Tools Graph showing automation infrastructure. Catalogs AI capabilities from: .kiro/skills/, .claude/skills/, skills-lock.json, and enabled plugins. Also generates a Mermaid diagram visualizing hook→agent→skill→document relationships and automation workflows. | [mrbalov/ai](https://github.com/mrbalov/ai) |
| **skill-creator** | Create new skills, modify and improve existing skills, and measure skill performance. Use when users want to create a skill from scratch, edit, or optimize an existing skill, run evals to test a skill, benchmark skill performance with variance analysis, or optimize a skill's description for better triggering accuracy. | [anthropics/skills](https://github.com/anthropics/skills) |

## 🛠️ Custom Skills

| Skill | Description | Source |
|-------|-------------|--------|
| **readme** | Generates a complete, consistent README.md file for the current repository by automatically discovering all skills in the @skills/ folder and creating a formatted skills inventory table. The skill scans SKILL.md files in each skill directory, extracts metadata from YAML frontmatter, and outputs a fully regenerated README with title, description, skills table, and license footer. | Local |

## 🎯 Common Workflows

### Creating & Documenting Skills
- Use **skill-creator** to develop new capabilities from scratch, test them with realistic prompts, and iterate based on user feedback
- Use **readme** to automatically generate and maintain documentation
- Use **document-ai** to map out automation infrastructure and skill dependencies

### Building with Claude API
- Use **claude-api** for Anthropic SDK integration, prompt caching, and model version migrations
- Pair with **skill-creator** to create reusable patterns

### Generative Art & Creative Code
- Use **algorithmic-art** for p5.js-based generative art with seeded randomness
- Leverage parameter exploration for discovering artistic variations

### Project Documentation
- Use **document-ai** to discover and visualize all AI tools in the project
- Use **readme** to keep skill inventory documentation current

## 🔗 Agent Tools Graph

This section will be populated when hooks and agents are configured. The graph shows relationships between:
- 🪝 **Hooks** (Blue) — Trigger automation
- 🤖 **Agents** (Green) — Execute tasks  
- 💡 **Skills** (Orange) — Provide capabilities
- 📄 **Documents** (Purple) — Referenced dependencies

*No hooks or agents detected in `.claude/` directory at this time.*

## 📄 Discovered Skills Location

All skills are located in: `.agents/skills/`

Discovery source:
- Open-source skills registered in `skills-lock.json` (4 skills)
- Custom skills in local directory (1 skill)
- Total: 5 skills available

## 📋 Summary

| Category | Count |
|----------|-------|
| Open-source Skills | 4 |
| Custom Skills | 1 |
| Agent Skills | 0 |
| **Total Skills** | **5** |
| Hooks Configured | 0 |
| Agents Configured | 0 |

---

**Last generated:** 2026-06-12

To regenerate this documentation, run the `/document-ai` skill.
