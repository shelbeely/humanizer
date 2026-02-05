# AI Agent Skills Repository

This repository contains agent skills following the [Agent Skills specification](https://agentskills.io/) for improving writing quality:

## Skills Available

### 1. Inclusive Humanizer (Recommended for Text)
**Location:** `inclusive-humanizer/`

A comprehensive skill that combines both humanizing AI text AND ensuring trans inclusivity. This is the recommended skill for documentation, blog posts, articles, and any written content.

**What it does:**
- Removes AI writing patterns (promotional language, filler phrases, AI vocabulary, formulaic patterns)
- Ensures trans-inclusive language (fixes gendered assumptions, outdated terminology, binary-only language)
- Makes text sound authentic, natural, and respectful

### 2. Inclusive Software (NEW - Recommended for Code/UI)
**Location:** `inclusive-software/`

A comprehensive skill for making software accessible and inclusive for all users. Use when building or reviewing software products, interfaces, APIs, and technical systems.

**What it does:**
- Ensures accessibility (WCAG AA compliance, keyboard navigation, screen reader support)
- Implements gender inclusivity in forms, data models, and UI
- Addresses cultural sensitivity (i18n, diverse examples, flexible formats)
- Supports age and economic diversity (font sizes, offline support, performance)
- Promotes representation in code (diverse test data, documentation examples)

### 3. Humanizer (Standalone)
**Location:** `SKILL.md` (root)

Focuses solely on removing signs of AI-generated writing based on Wikipedia's "Signs of AI writing" guide.

### 4. Trans Inclusivity (Standalone)
**Location:** `TRANS_INCLUSIVITY_SKILL.md`

Focuses solely on reviewing and improving text for trans-inclusive language.



## Installation

### Recommended: Clone the Repository

Clone the entire repository to get all skills:

```bash
git clone https://github.com/shelbeely/humanizer.git ~/.claude/skills/humanizer
```

This installs:
- `/inclusive-humanizer` - Combined skill for text (AI patterns + trans inclusivity)
- `/inclusive-software` - Combined skill for software (accessibility + inclusivity)
- `/humanizer` - Standalone humanizer  
- `/trans-inclusivity` - Standalone trans inclusivity (from TRANS_INCLUSIVITY_SKILL.md)

### Alternative: Install Individual Skills

If you only want specific skills:

**Inclusive Humanizer (for text):**
```bash
mkdir -p ~/.claude/skills/inclusive-humanizer
curl -o ~/.claude/skills/inclusive-humanizer/SKILL.md https://raw.githubusercontent.com/shelbeely/humanizer/main/inclusive-humanizer/SKILL.md
```

**Inclusive Software (for code/UI):**
```bash
mkdir -p ~/.claude/skills/inclusive-software
curl -o ~/.claude/skills/inclusive-software/SKILL.md https://raw.githubusercontent.com/shelbeely/humanizer/main/inclusive-software/SKILL.md
```

**Humanizer only:**
```bash
mkdir -p ~/.claude/skills/humanizer
curl -o ~/.claude/skills/humanizer/SKILL.md https://raw.githubusercontent.com/shelbeely/humanizer/main/SKILL.md
```

**Trans Inclusivity only:**
```bash
mkdir -p ~/.claude/skills/trans-inclusivity
curl -o ~/.claude/skills/trans-inclusivity/SKILL.md https://raw.githubusercontent.com/shelbeely/humanizer/main/TRANS_INCLUSIVITY_SKILL.md
```


## Usage

### Inclusive Humanizer (For Text/Documentation)

For comprehensive text improvement (removes AI patterns AND ensures inclusivity):

```
/inclusive-humanizer

[paste your text here]
```

Or ask Claude directly:
```
Please review and improve this text for both AI patterns and trans inclusivity: [your text]
```

### Inclusive Software (For Code/UI/Forms)

For making software accessible and inclusive:

```
/inclusive-software

[paste your code, describe your UI, or ask for review]
```

Or ask Claude directly:
```
Please review this form for inclusivity and accessibility issues: [your code]
```

### Individual Skills

**Humanizer only** (remove AI writing patterns):
```
/humanizer
[paste your text]
```

**Trans Inclusivity only** (review for inclusive language):
```
/trans-inclusivity
[paste your text]
```

## Why Use These Skills?

### The Problem

Modern software and documentation often have overlapping issues:

1. **Text Issues:**
   - Robotic AI patterns (formulaic language, promotional tone, vague claims)
   - Exclusionary language (gendered assumptions, binary-only options, outdated terminology)

2. **Software Issues:**
   - Inaccessible interfaces (poor contrast, no keyboard support, missing alt text)
   - Non-inclusive design (binary gender fields, culturally-specific assumptions)
   - Limited representation (Western-only examples, gendered defaults)

### The Solutions

**Inclusive Humanizer** fixes text issues, making content that is:
- Natural and authentic (not robotic)
- Specific and concrete (not vague)
- Respectful and inclusive (not exclusionary)

**Inclusive Software** fixes code/UI issues, creating products that:
- Work for users with disabilities (WCAG AA accessible)
- Support diverse gender identities (inclusive forms and data models)
- Respect cultural differences (i18n, diverse examples)
- Accommodate all users (age, economic constraints, technical ability)

**Use together for:**
- Technical documentation that's both well-written AND accessible
- Forms that use natural language AND inclusive fields
- Error messages that are clear AND respectful
- READMEs and docs with authentic voice AND diverse examples

### Key Insight from Wikipedia

> "LLMs use statistical algorithms to guess what should come next. The result tends toward the most statistically likely result that applies to the widest variety of cases."

## 24 Patterns Detected (with Before/After Examples)

### Content Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 1 | **Significance inflation** | "marking a pivotal moment in the evolution of..." | "was established in 1989 to collect regional statistics" |
| 2 | **Notability name-dropping** | "cited in NYT, BBC, FT, and The Hindu" | "In a 2024 NYT interview, she argued..." |
| 3 | **Superficial -ing analyses** | "symbolizing... reflecting... showcasing..." | Remove or expand with actual sources |
| 4 | **Promotional language** | "nestled within the breathtaking region" | "is a town in the Gonder region" |
| 5 | **Vague attributions** | "Experts believe it plays a crucial role" | "according to a 2019 survey by..." |
| 6 | **Formulaic challenges** | "Despite challenges... continues to thrive" | Specific facts about actual challenges |

### Language Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 7 | **AI vocabulary** | "Additionally... testament... landscape... showcasing" | "also... remain common" |
| 8 | **Copula avoidance** | "serves as... features... boasts" | "is... has" |
| 9 | **Negative parallelisms** | "It's not just X, it's Y" | State the point directly |
| 10 | **Rule of three** | "innovation, inspiration, and insights" | Use natural number of items |
| 11 | **Synonym cycling** | "protagonist... main character... central figure... hero" | "protagonist" (repeat when clearest) |
| 12 | **False ranges** | "from the Big Bang to dark matter" | List topics directly |

### Style Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 13 | **Em dash overuse** | "institutions—not the people—yet this continues—" | Use commas or periods |
| 14 | **Boldface overuse** | "**OKRs**, **KPIs**, **BMC**" | "OKRs, KPIs, BMC" |
| 15 | **Inline-header lists** | "**Performance:** Performance improved" | Convert to prose |
| 16 | **Title Case Headings** | "Strategic Negotiations And Partnerships" | "Strategic negotiations and partnerships" |
| 17 | **Emojis** | "🚀 Launch Phase: 💡 Key Insight:" | Remove emojis |
| 18 | **Curly quotes** | `said “the project”` | `said "the project"` |

### Communication Patterns

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 19 | **Chatbot artifacts** | "I hope this helps! Let me know if..." | Remove entirely |
| 20 | **Cutoff disclaimers** | "While details are limited in available sources..." | Find sources or remove |
| 21 | **Sycophantic tone** | "Great question! You're absolutely right!" | Respond directly |

### Filler and Hedging

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 22 | **Filler phrases** | "In order to", "Due to the fact that" | "To", "Because" |
| 23 | **Excessive hedging** | "could potentially possibly" | "may" |
| 24 | **Generic conclusions** | "The future looks bright" | Specific plans or facts |

## Full Example

**Before (AI-sounding):**
> Great question! Here is an essay on this topic. I hope this helps!
>
> AI-assisted coding serves as an enduring testament to the transformative potential of large language models, marking a pivotal moment in the evolution of software development. In today's rapidly evolving technological landscape, these groundbreaking tools—nestled at the intersection of research and practice—are reshaping how engineers ideate, iterate, and deliver, underscoring their vital role in modern workflows.
>
> At its core, the value proposition is clear: streamlining processes, enhancing collaboration, and fostering alignment. It's not just about autocomplete; it's about unlocking creativity at scale, ensuring that organizations can remain agile while delivering seamless, intuitive, and powerful experiences to users. The tool serves as a catalyst. The assistant functions as a partner. The system stands as a foundation for innovation.
>
> Industry observers have noted that adoption has accelerated from hobbyist experiments to enterprise-wide rollouts, from solo developers to cross-functional teams. The technology has been featured in The New York Times, Wired, and The Verge. Additionally, the ability to generate documentation, tests, and refactors showcases how AI can contribute to better outcomes, highlighting the intricate interplay between automation and human judgment.
>
> - 💡 **Speed:** Code generation is significantly faster, reducing friction and empowering developers.
> - 🚀 **Quality:** Output quality has been enhanced through improved training, contributing to higher standards.
> - ✅ **Adoption:** Usage continues to grow, reflecting broader industry trends.
>
> While specific details are limited based on available information, it could potentially be argued that these tools might have some positive effect. Despite challenges typical of emerging technologies—including hallucinations, bias, and accountability—the ecosystem continues to thrive. In order to fully realize this potential, teams must align with best practices.
>
> In conclusion, the future looks bright. Exciting times lie ahead as we continue this journey toward excellence. Let me know if you’d like me to expand on any section!

**After (Humanized):**
> AI coding assistants speed up some tasks. In a 2024 study by Google, developers using Codex completed simple functions 55% faster than a control group, but showed no improvement on debugging or architectural decisions.
>
> The tools are good at boilerplate: config files, test scaffolding, repetitive refactors. They are bad at knowing when they are wrong. I have mass-accepted suggestions that compiled, passed lint, and still did the wrong thing because I stopped paying attention.
>
> Mira, an engineer at a fintech startup I interviewed, said she uses Copilot "like autocomplete for boring code" but reviews every line before committing. Jake, a senior dev at a larger company, disabled it after it kept suggesting patterns from a deprecated internal library.
>
> The productivity claims are hard to verify. GitHub says Copilot users "accept 30% of suggestions," but acceptance is not correctness, and correctness is not value. The 2024 Uplevel study found no statistically significant difference in pull-request throughput between teams with and without AI assistants.
>
> None of this means the tools are useless. It means they are tools. They do not replace judgment, and they do not eliminate the need for tests. If you do not have tests, you cannot tell whether the suggestion is right.

## Example Transformation

**Before (AI-generated, non-inclusive):**
> Great question! In today's rapidly evolving technological landscape, developers—both men and women—are leveraging groundbreaking tools that serve as a testament to human ingenuity. Additionally, each programmer should ensure his code is well-documented. It's not just about functionality; it's about fostering a vibrant ecosystem where mankind can thrive. The future looks bright!

**After (Inclusive Humanizer applied):**
> Developers use various tools to write better code. Each programmer should document their code thoroughly. Good documentation helps everyone understand and maintain the codebase.

**What changed:**
- ❌ Removed AI patterns: "Great question!", "rapidly evolving landscape," "testament to," "leveraging," "groundbreaking," "fostering," "vibrant ecosystem," "thrive," "future looks bright"
- ✅ Fixed inclusivity: "men and women" → "developers," "his code" → "their code," "mankind" → "everyone"
- ✨ Added authenticity: Specific, concrete statements instead of vague promotional claims

## Key Patterns Addressed

### AI Writing Patterns (24 total)
- Significance inflation, promotional language, vague attributions
- AI vocabulary overload ("leverage," "foster," "landscape")
- Copula avoidance ("serves as" → "is")
- Rule of three, negative parallelisms, em dash overuse
- Chatbot artifacts, excessive hedging, generic conclusions
- [See full list in SKILL.md]

### Inclusivity Patterns (10+ total)
- Binary gender assumptions (Male/Female only options)
- Gendered assumptions about people (assuming "he" for developers)
- Outdated terminology ("transsexual," "sex change," "preferred pronouns")
- Unnecessarily gendered terms ("mankind," "manpower," "guys")
- Biological essentialism ("only women can get pregnant")
- [See full list in inclusive-humanizer/SKILL.md]

## Agent Skills Standard

All skills follow the [Agent Skills specification](https://agentskills.io/), an open standard maintained by Anthropic for teaching AI agents new capabilities. Each skill:
- Has a `SKILL.md` file with YAML frontmatter
- Contains detailed instructions and examples
- Works across AI agent platforms that support the standard
- Can be discovered and loaded automatically by agents

## References

### AI Writing Patterns
- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) - Primary source, maintained by WikiProject AI Cleanup
- Based on observations of thousands of AI-generated text instances

### Trans Inclusivity
- [GLAAD Media Reference Guide](https://www.glaad.org/reference/trans-terms) - Trans terminology and media best practices
- [Trans Journalists Association Style Guide](https://transjournalists.org/style-guide/) - Journalistic standards
- [Human Rights Campaign](https://www.hrc.org/resources/glossary-of-terms) - Terminology and workplace inclusion

## Version History

### Inclusive Humanizer
- **1.0.0** - Initial release (2026)
  - Combined humanizer and trans inclusivity patterns
  - 24 AI writing patterns + 10+ inclusivity patterns
  - Integrated examples showing both fixes together
  - Context-specific guidance for documentation, medical, historical contexts

### Humanizer (Standalone)
- **2.1.1** - Fixed pattern #18 example (curly quotes vs straight quotes)
- **2.1.0** - Added before/after examples for all 24 patterns
- **2.0.0** - Complete rewrite based on raw Wikipedia article content
- **1.0.0** - Initial release

### Trans Inclusivity (Standalone)
- **1.0.0** - Initial release (2026)
  - Core patterns for trans-inclusive language
  - Examples across multiple contexts
  - Guidance on pronouns, terminology, and erasure

## Contributing

Contributions are welcome! If you've identified new patterns or have suggestions for improvements, please open an issue or pull request.

For the Trans Inclusivity skill specifically, we welcome feedback from trans and non-binary individuals to ensure the guidance remains current and respectful.

## License

MIT
