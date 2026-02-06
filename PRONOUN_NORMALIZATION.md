# Pronoun Field Normalization Guide

## The Problem

When implementing pronoun fields in software, there's a fundamental tension:

- **Open text field**: Allows users to enter anything (respects diversity) but leads to inconsistency (variations like "she/her", "She/Her", "she / her", "she-her", "she")
- **Preset dropdown**: Ensures consistency but can never include all possibilities (excludes neopronouns, cultural variations, and evolving language)

## The Solution: Hybrid Approach

Use **free-text input with datalist suggestions** and apply **smart normalization** on the backend.

---

## Part 1: Frontend Implementation

### HTML5 Datalist (Recommended)

```html
<label for="pronouns">Pronouns (optional)</label>
<input 
  type="text" 
  id="pronouns"
  name="pronouns"
  placeholder="e.g., she/her, they/them"
  list="common-pronouns"
  maxlength="50"
  autocomplete="off"
  aria-describedby="pronouns-help"
/>
<datalist id="common-pronouns">
  <option value="she/her">
  <option value="he/him">
  <option value="they/them">
  <option value="she/they">
  <option value="he/they">
  <option value="ze/hir">
  <option value="ze/zir">
  <option value="xe/xem">
  <option value="any pronouns">
  <option value="ask me">
</datalist>
<small id="pronouns-help">
  How would you like to be referred to?
</small>
```

