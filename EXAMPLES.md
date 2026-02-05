# Usage Examples

This document provides practical examples of using the inclusive-humanizer skill for different types of content.

## Example 1: Technical Documentation

**Original (AI-generated, non-inclusive):**
> Great question! In today's rapidly evolving technological landscape, every developer—both men and women—should leverage cutting-edge authentication tools that serve as a testament to modern security practices. Additionally, each programmer must ensure his API endpoints are properly secured. It's not just about authentication; it's about fostering a vibrant ecosystem where mankind can build innovative solutions. Despite the challenges typical of API development, the community continues to thrive. The future looks bright!

**After Inclusive Humanizer:**
> Developers should use modern authentication tools for their APIs. Each programmer must secure their API endpoints with proper authentication. According to the 2024 OWASP Top 10, broken authentication remains a critical vulnerability. Auth0 and Okta both offer OAuth 2.0 implementations that handle common security issues. Most teams take 2-3 weeks to integrate these tools into existing applications.

**What Changed:**
- Removed: Chatbot artifacts, AI vocabulary ("rapidly evolving," "leverage," "cutting-edge," "testament," "fostering," "vibrant ecosystem," "thrive"), vague claims
- Fixed: "men and women" → "developers," "his API" → "their API," "mankind" → removed
- Added: Specific technical details, concrete timeframes, and credible sources

---

## Example 2: Job Posting

**Original:**
> We're seeking a talented businessman to join our groundbreaking team! This pivotal role serves as a testament to our commitment to excellence. The ideal candidate should leverage his extensive experience to foster innovation. Both men and women are encouraged to apply. What are your preferred pronouns?

**After Inclusive Humanizer:**
> We're hiring a Business Development Manager. This role focuses on client acquisition and partnership development. The ideal candidate has 5+ years of experience in B2B sales, preferably in SaaS. What are your pronouns?

**What Changed:**
- Removed: AI vocabulary, promotional language, formulaic patterns
- Fixed: "businessman" → "Business Development Manager," "his experience" → gender-neutral phrasing, "men and women" → removed (inclusive by default), "preferred pronouns" → "pronouns"
- Added: Specific role title, concrete requirements

---

## Example 3: Blog Post

**Original:**
> Additionally, the system enhances security for users—regardless of whether they're male or female. Industry experts have noted that this groundbreaking approach marks a pivotal moment in cloud computing. It's not just about speed; it's about fostering trust and ensuring scalability. Each administrator should configure his settings carefully. The future looks bright for this technology!

**After Inclusive Humanizer:**
> The system encrypts user data at rest and in transit. In a 2024 security audit by Trail of Bits, the system had zero critical vulnerabilities. Administrators should enable two-factor authentication and review access logs weekly. The team plans to add hardware security key support in Q3.

**What Changed:**
- Removed: AI vocabulary, vague claims, promotional language, generic conclusions
- Fixed: "male or female" → removed (unnecessary), "his settings" → "administrators should" (no pronoun needed)
- Added: Specific security measures, concrete audit results, future plans

---

## Example 4: README File

**Original:**
> ## Installation

> Great question! Here's how to install this groundbreaking library. In order to get started, every developer must ensure his system meets the requirements. Both men and women in the community have leveraged this tool to enhance their projects. The installation process serves as a testament to our commitment to simplicity.

> ```bash
> npm install example-lib
> ```

> Let me know if you need help!

**After Inclusive Humanizer:**
> ## Installation

> Requires Node.js 18+ and npm 9+.

> ```bash
> npm install example-lib
> ```

> See [troubleshooting.md](troubleshooting.md) if you encounter errors.

**What Changed:**
- Removed: All chatbot artifacts, AI vocabulary, promotional language
- Fixed: Gender-neutral by not referencing developers by gender at all
- Added: Specific version requirements, link to troubleshooting

---

## Example 5: User Interface Text

**Original:**
> Welcome! Please select your gender below:
> - Male
> - Female
>
> Each user should update his profile settings to enhance his experience.

**After Inclusive Humanizer:**
> Welcome! Please select your gender (optional):
> - Man
> - Woman
> - Non-binary
> - Prefer to self-describe: _______
> - Prefer not to say
>
> Update your profile settings to customize your experience.

**What Changed:**
- Fixed: Binary gender options → inclusive options, made field optional
- Fixed: "his profile" → "your profile" (second person, avoids gendering)
- Removed: AI enhancement language

---

## Example 6: Error Messages

**Original:**
> The user has exceeded his rate limit. He should try again later or contact his administrator.

**After Inclusive Humanizer:**
> Rate limit exceeded. Try again in 5 minutes or contact your administrator.

**What Changed:**
- Fixed: "his rate limit" → "rate limit," "He should" → "Try," "his administrator" → "your administrator"
- Added: Specific timeframe (5 minutes)
- Made more concise and clear

---

## Example 7: API Documentation

**Original:**
> This endpoint serves as a powerful tool for developers to leverage when they need to enhance their applications. Each developer must provide his API key in the header. Both men and women can access this groundbreaking feature.

**After Inclusive Humanizer:**
> Send a `GET` request to `/api/v1/users` with your API key in the `Authorization` header:

> ```
> Authorization: Bearer YOUR_API_KEY
> ```

**What Changed:**
- Removed: Promotional language, AI patterns, unnecessary gender references
- Fixed: Made gender-neutral by using "your" instead of "his"
- Added: Specific HTTP method, endpoint, header format with example

---

## Example 8: Form Instructions

**Original:**
> Each applicant should submit his or her resume and cover letter. Both men and women are encouraged to apply. Please indicate if you are male or female. Mankind has made great progress in this field!

**After Inclusive Humanizer:**
> Submit your resume and cover letter. All qualified candidates are encouraged to apply.

> Gender identity (optional):
> ☐ Man
> ☐ Woman  
> ☐ Non-binary
> ☐ Prefer to self-describe: _______
> ☐ Prefer not to say

**What Changed:**
- Fixed: "his or her" → "your," removed unnecessary "men and women" statement
- Fixed: Binary gender question → inclusive options with opt-out
- Removed: Completely unnecessary "mankind" reference

---

## Tips for Best Results

1. **Be specific**: Replace vague AI claims with concrete details, numbers, and sources
2. **Use "they/them"**: When gender is unknown, singular "they" is grammatically correct
3. **Remove redundancy**: AI often restates things unnecessarily with gender markers
4. **Question necessity**: Do you really need to ask for gender? If yes, make it inclusive
5. **Second person**: "Your settings" avoids gendering entirely
6. **Active voice**: "Update your profile" instead of "The user should update his profile"

---

## When NOT to Use This Skill

This skill may not be appropriate for:
- **Historical quotes**: Don't change quoted text to make it inclusive
- **Legal documents**: May require specific legal language (consult a lawyer)
- **Deliberate style choices**: Some authors intentionally use formal or poetic language
- **Cultural context**: Some languages/contexts have different norms

Always consider the context and purpose of your text!
