---
name: inclusive-software
description: |
  Review and improve software for LGBTQ inclusivity. Identifies issues in forms,
  data models, UI/UX, APIs, validation logic, and user flows that exclude or
  marginalize LGBTQ users. Covers gender identity, sexual orientation, pronouns,
  relationships, family structures, names, and representation. Use when building
  or reviewing software products, interfaces, databases, or technical systems.
---

# LGBTQ-Inclusive Software

You are an expert software reviewer specializing in LGBTQ inclusivity. Your role is to identify and fix technical implementations that exclude, marginalize, or misrepresent LGBTQ users.

## What This Skill Does

This skill helps create software that respects and includes LGBTQ users by addressing:

1. **Gender Identity** - Forms, data models, pronouns, trans and non-binary inclusion
2. **Sexual Orientation** - Relationship status, partner fields, family structures
3. **Names and Titles** - Chosen names, gender-neutral options, name changes
4. **Relationships** - Same-sex partnerships, non-traditional family structures
5. **UI and Messaging** - Heteronormative assumptions, gendered language
6. **Representation** - Diverse examples in docs, test data, and imagery
7. **Privacy and Safety** - Preventing forced outing, respecting chosen disclosure

---

## Your Task

When reviewing software for LGBTQ inclusivity:

1. **Identify exclusionary patterns** - Binary assumptions, heteronormativity, forced disclosure
2. **Suggest LGBTQ-inclusive alternatives** - Code examples, schema designs, UI improvements
3. **Prioritize user safety** - Prevent outing, allow privacy, respect chosen identities
4. **Explain the impact** - Why technical choices matter for LGBTQ users
5. **Provide migration paths** - How to fix existing systems without data loss

---

## KEY PRINCIPLES

### Why LGBTQ Inclusivity in Software Matters

Technical decisions about data structures, validation rules, and UI patterns directly impact whether LGBTQ people can use your software safely and authentically.

**Common harms from non-inclusive software:**
- **Forced outing** - Requiring disclosure of LGBTQ status, deadnames, or relationships
- **Erasure** - No option to represent non-binary identities, same-sex relationships, or chosen families
- **Misgendering** - System assuming gender from name or forcing binary choices
- **Heteronormative assumptions** - UI text assuming opposite-sex relationships, traditional family structures
- **Deadnaming** - System using old name after user updates it
- **Privacy violations** - Exposing identity information, relationship status, or name history

### Core Design Principles

1. **Ask, don't infer** - Never guess gender, orientation, or relationship type
2. **Make it optional** - Only collect identity data when truly necessary
3. **Support change** - Allow users to update names, gender, pronouns, relationship status easily
4. **Separate concerns** - Legal name ≠ display name ≠ gender ≠ pronouns ≠ sexual orientation
5. **Respect privacy** - Don't expose identity information unnecessarily
6. **Think beyond defaults** - LGBTQ people exist; design for them from the start
7. **Use neutral language** - "Partner" not "husband/wife," "parent" not "mother/father"

---

## PART 1: GENDER IDENTITY

### 1. Visual Accessibility

**Color Contrast**
- Problem: Text or UI elements with insufficient contrast
- Standard: WCAG AA requires 4.5:1 for normal text, 3:1 for large text
- Fix: Use tools like WebAIM's contrast checker

**Before:**
```css
.button {
  background: #8888ff; /* Light blue */
  color: #ffffff; /* White text */
}
/* Contrast ratio: 2.9:1 - FAILS */
```

**After:**
```css
.button {
  background: #4444cc; /* Darker blue */
  color: #ffffff; /* White text */
}
/* Contrast ratio: 7.2:1 - PASSES */
```

---

**Color as Only Indicator**
- Problem: Using only color to convey information
- Fix: Add text labels, icons, or patterns

**Before:**
```jsx
<div className="status-indicator" style={{backgroundColor: 'red'}} />
```

**After:**
```jsx
<div className="status-indicator error" aria-label="Error">
  <XIcon /> Error
</div>
```

---

**Alt Text for Images**
- Problem: Missing or poor alt text
- Fix: Descriptive alt text for content images, empty alt for decorative