**Why this works:**
- ✅ Shows common options (guides users, reduces typos)
- ✅ Allows free text (respects diversity, includes everything)
- ✅ No forced choice (doesn't exclude anyone)
- ✅ Works progressively (degrades to plain text field in older browsers)
- ✅ Easy to expand suggestions without breaking existing entries

### React/JSX Example

```jsx
function PronounField({ value, onChange, error }) {
  const commonPronouns = [
    'she/her',
    'he/him', 
    'they/them',
    'she/they',
    'he/they',
    'ze/hir',
    'ze/zir',
    'xe/xem',
    'ey/em',
    'fae/faer',
    'any pronouns',
    'ask me'
  ];

  return (
    <div className="form-field">
      <label htmlFor="pronouns">
        Pronouns <span className="optional">(optional)</span>
      </label>
      
      <input
        type="text"
        id="pronouns"
        name="pronouns"
        value={value}
        onChange={onChange}
        placeholder="e.g., she/her, they/them"
        list="common-pronouns"
        maxLength={50}
        autoComplete="off"
        aria-describedby="pronouns-help"
        aria-invalid={error ? 'true' : 'false'}
      />
      
      <datalist id="common-pronouns">
        {commonPronouns.map(pronoun => (
          <option key={pronoun} value={pronoun} />
        ))}
      </datalist>
      
      <small id="pronouns-help" className="help-text">
        Enter your pronouns as you'd like them displayed
      </small>
      
      {error && <span className="error">{error}</span>}
    </div>
  );
}
```

---

## Part 2: Backend Normalization

### Normalization Strategy

**Goal:** Store pronouns as entered, but normalize for display/comparison while respecting user intent.

### JavaScript Normalization Function

```javascript
/**
 * Normalize pronoun strings for consistent storage and comparison
 * Preserves original user input but provides canonical form
 */
function normalizePronoun(input) {
  if (!input || typeof input !== 'string') {
    return { original: '', normalized: '', canonical: null };
  }

  const original = input.trim();
  
  // Lowercase and remove extra whitespace
  const normalized = original
    .toLowerCase()
    .replace(/\s+/g, ' ')  // Multiple spaces to single space
    .replace(/\s*\/\s*/g, '/') // "she / her" → "she/her"
    .replace(/\s*-\s*/g, '/'); // "she-her" → "she/her"
  
  // Map to canonical forms (for matching, not replacing)
  const canonicalMap = {
    'she/her': 'she/her',
    'she/hers': 'she/her',
    'she': 'she/her',
    
    'he/him': 'he/him',
    'he/his': 'he/him',
    'he': 'he/him',
    
    'they/them': 'they/them',
    'they/theirs': 'they/them',
    'they': 'they/them',
    
    'she/they': 'she/they',
    'they/she': 'she/they',
    
    'he/they': 'he/they',
    'they/he': 'he/they',
    
    'ze/hir': 'ze/hir',
    'ze/zir': 'ze/zir',
    'xe/xem': 'xe/xem',
    'ey/em': 'ey/em',
    'fae/faer': 'fae/faer',
    've/ver': 've/ver',
    
    'any': 'any pronouns',
    'any pronouns': 'any pronouns',
    'all pronouns': 'any pronouns',
    
    'ask': 'ask me',
    'ask me': 'ask me'
  };
  
  const canonical = canonicalMap[normalized] || null;
  
  return {
    original,      // What the user typed (display this!)
    normalized,    // Normalized for comparison
    canonical      // Recognized canonical form (null if not in map)
  };
}

// Usage
const result = normalizePronoun("She / Her ");
console.log(result);
// {
//   original: "She / Her",
//   normalized: "she/her",
//   canonical: "she/her"
// }

const custom = normalizePronoun("fæ/fær");
console.log(custom);
// {
//   original: "fæ/fær",
//   normalized: "fæ/fær", 
//   canonical: null  // Not in predefined list, but that's OK!
// }
```

### Python Normalization Function

```python
from typing import Optional, Dict
import re

def normalize_pronoun(input_str: Optional[str]) -> Dict[str, Optional[str]]:
    """
    Normalize pronoun strings for consistent storage and comparison.
    
    Returns dict with:
    - original: What the user entered (always display this)
    - normalized: Lowercased, whitespace normalized
    - canonical: Recognized standard form (None if custom)
    """
    if not input_str or not isinstance(input_str, str):
        return {
            'original': '',
            'normalized': '',
            'canonical': None
        }
    
    original = input_str.strip()
    
    # Normalize spacing and separators
    normalized = original.lower()
    normalized = re.sub(r'\s+', ' ', normalized)  # Multiple spaces → single
    normalized = re.sub(r'\s*/\s*', '/', normalized)  # "she / her" → "she/her"
    normalized = re.sub(r'\s*-\s*', '/', normalized)  # "she-her" → "she/her"
    
    # Canonical mappings
    canonical_map = {
        'she/her': 'she/her',
        'she/hers': 'she/her',
        'she': 'she/her',
        
        'he/him': 'he/him',
        'he/his': 'he/him',
        'he': 'he/him',
        
        'they/them': 'they/them',
        'they/theirs': 'they/them',
        'they': 'they/them',
        
        'she/they': 'she/they',
        'they/she': 'she/they',
        
        'he/they': 'he/they',
        'they/he': 'he/they',
        
        'ze/hir': 'ze/hir',
        'ze/zir': 'ze/zir',
        'xe/xem': 'xe/xem',
        'ey/em': 'ey/em',
        'fae/faer': 'fae/faer',
        've/ver': 've/ver',
        
        'any': 'any pronouns',
        'any pronouns': 'any pronouns',
        'all pronouns': 'any pronouns',
        
        'ask': 'ask me',
        'ask me': 'ask me'
    }
    
    canonical = canonical_map.get(normalized)
    
    return {
        'original': original,
        'normalized': normalized,
        'canonical': canonical
    }

# Example usage
result = normalize_pronoun("She / Her ")
print(result)
# {'original': 'She / Her', 'normalized': 'she/her', 'canonical': 'she/her'}

custom = normalize_pronoun("fæ/fær")
print(custom)
# {'original': 'fæ/fær', 'normalized': 'fæ/fær', 'canonical': None}
```

---

## Part 3: Database Storage

### Recommended Schema

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  
  -- Store original exactly as entered
  pronouns_display VARCHAR(50) NULL,
  
  -- Store normalized version for searching/filtering
  pronouns_normalized VARCHAR(50) NULL,
  
  -- Optional: Store canonical form for analytics
  pronouns_canonical VARCHAR(50) NULL,
  
  -- Timestamp for when pronouns were last updated
  pronouns_updated_at TIMESTAMP NULL,
  
  CONSTRAINT pronouns_length CHECK (
    LENGTH(TRIM(pronouns_display)) <= 50
  )
);

