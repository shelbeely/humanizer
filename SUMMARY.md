# Repository Summary

This repository provides **Agent Skills** for improving text and software inclusivity, following the [Agent Skills specification](https://agentskills.io/).

## What Was Accomplished

Based on the original question "Can we use this as a base for an agent skill for trans inclusivity?", this repository now contains:

### ✅ Four Complete Agent Skills

1. **Humanizer** (`SKILL.md`) - Removes AI writing patterns
2. **Trans Inclusivity** (`TRANS_INCLUSIVITY_SKILL.md`) - Trans-inclusive language for text
3. **Inclusive Humanizer** (`inclusive-humanizer/SKILL.md`) - Combined: AI pattern removal + trans inclusivity
4. **LGBTQ-Inclusive Software** (`inclusive-software/SKILL.md`) - Making software LGBTQ-inclusive

### Skills Overview

#### Inclusive Humanizer (For Text/Documentation)
**Purpose:** Review and improve text to remove AI writing patterns while ensuring trans inclusivity.

**Covers:**
- 24 AI writing patterns from Wikipedia's "Signs of AI writing"
- 10+ trans inclusivity patterns (pronouns, gender-neutral language, etc.)
- Combined approach fixing both issues simultaneously
- Context-specific guidance for documentation, medical, historical contexts

**Use for:** Blog posts, documentation, articles, README files, technical writing

---

#### LGBTQ-Inclusive Software (For Code/UI/Systems)
**Purpose:** Review and improve software for LGBTQ inclusivity across gender identity, sexual orientation, and relationships.

**Covers:**

**Gender Identity:**
- Non-binary gender fields (not just Male/Female)
- Pronoun support (she/her, he/him, they/them, ze/zir)
- Name change handling (no deadnaming)
- Title fields (includes Mx.)
- Database schemas (flexible VARCHAR, not ENUM)
- Privacy controls (users control disclosure)

**Sexual Orientation & Relationships:**
- Neutral relationship terms ("partner" not "wife/husband")
- Same-sex relationship support
- Non-traditional family structures
- Flexible emergency contact fields
- Diverse relationship status options
- Privacy for relationship disclosure

**Technical Implementation:**
- Form design (inclusive options, optional fields)
- Database schemas (flexible, privacy-respecting)
- API design (no exposure of sensitive info)
- Validation logic (accepting diverse identities)
- UI language (gender-neutral messaging)
- Test data (LGBTQ representation)

**Use for:** User registration forms, profile systems, relationship/family fields, database design, API development, UI/UX review

---

## Installation

```bash
# Clone entire repository (recommended)
git clone https://github.com/shelbeely/humanizer.git ~/.claude/skills/humanizer
```

This provides:
- `/inclusive-humanizer` - For text (AI patterns + trans inclusivity)
- `/inclusive-software` - For software (LGBTQ inclusivity in code/UI)
- `/humanizer` - Standalone AI pattern remover
- `/trans-inclusivity` - Standalone trans-inclusive language reviewer

## Usage Examples

### Text Review
```
/inclusive-humanizer

Great question! In today's rapidly evolving landscape, every developer—both 
men and women—should ensure his code is properly documented.
```

**Output:** Removes AI patterns AND fixes gendered language.

---

### Software Review
```
/inclusive-software

Please review this user registration form:

<select name="gender" required>
  <option value="M">Male</option>
  <option value="F">Female</option>
</select>
<input name="spouse_name" placeholder="Husband/Wife Name" />
```

**Output:** Identifies binary gender field, heteronormative spouse field, provides LGBTQ-inclusive alternatives.

---

## Key Features

### Trans Inclusivity Coverage
- ✅ Gender fields (non-binary options)
- ✅ Pronouns (she/her, he/him, they/them, neopronouns)
- ✅ Name changes (chosen name support, no deadnaming)
- ✅ Titles (Mx. included)
- ✅ Database design (flexible schemas)
- ✅ Privacy controls
- ✅ Documentation examples

### Sexual Orientation & Relationships
- ✅ Partner terminology (not spouse/husband/wife)
- ✅ Same-sex relationships
- ✅ Diverse family structures
- ✅ Non-heteronormative language
- ✅ Relationship privacy
- ✅ Inclusive test data

### Technical Guidance
- ✅ Code examples (forms, validation, databases)
- ✅ Migration strategies (fixing existing systems)
- ✅ API design patterns
- ✅ Testing checklists
- ✅ Before/after comparisons

---

## Validation

All skills validated against Agent Skills specification:
- ✅ Valid YAML frontmatter
- ✅ Proper name format (lowercase, hyphens only)
- ✅ Description under 1024 characters
- ✅ Complete body content
- ✅ Follows progressive disclosure pattern

---

## Resources Referenced

### AI Writing Patterns
- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- WikiProject AI Cleanup

### LGBTQ Inclusivity
- [GLAAD Media Reference Guide](https://www.glaad.org/reference)
- [Trans Journalists Association Style Guide](https://transjournalists.org/style-guide/)
- [Human Rights Campaign](https://www.hrc.org/)

### Agent Skills Standard
- [AgentSkills.io](https://agentskills.io/)
- [GitHub: agentskills/agentskills](https://github.com/agentskills/agentskills)

---

## Answer to Original Question

**"Can we use this as a base for an agent skill for trans inclusivity?"**

✅ **YES** - The repository now contains TWO comprehensive skills for trans/LGBTQ inclusivity:

1. **inclusive-humanizer** - For making TEXT trans-inclusive (removes AI patterns + fixes gendered language)

2. **inclusive-software** - For making SOFTWARE LGBTQ-inclusive (covers gender identity, sexual orientation, relationships in code/UI/databases)

Both skills are production-ready, validated, and follow the Agent Skills specification. They can be used independently or together for comprehensive LGBTQ inclusivity across text and software systems.

---

## Contributing

Contributions welcome! Please open issues or PRs to:
- Add new patterns
- Update terminology to current best practices
- Provide additional examples
- Report issues or inaccuracies

LGBTQ inclusivity best practices evolve - feedback from LGBTQ community members is especially valued.

---

## License

MIT