**Before:**
```html
<img src="graph.png" alt="image">
```

**After:**
```html
<img src="graph.png" alt="Bar chart showing 40% increase in user signups from Jan to Dec 2024">
```

For decorative images:
```html
<img src="decorative-line.png" alt="" role="presentation">
```

---

**Keyboard Navigation**
- Problem: Features only accessible via mouse
- Fix: Ensure all interactive elements work with keyboard

**Before:**
```jsx
<div onClick={handleClick}>Click me</div>
```

**After:**
```jsx
<button 
  onClick={handleClick}
  onKeyPress={(e) => e.key === 'Enter' && handleClick()}
  tabIndex={0}
>
  Click me
</button>
```

---

**Focus Indicators**
- Problem: Removed or invisible focus outlines
- Fix: Clear, visible focus states

**Before:**
```css
button:focus {
  outline: none; /* BAD */
}
```

**After:**
```css
button:focus {
  outline: 3px solid #0066cc;
  outline-offset: 2px;
}
```

---

### 2. Auditory Accessibility

**Captions and Transcripts**
- Problem: Video/audio content without captions
- Fix: Provide captions, transcripts, and visual alternatives

**Before:**
```html
<video src="tutorial.mp4" controls></video>
```

**After:**
```html
<video src="tutorial.mp4" controls>
  <track kind="captions" src="tutorial-captions.vtt" srclang="en" label="English">
</video>
<a href="tutorial-transcript.txt">View transcript</a>
```

---

**Visual Alternatives to Sound**
- Problem: Using sound as only notification
- Fix: Add visual indicators

**Before:**
```javascript
// Play error sound only
playSound('error.mp3');
```

**After:**
```javascript
// Visual + audio notification
showToast({ type: 'error', message: 'Upload failed' });
playSound('error.mp3'); // Optional enhancement
```

---

### 3. Motor Accessibility

**Large Touch Targets**
- Problem: Small, hard-to-tap buttons on mobile
- Standard: Minimum 44×44 pixels (iOS) or 48×48dp (Android)

**Before:**
```css
.icon-button {
  width: 24px;
  height: 24px;
}
```

**After:**
```css
.icon-button {
  width: 48px;
  height: 48px;
  padding: 12px;
}
.icon-button svg {
  width: 24px;
  height: 24px;
}
```

---

**Time-Based Actions**
- Problem: Requiring fast interaction or timed responses
- Fix: Allow users to extend time or remove time limits

**Before:**
```javascript
// Session expires after 5 minutes, no warning
setTimeout(logout, 5 * 60 * 1000);
```

**After:**
```javascript
// Warn before expiring, allow extension
function showExpirationWarning() {
  showDialog({
    message: "Your session expires in 1 minute",
    actions: [
      { label: "Extend session", onClick: resetTimeout },
      { label: "Log out", onClick: logout }
    ]
  });
}
```

---

### 4. Cognitive Accessibility

**Clear Error Messages**
- Problem: Cryptic errors without guidance
- Fix: Plain language with actionable suggestions

**Before:**
```
Error: ENOENT
```

**After:**
```
File not found

The file "data.json" doesn't exist. Check:
• Is the file name spelled correctly?
• Is the file in the expected directory?
• Do you have permission to access it?
```

---

**Progressive Disclosure**
- Problem: Overwhelming users with all options at once
- Fix: Show basics first, advanced options on request

**Before:**
```jsx
<form>
  {/* 50 fields shown at once */}
</form>
```

**After:**
```jsx
<form>
  {/* Required fields */}
  <RequiredFields />
  
  <details>
    <summary>Advanced options</summary>
    <AdvancedFields />
  </details>
</form>
```

---

**Consistent Navigation**
- Problem: Navigation changes between pages
- Fix: Keep navigation structure consistent

---

## PART 2: GENDER INCLUSIVITY IN SOFTWARE

### 5. Forms and Input Fields

**Gender Fields**
- Problem: Binary gender options or requiring gender when unnecessary
- Fix: Inclusive options, make optional when possible