-- Index for searching by normalized form
CREATE INDEX idx_users_pronouns_normalized 
  ON users(pronouns_normalized) 
  WHERE pronouns_normalized IS NOT NULL;
```

**Why three fields?**

1. **`pronouns_display`** - ALWAYS show this to users (respects their exact input)
2. **`pronouns_normalized`** - Use for searching/matching (handles "she/her" vs "She / Her")
3. **`pronouns_canonical`** - Optional for analytics ("how many users use they/them?")

### Validation Rules

```javascript
function validatePronouns(input) {
  if (!input || input.trim() === '') {
    return { valid: true, error: null }; // Optional field
  }
  
  const trimmed = input.trim();
  
  // Length check
  if (trimmed.length > 50) {
    return { 
      valid: false, 
      error: 'Pronouns must be 50 characters or less' 
    };
  }
  
  // Allow almost any characters (support international characters)
  if (!/^[\p{L}\p{N}\p{P}\p{Zs}]+$/u.test(trimmed)) {
    return { 
      valid: false, 
      error: 'Pronouns contain unsupported characters' 
    };
  }
  
  return { valid: true, error: null };
}
```

---

## Part 4: Display and Usage

### Displaying Pronouns

```javascript
// ALWAYS display the original
function displayUserPronouns(user) {
  if (!user.pronouns_display) {
    return null; // User didn't provide pronouns
  }
  
  return user.pronouns_display; // Show exactly what they entered
}

// Example in UI
<span className="user-pronouns">
  {user.name} {user.pronouns_display && `(${user.pronouns_display})`}
</span>
// Output: "Alex (they/them)" or "Sam (ze/hir)" or "Jordan (fae/faer)"
```

### Using Pronouns in Text

```javascript
/**
 * Parse pronouns to extract subject/object forms
 * Handles common patterns, falls back to they/them
 */
function parsePronouns(pronounString) {
  if (!pronounString) {
    return { subject: 'they', object: 'them', possessive: 'their' };
  }
  
  const normalized = pronounString.toLowerCase().trim();
  
  // Handle "pronoun/pronoun" format
  if (normalized.includes('/')) {
    const [subject, object] = normalized.split('/').map(p => p.trim());
    
    // Common mappings
    const possessiveMap = {
      'her': 'her',
      'him': 'his',
      'them': 'their',
      'hir': 'hir',
      'zir': 'zir',
      'xem': 'xyr',
      'em': 'eir',
      'faer': 'faer',
      'ver': 'vis'
    };
    
    return {
      subject: subject,
      object: object,
      possessive: possessiveMap[object] || object
    };
  }
  
  // Handle special cases
  if (normalized.includes('any')) {
    return { subject: 'they', object: 'them', possessive: 'their' };
  }
  
  if (normalized.includes('ask')) {
    return { subject: 'they', object: 'them', possessive: 'their' };
  }
  
  // Default to they/them
  return { subject: 'they', object: 'them', possessive: 'their' };
}

// Usage in generated text
function generateMessage(user, action) {
  const pronouns = parsePronouns(user.pronouns_display);
  return `${user.name} updated ${pronouns.possessive} profile. ` +
         `${pronouns.subject.charAt(0).toUpperCase() + pronouns.subject.slice(1)} ` +
         `${pronouns.subject === 'they' ? 'have' : 'has'} ` +
         `${action}.`;
}

// Examples:
// generateMessage({name: 'Alex', pronouns_display: 'they/them'}, 'logged in')
// → "Alex updated their profile. They have logged in."

// generateMessage({name: 'Sam', pronouns_display: 'ze/hir'}, 'logged in')
// → "Sam updated hir profile. Ze has logged in."
```

---

## Part 5: API Design

### API Request/Response

```javascript
// POST /api/users
{
  "name": "Alex Rivera",
  "pronouns": "they/them"  // Accept free text
}

// Response
{
  "id": "123",
  "name": "Alex Rivera",
  "pronouns": "they/them",  // Return exactly what was provided
  "created_at": "2024-01-15T10:30:00Z"
}

