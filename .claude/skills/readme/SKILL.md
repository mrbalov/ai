---
name: readme
description: |
  Generates a complete, consistent README.md file for the current repository by automatically discovering all skills in the @skills/ folder and creating a formatted skills inventory table. The skill scans SKILL.md files in each skill directory, extracts metadata from YAML frontmatter, and outputs a fully regenerated README with title, description, skills table (Skill | Description | Documentation columns), and license footer. Use this skill whenever you need to generate or update the README.md file, especially after adding new skills, modifying skill descriptions, or maintaining consistency across the documentation. Always invoke this skill to keep README.md in sync with actual skills in the repository.
license: MIT
metadata:
  author: Mr.B.Lab
---

# README Generator Skill

## Overview

This skill automatically generates a complete, consistent README.md file for your project by discovering all available skills and formatting them into a structured documentation file. It ensures your README always reflects the current state of your skills directory.

## What This Skill Does

1. **Discovers all skills** — Scans ONLY the `/skills/` directory for all skill folders
2. **Extracts metadata** — Reads each skill's `SKILL.md` file and parses YAML frontmatter to get:
   - Skill name
   - Description
   - License (if present)
3. **Generates README** — Creates a complete, formatted README.md with:
   - Project title and description
   - Skills inventory table with columns: Skill | Description | Documentation
   - License footer
4. **Clears and replaces** — Completely overwrites the existing README.md to ensure no stale content persists

## Discovery Process

### Step 1: Locate Skills Directory

Search for skills ONLY in the following folder: `/skills/` (project root). Do NOT scan any other directories or subdirectories outside of this path. This ensures we only document actual skills and not unrelated files.

### Step 2: Scan for SKILL.md Files

For each subdirectory in the skills folder:
- Look for a `SKILL.md` file
- If found, extract the YAML frontmatter at the top of the file
- Skip directories without SKILL.md files

### Step 3: Extract Metadata

From each SKILL.md frontmatter, extract:
- `name` — The skill identifier (use this as the table skill name)
- `description` — The skill description (first paragraph or line only, ~100 words max for the table)
- `license` — Optional license field

**Parsing pattern:**
```yaml
---
name: skill-name
description: |
  Skill description text here
license: MIT
metadata:
  author: Name
---
```

Treat the `---` delimiters as YAML block markers. Extract only content between the opening and closing `---`.

## README Output Format

**ALWAYS generate the README with this exact structure:**

```markdown
# AI Skills & Tools 🤖

This is the place where I gather personally developed and reusable AI stuff for my everyday software development activities.

## 🛠️ Skills

| Skill | Description | Documentation |
|-------|-------------|-----------------|
| **skill-name** | Skill description text (truncated to ~100 words) | [README.md](skills/skill-name/README.md) [SKILL.md](skills/skill-name/SKILL.md) |
| **another-skill** | Another skill description | [README.md](skills/another-skill/README.md) [SKILL.md](skills/another-skill/SKILL.md) |

## License

MIT
```

### Table Format Requirements

- **Skill column**: Format as `**skill-name**` (bold, lowercase name from frontmatter)
- **Description column**: Include the first 100-150 words of the skill description. Truncate longer descriptions with "..." if needed. Do NOT include line breaks within the description cell.
- **Documentation column**: Create markdown links to:
  - `[README.md](skills/skill-name/README.md)` (point to the skill's README if it exists)
  - `[SKILL.md](skills/skill-name/SKILL.md)` (always point to the skill's SKILL.md)
  - If README.md doesn't exist in the skill folder, omit that link and only include SKILL.md

## Handling Edge Cases

- **No skills found**: Generate README with an empty skills table and a note: "(No skills discovered)"
- **Malformed SKILL.md**: Skip the skill and log a warning, continue processing others
- **Missing fields**: 
  - If name is missing, use the folder name as the skill name
  - If description is missing, use "(No description available)"
- **Multiple skills**: Sort alphabetically by skill name
- **Skill name variations**: Always use the `name` field from frontmatter, never the folder name (unless name is missing)

## Destructive Operation: Clear Existing README

**This skill ALWAYS clears the existing README.md before writing the new one.**

Before generating:
1. Check if README.md exists in the project root
2. If it exists, **delete its entire contents**
3. Write the newly generated README from scratch

This ensures no stale content, outdated sections, or merge conflicts persist. The README is completely regenerated every time.

**Why this matters**: If you don't clear the old file, sections might be duplicated, descriptions might become out of sync, or the footer might be corrupted. A complete regeneration is the only way to guarantee consistency.

## Success Criteria

✅ README.md exists in project root
✅ Title and intro text match the template
✅ Skills table is formatted correctly (Skill | Description | Documentation)
✅ All skills from `skills/` folder are listed in the table
✅ Skill names are bold and match frontmatter `name` field
✅ Descriptions are truncated to ~100-150 words
✅ Documentation links point to correct SKILL.md files
✅ Skills are sorted alphabetically
✅ License footer is present and correct
✅ Old README.md was completely replaced (no stale content)
✅ No malformed table syntax
✅ No line breaks or special characters breaking table cells

## When to Use

- **After adding new skills**: Regenerate README to include them
- **After updating skill descriptions**: Keep README in sync with actual skill metadata
- **Before releases**: Ensure documentation is current and complete
- **Onboarding**: Generate fresh documentation for new team members
- **Documentation maintenance**: Periodically regenerate to catch drift

## Key Characteristics

- **Completely regenerated** — No stale data persists; old README is deleted before writing new one
- **Consistent format** — Every invocation produces identical table format and structure
- **Automated discovery** — No manual updates needed; scans actual skill files
- **Alphabetically sorted** — Skills listed in predictable order
- **Metadata-driven** — Extracts from authoritative SKILL.md frontmatter, not hardcoded