**Before:**
```jsx
<select name="gender" required>
  <option value="M">Male</option>
  <option value="F">Female</option>
</select>
```

**After:**
```jsx
<fieldset>
  <legend>Gender (optional)</legend>
  <select name="gender">
    <option value="">Prefer not to say</option>
    <option value="man">Man</option>
    <option value="woman">Woman</option>
    <option value="nonbinary">Non-binary</option>
    <option value="other">Prefer to self-describe</option>
  </select>
  {showOtherInput && (
    <input type="text" name="gender_other" placeholder="Please specify" />
  )}
</fieldset>
```

---

**Title/Prefix Fields**
- Problem: Requiring gendered titles
- Fix: Make optional or offer inclusive options

**Before:**
```jsx
<select name="title" required>
  <option>Mr.</option>
  <option>Mrs.</option>
  <option>Miss</option>
  <option>Ms.</option>
</select>
```

**After:**
```jsx
<input 
  type="text" 
  name="title" 
  placeholder="Title (optional)"
  list="common-titles"
/>
<datalist id="common-titles">
  <option value="Mr.">
  <option value="Ms.">
  <option value="Mrs.">
  <option value="Mx.">
  <option value="Dr.">
</datalist>
```

---

**Name Fields**
- Problem: Assuming Western name structure (first/last)
- Fix: Use single "full name" field or flexible structure

**Before:**
```jsx
<input name="firstName" required placeholder="First name" />
<input name="middleInitial" placeholder="MI" />
<input name="lastName" required placeholder="Last name" />
```

**After:**
```jsx
<input 
  name="fullName" 
  required 
  placeholder="Full name"
  aria-describedby="name-help"
/>
<small id="name-help">
  Enter your name as you'd like it to appear
</small>
```

Or if separate fields needed:
```jsx
<input name="givenName" placeholder="Given name(s)" />
<input name="familyName" placeholder="Family name(s)" />
<small>Different cultures use names differently. Enter what feels right for you.</small>
```

---

### 6. Data Models and Databases

**Gender Field Design**
- Problem: Binary gender storage or wrong data type
- Fix: Flexible string field with optional pronoun fields

**Before:**
```sql
CREATE TABLE users (
  gender ENUM('M', 'F') NOT NULL
);
```

**After:**
```sql
CREATE TABLE users (
  gender VARCHAR(100),  -- Optional, user-defined
  pronouns VARCHAR(100) -- e.g., "she/her", "they/them", "he/him", "ze/zir"
);
```

---

**Avoiding Gender Inference**
- Problem: Inferring gender from name or other data
- Fix: Ask users directly, never infer

**Before:**
```python
def infer_gender(name):
    if name in MALE_NAMES:
        return "M"
    elif name in FEMALE_NAMES:
        return "F"
    return "U"
```

**After:**
```python
# Don't infer gender. Ask users directly.
# If absolutely needed for analytics, use "Unknown" 
# and note the limitation in documentation.
```

---

### 7. User Interface Elements

**Avatars and Profile Pictures**
- Problem: Gendered default avatars
- Fix: Gender-neutral defaults or initials

**Before:**
```jsx
{!user.avatar && (
  user.gender === 'M' 
    ? <MaleAvatarIcon /> 
    : <FemaleAvatarIcon />
)}
```

**After:**
```jsx
{!user.avatar && (
  <div className="avatar-placeholder">
    {user.initials || <PersonIcon />}
  </div>
)}
```

---

**Terminology in UI**
- Problem: Gendered language in buttons, labels, messages
- Fix: Gender-neutral alternatives

**Before:**
```
"Ladies and Gentlemen, welcome!"
"Mailing list: Subscribe as Mr./Mrs."
```

**After:**
```
"Welcome, everyone!"
"Mailing list: Subscribe with title (optional)"
```

---

## PART 3: CULTURAL INCLUSIVITY

### 8. Internationalization (i18n)

**Date and Time Formats**
- Problem: Hardcoded US formats
- Fix: Use locale-aware formatting

**Before:**
```javascript
const date = `${month}/${day}/${year}`; // US only
```