// GET /api/users/123
{
  "id": "123",
  "name": "Alex Rivera",
  "pronouns": "they/them"  // Always return original
}
```

### Search/Filter API

```javascript
// GET /api/users?pronouns=they/them
// Searches using normalized form, returns original

{
  "users": [
    {
      "id": "123",
      "name": "Alex",
      "pronouns": "they/them"  // Original: "they/them"
    },
    {
      "id": "456", 
      "name": "Sam",
      "pronouns": "They / Them"  // Original: "They / Them" (user's formatting preserved)
    }
  ]
}
```

---

## Part 6: Analytics and Reporting

### Aggregating Pronoun Usage

```sql
-- Count by canonical form (for reporting)
SELECT 
  COALESCE(pronouns_canonical, 'other') as pronoun_category,
  COUNT(*) as user_count
FROM users
WHERE pronouns_display IS NOT NULL
GROUP BY pronouns_canonical
ORDER BY user_count DESC;

-- Results:
-- they/them: 1,234
-- she/her: 987
-- he/him: 876
-- she/they: 234
-- any pronouns: 123
-- other: 89  (includes all neopronouns and custom entries)
```

**Important:** 
- Group custom/neopronoun entries as "other" for privacy
- Don't expose individual custom pronouns in analytics
- Only report on canonical forms (common pronouns)

---

## Part 7: Best Practices Summary

### ✅ DO

- **Accept free text** - Use input + datalist, not dropdown
- **Store original** - Display exactly what user entered
- **Normalize for matching** - Handle "she/her" vs "She / Her" as same
- **Allow empty** - Pronouns should be optional
- **Support updates** - Users should be able to change pronouns easily
- **Respect neopronouns** - Don't reject ze/zir, fae/faer, etc.
- **Default to they/them** - When unsure or unavailable

### ❌ DON'T

- **Force selection from dropdown** - Excludes new/uncommon pronouns
- **Reject "invalid" pronouns** - Language evolves, respect users
- **Normalize display** - Show user's exact input, not "corrected" version
- **Expose analytics** - Don't report individual neopronoun usage
- **Make required** - Pronouns are personal, keep optional
- **Infer from name/gender** - Always ask, never assume

---

## Part 8: Migration Strategy

### Adding Pronouns to Existing System

```sql
-- Phase 1: Add fields
ALTER TABLE users 
  ADD COLUMN pronouns_display VARCHAR(50) NULL,
  ADD COLUMN pronouns_normalized VARCHAR(50) NULL,
  ADD COLUMN pronouns_canonical VARCHAR(50) NULL;

-- Phase 2: Update UI to show pronoun field (optional)

-- Phase 3: Create index after users start adding data
CREATE INDEX idx_users_pronouns_normalized 
  ON users(pronouns_normalized) 
  WHERE pronouns_normalized IS NOT NULL;
```

### Prompting Existing Users

```jsx
// Show optional profile completion prompt
{!user.pronouns && showProfileCompletion && (
  <Banner dismissible onDismiss={() => setShowProfileCompletion(false)}>
    <h4>Share your pronouns (optional)</h4>
    <p>
      Help others address you correctly by adding your pronouns to your profile.
    </p>
    <Button onClick={goToProfileSettings}>
      Add pronouns
    </Button>
    <Button variant="text" onClick={() => setShowProfileCompletion(false)}>
      Skip
    </Button>
  </Banner>
)}
```

---

## Conclusion

The hybrid approach solves the pronoun normalization challenge:

1. **Frontend**: Free-text input with datalist suggestions
2. **Backend**: Normalize for comparison, store original for display
3. **Database**: Three fields (display, normalized, canonical)
4. **Display**: Always show user's exact input
5. **Matching**: Use normalized form for searches
6. **Analytics**: Group by canonical, respect privacy

This approach:
- ✅ Respects user autonomy (any pronouns accepted)
- ✅ Reduces errors (common suggestions guide users)
- ✅ Enables matching ("she/her" = "She / Her")
- ✅ Future-proof (new pronouns work without code changes)
- ✅ Privacy-respecting (custom pronouns not exposed in analytics)

**The key insight:** Store what users enter, normalize for comparison, but ALWAYS display the original.
