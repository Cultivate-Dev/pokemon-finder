# Pokemon Finder - Project Requirements Document

## 1. Project Overview

**Project Name:** Simple Pokemon Finder
**Target Users:** Beginner web developers (high school level)
**Technology Stack:** HTML, CSS, JavaScript (vanilla - no frameworks)
**Data Source:** PokeAPI (https://pokeapi.co/api/v2/)
**Timeline:** 2-3 weeks (casual pace, ~2-4 hours per week)

**Project Goal:**
Build a simple, single-page web application that allows users to search for Pokemon by name and view their basic information including stats, types, and appearance.

---

## 2. Functional Requirements

### FR-1: Search Functionality
- **FR-1.1:** User can enter Pokemon name in a text input field
- **FR-1.2:** User can submit search by clicking "Search" button
- **FR-1.3:** User can submit search by pressing Enter key
- **FR-1.4:** Search is case-insensitive (accepts "PIKACHU", "pikachu", "Pikachu")
- **FR-1.5:** Search trims whitespace from input

### FR-2: Display Pokemon Information
- **FR-2.1:** Display Pokemon sprite/image
- **FR-2.2:** Display Pokemon name (capitalized)
- **FR-2.3:** Display Pokemon type(s) (e.g., "Electric", "Fire/Flying")
- **FR-2.4:** Display core stats:
  - HP
  - Attack
  - Defense
  - Speed
- **FR-2.5:** Display physical characteristics:
  - Height (in meters)
  - Weight (in kilograms)

### FR-3: Error Handling
- **FR-3.1:** Display error message if search field is empty
- **FR-3.2:** Display error message if Pokemon not found
- **FR-3.3:** Provide example Pokemon names in error message
- **FR-3.4:** Clear previous error messages on new search

### FR-4: User Interface Behavior
- **FR-4.1:** Pokemon info hidden until successful search
- **FR-4.2:** Previous Pokemon info replaced with new search results
- **FR-4.3:** Search input remains populated after search

---

## 3. Non-Functional Requirements

### NFR-1: Performance
- Page should load in under 2 seconds
- API calls should complete within 3 seconds
- No page refresh required between searches

### NFR-2: Usability
- Interface should be intuitive for first-time users
- Error messages should be clear and helpful
- Text should be readable (minimum 14px font size)

### NFR-3: Compatibility
- Works in modern browsers (Chrome, Firefox, Safari, Edge)
- Responsive on desktop screens (mobile optional for v1)
- No external dependencies required

### NFR-4: Code Quality
- Code should have clear comments
- Functions should have single responsibilities
- Variable names should be descriptive

---

## 4. User Stories

**As a user, I want to...**

1. **Search for Pokemon by name** so I can learn about my favorite Pokemon
   - Acceptance: Enter "pikachu" → see Pikachu's info

2. **See what a Pokemon looks like** so I can recognize it
   - Acceptance: Image displays clearly and centered

3. **Know a Pokemon's type** so I understand its strengths
   - Acceptance: Types displayed (e.g., "Electric")

4. **View Pokemon stats** so I can compare Pokemon strength
   - Acceptance: HP, Attack, Defense, Speed shown as numbers

5. **Get helpful feedback** when I make a mistake
   - Acceptance: Clear error message with suggestions

6. **Quickly try different Pokemon** without page reload
   - Acceptance: Can search multiple Pokemon in succession

---

## 5. Technical Requirements

### TR-1: API Integration
- **Endpoint:** `https://pokeapi.co/api/v2/pokemon/{name}`
- **Method:** GET
- **Response Format:** JSON
- **No Authentication Required**

### TR-2: Key Data Points to Extract
```javascript
{
  name: string,
  sprites: {
    front_default: string (image URL)
  },
  types: [
    {
      type: {
        name: string
      }
    }
  ],
  stats: [
    {
      stat: { name: string },
      base_stat: number
    }
  ],
  height: number (decimeters),
  weight: number (hectograms)
}
```

### TR-3: Browser APIs Used
- DOM Manipulation: `document.getElementById()`
- Event Listeners: `addEventListener()`
- HTTP Requests: `fetch()`
- Promise Handling: `.then()`, `.catch()`

---

## 6. Wireframes

### Wireframe 1: Initial State (Before Search)

```
┌─────────────────────────────────────────┐
│                                         │
│         🔍 Pokemon Finder               │
│                                         │
│  ┌──────────────────┐  ┌──────────┐   │
│  │ Enter Pokemon... │  │  Search  │   │
│  └──────────────────┘  └──────────┘   │
│                                         │
│                                         │
│      (Pokemon info hidden)              │
│                                         │
│                                         │
└─────────────────────────────────────────┘
```

### Wireframe 2: After Successful Search

```
┌─────────────────────────────────────────┐
│                                         │
│         🔍 Pokemon Finder               │
│                                         │
│  ┌──────────────────┐  ┌──────────┐   │
│  │ pikachu          │  │  Search  │   │
│  └──────────────────┘  └──────────┘   │
│                                         │
│           ┌─────────────┐              │
│           │             │              │
│           │   [IMAGE]   │              │
│           │  Pikachu    │              │
│           │             │              │
│           └─────────────┘              │
│                                         │
│            Pikachu                      │
│         Type: electric                  │
│                                         │
│         ┌──────────────────┐           │
│         │ HP:        35     │           │
│         │ Attack:    55     │           │
│         │ Defense:   40     │           │
│         │ Speed:     90     │           │
│         │ Height:    0.4 m  │           │
│         │ Weight:    6.0 kg │           │
│         └──────────────────┘           │
│                                         │
└─────────────────────────────────────────┘
```

### Wireframe 3: Error State

```
┌─────────────────────────────────────────┐
│                                         │
│         🔍 Pokemon Finder               │
│                                         │
│  ┌──────────────────┐  ┌──────────┐   │
│  │ asdfgh           │  │  Search  │   │
│  └──────────────────┘  └──────────┘   │
│                                         │
│  ┌───────────────────────────────────┐ │
│  │ ⚠️ Pokemon not found!              │ │
│  │ Try: pikachu, charizard, bulbasaur│ │
│  └───────────────────────────────────┘ │
│                                         │
│      (Pokemon info hidden)              │
│                                         │
└─────────────────────────────────────────┘
```

### Wireframe 4: Component Breakdown

```
┌────────────────────────────────────────────┐
│  CONTAINER (white box, centered)           │
│  ┌──────────────────────────────────────┐  │
│  │ HEADER                               │  │
│  │   • Title (H1)                       │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  ┌──────────────────────────────────────┐  │
│  │ SEARCH SECTION                       │  │
│  │   • Text Input (60% width)           │  │
│  │   • Search Button (inline)           │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  ┌──────────────────────────────────────┐  │
│  │ ERROR MESSAGE (conditional)          │  │
│  │   • Red text, bordered box           │  │
│  │   • Hidden by default                │  │
│  └──────────────────────────────────────┘  │
│                                            │
│  ┌──────────────────────────────────────┐  │
│  │ POKEMON INFO (conditional)           │  │
│  │   ┌────────────────────────────────┐ │  │
│  │   │ IMAGE SECTION                  │ │  │
│  │   │  • 150x150px sprite            │ │  │
│  │   └────────────────────────────────┘ │  │
│  │   ┌────────────────────────────────┐ │  │
│  │   │ NAME SECTION                   │ │  │
│  │   │  • Large, bold, capitalized    │ │  │
│  │   └────────────────────────────────┘ │  │
│  │   ┌────────────────────────────────┐ │  │
│  │   │ TYPE SECTION                   │ │  │
│  │   │  • "Type: [types]"             │ │  │
│  │   └────────────────────────────────┘ │  │
│  │   ┌────────────────────────────────┐ │  │
│  │   │ STATS SECTION                  │ │  │
│  │   │  • Left-aligned list           │ │  │
│  │   │  • Label + Value pairs         │ │  │
│  │   │  • 6 rows total                │ │  │
│  │   └────────────────────────────────┘ │  │
│  │   • Hidden by default              │  │
│  └──────────────────────────────────────┘  │
└────────────────────────────────────────────┘
```

---

## 7. Project Phases & Milestones

### Phase 1: Setup & Basic Structure (Week 1, Days 1-2)
**Duration:** 2-3 hours
**Goal:** Create HTML structure and basic styling

**Tasks:**
- [ ] Create `pokemon-finder.html` file
- [ ] Write HTML structure (container, title, input, button)
- [ ] Add basic CSS styling (colors, fonts, layout)
- [ ] Test file opens in browser
- [ ] Make it look presentable

**Deliverable:** Static webpage with search box (no functionality)

**Success Criteria:**
- ✓ Page displays correctly in browser
- ✓ Input and button are visible
- ✓ Layout is centered and clean

---

### Phase 2: Basic JavaScript & API Connection (Week 1, Days 3-4)
**Duration:** 3-4 hours
**Goal:** Connect to PokeAPI and console.log results

**Tasks:**
- [ ] Write `searchPokemon()` function
- [ ] Get input value from text field
- [ ] Build API URL
- [ ] Make `fetch()` call to PokeAPI
- [ ] Log response to console (F12 Developer Tools)
- [ ] Test with multiple Pokemon names

**Deliverable:** Search that logs data to console

**Success Criteria:**
- ✓ Can search for "pikachu" and see data in console
- ✓ Understand the JSON structure returned
- ✓ No errors in console

**Learning Checkpoint:**
- Understand: How `fetch()` works
- Understand: What promises are
- Understand: How to read JSON data

---

### Phase 3: Display Pokemon Information (Week 2, Days 1-2)
**Duration:** 3-4 hours
**Goal:** Show Pokemon data on the page

**Tasks:**
- [ ] Write `displayPokemon()` function
- [ ] Create HTML elements for Pokemon info section
- [ ] Extract name from API response
- [ ] Extract image URL and set `src` attribute
- [ ] Extract types and display as text
- [ ] Show/hide Pokemon info section

**Deliverable:** Pokemon name, image, and type display on page

**Success Criteria:**
- ✓ Pikachu's image appears
- ✓ Name shows as "pikachu"
- ✓ Type shows as "electric"

---

### Phase 4: Display Stats (Week 2, Days 3-4)
**Duration:** 2-3 hours
**Goal:** Add all stats to display

**Tasks:**
- [ ] Loop through `pokemon.stats` array
- [ ] Extract HP, Attack, Defense, Speed
- [ ] Display stats in stat section
- [ ] Convert height (decimeters → meters)
- [ ] Convert weight (hectograms → kilograms)
- [ ] Display height and weight

**Deliverable:** Complete stat display

**Success Criteria:**
- ✓ All 6 stat fields populated
- ✓ Numbers are correct
- ✓ Units are displayed (m, kg)

---

### Phase 5: Error Handling (Week 3, Days 1-2)
**Duration:** 2 hours
**Goal:** Handle errors gracefully

**Tasks:**
- [ ] Check if input is empty
- [ ] Show error message for empty input
- [ ] Handle Pokemon not found (404 error)
- [ ] Create `showError()` function
- [ ] Create `hideError()` function
- [ ] Add helpful suggestions to error message

**Deliverable:** Robust error handling

**Success Criteria:**
- ✓ Empty search shows error
- ✓ Invalid Pokemon name shows error
- ✓ Error clears on new search
- ✓ Error message is helpful

---

### Phase 6: Polish & Enhancements (Week 3, Days 3-4)
**Duration:** 2-3 hours
**Goal:** Improve user experience

**Tasks:**
- [ ] Add Enter key support
- [ ] Style error messages (color, border)
- [ ] Improve spacing and padding
- [ ] Test with many Pokemon
- [ ] Fix any bugs
- [ ] Add code comments
- [ ] Clean up code

**Deliverable:** Polished, complete application

**Success Criteria:**
- ✓ Press Enter to search works
- ✓ UI looks clean and professional
- ✓ Code is well-commented
- ✓ No console errors

---

## 8. Project Roadmap Timeline

### Week 1: Foundation
```
Day 1-2: HTML & CSS Setup         ████░░ 40% complete
Day 3-4: JavaScript & API         ██░░░░ 20% complete
                                  ─────────────────────
Week 1 Total:                     ███░░░ 60% complete
```

### Week 2: Core Functionality
```
Day 1-2: Display Pokemon Info     ██░░░░ 20% complete
Day 3-4: Display Stats            ██░░░░ 20% complete
                                  ─────────────────────
Week 2 Total:                     ████░░ 40% complete
```

### Week 3: Polish
```
Day 1-2: Error Handling           ██░░░░ 15% complete
Day 3-4: Polish & Testing         ██░░░░ 15% complete
                                  ─────────────────────
Week 3 Total:                     ████░░ 30% complete
```

**Overall Project Completion: 100% in 3 weeks**

---

## 9. Testing Checklist

### Functional Testing
- [ ] Search for "pikachu" - displays correctly
- [ ] Search for "charizard" - displays correctly
- [ ] Search for "25" (Pokemon ID) - displays Pikachu
- [ ] Search for "BULBASAUR" (caps) - works correctly
- [ ] Search for " eevee " (with spaces) - works correctly
- [ ] Search for "asdfgh" (invalid) - shows error
- [ ] Leave search empty and click Search - shows error
- [ ] Press Enter key - triggers search
- [ ] Search multiple Pokemon in a row - updates correctly
- [ ] Check all stats are correct (compare to Google)

### Browser Testing
- [ ] Works in Chrome
- [ ] Works in Firefox
- [ ] Works in Safari
- [ ] Works in Edge

### Code Quality
- [ ] All functions have comments
- [ ] Variable names are descriptive
- [ ] No console errors
- [ ] Code is properly indented

---

## 10. Optional Enhancements (Future Versions)

### Version 1.1 (Add After Completing Core)
- [ ] Random Pokemon button
- [ ] Show Pokemon abilities
- [ ] Add Special Attack and Special Defense stats
- [ ] Show Pokemon description/flavor text

### Version 1.2
- [ ] Save favorite Pokemon (localStorage)
- [ ] Show Pokemon evolution chain
- [ ] Add Pokemon moves/attacks
- [ ] Compare two Pokemon side-by-side

### Version 2.0
- [ ] Browse all Pokemon in a grid
- [ ] Filter by type
- [ ] Filter by generation
- [ ] Team builder (6 Pokemon max)

---

## 11. Learning Objectives

By completing this project, you will learn:

### HTML Skills
- ✓ Semantic HTML structure
- ✓ Form inputs and buttons
- ✓ Image elements
- ✓ Div containers and layout

### CSS Skills
- ✓ Styling text (fonts, colors, sizes)
- ✓ Box model (padding, margin, border)
- ✓ Layout (centering, spacing)
- ✓ Pseudo-classes (hover effects)
- ✓ Responsive units

### JavaScript Skills
- ✓ Variables and data types
- ✓ Functions
- ✓ Conditional statements (if/else)
- ✓ Loops (for loops)
- ✓ DOM manipulation
- ✓ Event listeners
- ✓ Fetch API and promises
- ✓ JSON parsing
- ✓ Error handling

### Software Development Skills
- ✓ Project planning
- ✓ Breaking down large tasks
- ✓ Testing and debugging
- ✓ Reading API documentation
- ✓ Problem solving

---

## 12. Resources & References

### Documentation
- PokeAPI Docs: https://pokeapi.co/docs/v2
- MDN Web Docs: https://developer.mozilla.org/
- Fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

### Helpful Pokemon for Testing
| Pokemon | ID | Types | Notes |
|---------|-----|-------|-------|
| pikachu | 25 | Electric | Great starter |
| charizard | 6 | Fire/Flying | Dual type |
| bulbasaur | 1 | Grass/Poison | First Pokemon |
| mewtwo | 150 | Psychic | Legendary |
| eevee | 133 | Normal | Popular |
| dragonite | 149 | Dragon/Flying | Pseudo-legendary |

### Common Pokemon Names to Try
- Single type: pikachu, charmander, squirtle, rattata
- Dual type: charizard, butterfree, pidgeot, gyarados
- Legendary: mewtwo, articuno, zapdos, moltres

---

## 13. Success Metrics

### Project Completion Metrics
- ✓ All 6 phases completed
- ✓ All functional requirements met
- ✓ All test cases pass
- ✓ Code is commented and clean

### Learning Metrics
- ✓ Can explain how fetch() works
- ✓ Can explain what JSON is
- ✓ Can explain DOM manipulation
- ✓ Can debug using browser console
- ✓ Can read API documentation

### Confidence Metrics
- ✓ Feel comfortable searching for Pokemon
- ✓ Can modify code to add new features
- ✓ Can fix bugs independently
- ✓ Proud to show project to others

---

## 14. Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| API goes down | Low | High | Use cached example in comments |
| Don't understand promises | Medium | High | Read MDN guide, watch videos |
| Typos in Pokemon names | High | Low | Show suggestions in errors |
| JSON structure confusing | Medium | Medium | Console.log everything first |
| Lose motivation | Medium | High | Make small wins each session |

---

## Appendix: Code Structure Overview

```
pokemon-finder.html
├── <!DOCTYPE html>
├── <head>
│   ├── Meta tags
│   └── <style> CSS
│       ├── Body styling
│       ├── Container styling
│       ├── Input/Button styling
│       ├── Pokemon info styling
│       └── Error styling
├── <body>
│   └── <div class="container">
│       ├── <h1> Title
│       ├── Search section
│       │   ├── <input> Search field
│       │   └── <button> Search button
│       ├── <div> Error message (hidden)
│       └── <div> Pokemon info (hidden)
│           ├── <img> Pokemon image
│           ├── <div> Pokemon name
│           ├── <div> Pokemon types
│           └── <div> Stats section
│               ├── HP
│               ├── Attack
│               ├── Defense
│               ├── Speed
│               ├── Height
│               └── Weight
└── <script>
    ├── searchPokemon()
    ├── displayPokemon()
    ├── showError()
    ├── hideError()
    └── Event listeners
```

---

**Document Version:** 1.0
**Last Updated:** November 11, 2025
**Author:** Project Team
**Status:** Ready for Development