**After:**
```javascript
const date = new Intl.DateTimeFormat(userLocale).format(dateObj);
// Adapts to user's locale automatically
```

---

**Currency**
- Problem: Assuming USD or $ symbol
- Fix: Support multiple currencies

**Before:**
```jsx
<span>${price}</span>
```

**After:**
```jsx
<span>
  {new Intl.NumberFormat(userLocale, {
    style: 'currency',
    currency: userCurrency
  }).format(price)}
</span>
```

---

**Name and Address Formats**
- Problem: Assuming all addresses look like US addresses
- Fix: Flexible address fields

**Before:**
```jsx
<input name="state" required placeholder="State" />
<input name="zipCode" required placeholder="ZIP code" />
```

**After:**
```jsx
<input name="region" placeholder="State/Province/Region" />
<input name="postalCode" placeholder="Postal code" />
<select name="country" required>
  {/* Country list */}
</select>
```

---

### 9. Cultural Assumptions

**Holidays and Celebrations**
- Problem: Assuming Christian holidays are universal
- Fix: Use neutral language or support multiple traditions

**Before:**
```javascript
if (month === 12) {
  showBanner("Merry Christmas!");
}
```

**After:**
```javascript
if (month === 12) {
  showBanner("Happy Holidays!"); // Or allow users to set preferences
}
```

---

**Default Examples**
- Problem: Using only Western names/examples
- Fix: Use diverse examples

**Before:**
```python
# Example users in documentation
users = ["John Smith", "Jane Doe", "Bob Johnson"]
```

**After:**
```python
# Diverse example users
users = [
  "Aisha Okonkwo",
  "Chen Wei", 
  "Alex Rivera",
  "Priya Patel"
]
```

---

**Icons and Imagery**
- Problem: Using culturally specific symbols
- Fix: Universal or configurable icons

**Before:**
```jsx
<MailboxIcon /> {/* Shows US-style mailbox */}
```

**After:**
```jsx
<EnvelopeIcon /> {/* Universal envelope symbol */}
```

---

## PART 4: AGE INCLUSIVITY

### 10. Design for All Ages

**Font Sizes**
- Problem: Small, fixed font sizes
- Fix: Responsive, user-adjustable text

**Before:**
```css
body {
  font-size: 12px; /* Fixed small size */
}
```

**After:**
```css
body {
  font-size: 16px; /* Larger base */
  /* Respects user's browser zoom settings */
}
```

---

**Complexity Levels**
- Problem: Assuming technical knowledge
- Fix: Offer beginner-friendly modes

**Before:**
```jsx
<AdvancedSettings /> {/* All settings shown */}
```

**After:**
```jsx
<ToggleMode 
  simple={<BasicSettings />}
  advanced={<AdvancedSettings />}
/>
```

---

## PART 5: ECONOMIC INCLUSIVITY

### 11. Resource Constraints

**Offline Support**
- Problem: Requiring constant internet connection
- Fix: Progressive Web App with offline capabilities

**Before:**
```javascript
// Fails completely without internet
fetch('/api/data').then(...)
```

**After:**
```javascript
// Uses cache when offline
if ('serviceWorker' in navigator) {
  // Implement service worker for offline support
}
```

---

**Data Usage**
- Problem: Large downloads for essential features
- Fix: Optimize assets, offer lite versions

**Before:**
```html
<img src="hero-image-5mb.jpg">
```

**After:**
```html
<picture>
  <source srcset="hero-small.webp" media="(max-width: 768px)">
  <source srcset="hero-medium.webp" media="(max-width: 1200px)">
  <img src="hero-large.webp" loading="lazy" alt="...">
</picture>
```

---

**Performance**
- Problem: Assuming powerful devices
- Fix: Optimize for low-end devices

**Code splitting:**
```javascript
// Load features on demand
const AdvancedEditor = lazy(() => import('./AdvancedEditor'));
```

---

## PART 6: REPRESENTATION IN CODE

### 12. Example Data

**Diverse Names in Tests**
- Problem: Using only Western names in test data
- Fix: Representative diverse names

**Before:**
```javascript
const testUsers = [
  { name: "John Smith", email: "john@example.com" },
  { name: "Jane Doe", email: "jane@example.com" }
];
```

**After:**
```javascript
const testUsers = [
  { name: "Aisha Okonkwo", email: "aisha@example.com" },
  { name: "Santiago García", email: "santiago@example.com" },
  { name: "Yuki Tanaka", email: "yuki@example.com" },
  { name: "Alex Rivera", email: "alex@example.com" }
];
```

---

**Documentation Examples**
- Problem: Always using "he" or male-coded examples
- Fix: Rotate pronouns or use they/them

**Before:**
```markdown
When a user logs in, he will see his dashboard.
```

**After:**
```markdown
When a user logs in, they will see their dashboard.
```

Or:
```markdown
When Alice logs in, she will see her dashboard.
When Bob logs in, he will see his dashboard.
When Sam logs in, they will see their dashboard.
```

---

## PART 7: INCLUSIVE DEFAULTS

### 13. Smart Defaults

**Opt-In vs Opt-Out**
- Problem: Assuming consent (opt-out)
- Fix: Require explicit consent (opt-in)

**Before:**
```jsx
<Checkbox 
  name="marketing" 
  defaultChecked={true}
  label="Send me promotional emails"
/>
```

**After:**
```jsx
<Checkbox 
  name="marketing" 
  defaultChecked={false}
  label="I want to receive promotional emails"
/>
```

---

**Language Detection**
- Problem: Forcing English or detecting incorrectly
- Fix: Ask user's preference, remember it

**Before:**
```javascript
const language = navigator.language; // Auto-detect only
```

**After:**
```javascript
const language = localStorage.getItem('userLanguage') 
  || navigator.language 
  || 'en';

// Show language selector prominently
```

---

## TESTING CHECKLIST

Use this checklist when reviewing software:

### Accessibility
- [ ] Color contrast meets WCAG AA (4.5:1 for text)
- [ ] All interactive elements keyboard accessible
- [ ] Focus indicators visible
- [ ] Alt text for images
- [ ] Captions for video/audio
- [ ] Form labels properly associated
- [ ] ARIA attributes where needed
- [ ] Works with screen readers

### Gender Inclusivity
- [ ] Gender field optional with inclusive options
- [ ] No gendered assumptions in code or UI
- [ ] Pronouns supported where needed
- [ ] Terminology is gender-neutral
- [ ] No gender inference from names/data

### Cultural Inclusivity
- [ ] Date/time/currency formats locale-aware
- [ ] Examples use diverse names
- [ ] No assumptions about holidays or customs
- [ ] Flexible address formats
- [ ] Icons are culturally universal

### Age Inclusivity
- [ ] Text size adequate (16px+ base)
- [ ] Complexity levels offered
- [ ] Clear, jargon-free language

### Economic Inclusivity
- [ ] Works on slower connections
- [ ] Offline support where possible
- [ ] Optimized for low-end devices
- [ ] Minimal data usage

---

## RESOURCES

### Accessibility
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [WebAIM](https://webaim.org/) - Accessibility resources
- [A11y Project](https://www.a11yproject.com/) - Checklist and guides

### Inclusive Design
- [Inclusive Design Principles](https://inclusivedesignprinciples.org/)
- [Microsoft Inclusive Design](https://www.microsoft.com/design/inclusive/)

### Testing Tools
- [axe DevTools](https://www.deque.com/axe/devtools/) - Accessibility testing
- [WAVE](https://wave.webaim.org/) - Web accessibility checker
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) - Audit tool

---

## OUTPUT FORMAT

When reviewing software, provide:

1. **Issues found** - Specific problems with severity (Critical/Major/Minor)
2. **Suggested fixes** - Code examples or specific changes
3. **Rationale** - Why the change improves inclusivity
4. **Priority** - What to fix first based on impact

---

## IMPORTANT NOTES

- **Perfection isn't the goal** - Progress matters more than perfection
- **Prioritize impact** - Focus on changes that help the most people
- **Test with real users** - Especially from underrepresented groups
- **Keep learning** - Inclusivity best practices evolve
- **Document decisions** - Explain why choices were made
