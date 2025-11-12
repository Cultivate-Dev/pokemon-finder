# Pokemon Finder - Project Guide

## Overview

Build a single-page web application that fetches Pokemon data from an API and displays it to users. This project teaches core web development concepts through practical implementation.

**What you'll build:**

- A search interface that accepts Pokemon names
- A display that shows Pokemon sprites, types, and statistics
- Error handling for invalid inputs

**Time estimate:** 2-3 weeks at 2-4 hours per week  
**Prerequisites:** Basic understanding of HTML, CSS, and JavaScript syntax  
**Tech stack:** HTML5, CSS3, Vanilla JavaScript, PokeAPI

---

## Learning Objectives

Complete this project to gain hands-on experience with:

### Frontend Development

- Structure semantic HTML documents
- Style interfaces with CSS
- Manipulate the DOM with JavaScript
- Handle user input and events

### API Integration

- Make HTTP requests with the Fetch API
- Parse JSON responses
- Handle asynchronous operations with Promises
- Manage API errors gracefully

### Software Engineering Practices

- Break down complex tasks into manageable steps
- Test functionality across different scenarios
- Debug using browser developer tools
- Write maintainable, commented code

---

## Development Roadmap

### Week 1: Build the Interface

**Objective:** Create the HTML structure and CSS styling for your application.

**Tasks:**

1. Create `pokemon-finder.html` in your project directory
2. Add the HTML structure:
   - A heading that displays "Pokemon Finder"
   - A text input field for Pokemon names
   - A search button
   - A container for Pokemon information (hidden initially)
3. Style your interface with CSS:
   - Center the container on the page
   - Style the input field and button
   - Define styles for Pokemon information display
   - Add a `.hidden` class to hide/show elements

**Deliverable:** A styled webpage with a search interface (no functionality yet)

**Validation:**

- Open the file in your browser
- Verify the search box and button display correctly
- Confirm the layout matches your design intention

**Time estimate:** 2-3 hours

---

### Week 2: Implement Core Functionality

#### Part 1: Connect to the API

**Objective:** Fetch data from PokeAPI and display basic information.

**Tasks:**

1. Write the `searchPokemon()` function:

   ```javascript
   function searchPokemon() {
       // Get the input value
       // Validate the input
       // Build the API URL
       // Make the fetch request
       // Handle the response
   }
   ```

2. Attach the function to your search button:

   ```javascript
   button.addEventListener('click', searchPokemon);
   ```

3. Build the API request:

   ```javascript
   const apiUrl = `https://pokeapi.co/api/v2/pokemon/${pokemonName}`;
   fetch(apiUrl)
       .then(response => response.json())
       .then(data => console.log(data));
   ```

4. Open your browser's developer console (F12) to view the response data
5. Examine the JSON structure to understand the data format

**Tasks:**

1. Create the `displayPokemon(pokemon)` function
2. Extract and display:
   - Pokemon sprite (`pokemon.sprites.front_default`)
   - Pokemon name (`pokemon.name`)
   - Pokemon types (`pokemon.types`)
3. Show the Pokemon information container
4. Test with multiple Pokemon names

**Deliverable:** A functional search that displays Pokemon name, image, and type

**Validation:**

- Search for "pikachu" and verify the image displays
- Confirm the name appears as "pikachu"
- Check that "Type: electric" displays correctly
- Open the console and verify no errors appear

**Time estimate:** 3-4 hours

#### Part 2: Display Statistics

**Objective:** Extract and display Pokemon statistics from the API response.

**Tasks:**
1. Locate statistics in the API response (`pokemon.stats` array)

2. Loop through the stats array to find:
   - HP (`stat.name === 'hp'`)
   - Attack (`stat.name === 'attack'`)
   - Defense (`stat.name === 'defense'`)
   - Speed (`stat.name === 'speed'`)
3. Update the corresponding HTML elements with stat values
4. Convert height from decimeters to feet and inches:

   ```javascript
   const heightInFeet = pokemon.height * 0.328084;
   const feet = Math.floor(heightInFeet);
   const inches = Math.round((heightInFeet - feet) * 12);
   ```

5. Convert weight from hectograms to pounds: `weight * 0.220462`
6. Display height and weight with proper units

**Deliverable:** Complete stat display with all six values

**Validation:**

- Search for "pikachu"
- Verify HP displays as 35
- Verify Attack displays as 55
- Confirm height shows as "1' 4\"" (1 foot 4 inches)
- Confirm weight shows as "13.2 lbs"

**Time estimate:** 2-3 hours

---

### Week 3: Add Error Handling and Polish

**Objective:** Handle edge cases and improve user experience.

**Tasks:**
1. Validate user input before making API requests:

   ```javascript
   if (pokemonName === '') {
       showError('Enter a Pokemon name to search.');
       return;
   }
   ```

2. Handle API errors (Pokemon not found):

   ```javascript
   .catch(error => {
       showError('Pokemon not found. Try pikachu, charizard, or bulbasaur.');
   });
   ```

3. Create helper functions:

   ```javascript
   function showError(message) {
       // Display error message
       // Hide Pokemon info
   }
   
   function hideError() {
       // Hide error message
   }
   ```

4. Add keyboard support:

   ```javascript
   searchInput.addEventListener('keypress', (event) => {
       if (event.key === 'Enter') {
           searchPokemon();
       }
   });
   ```

5. Clean up your code:
   - Add comments explaining each function
   - Use descriptive variable names
   - Remove console.log statements (or keep them for debugging)
   - Ensure consistent indentation

**Deliverable:** A polished application with comprehensive error handling

**Validation:**

- Click search with an empty input field (should show error)
- Search for "asdfgh" (should show error with suggestions)
- Search for a valid Pokemon (should clear any previous errors)
- Press Enter in the search field (should trigger search)
- Search for multiple Pokemon in succession (should update correctly)

**Time estimate:** 3-4 hours

---

## Feature Checklist

### Core Features

- [ ] Search accepts Pokemon names as input
- [ ] Search button triggers the API request
- [ ] Enter key triggers the search
- [ ] Pokemon sprite displays correctly
- [ ] Pokemon name displays in capitalized format
- [ ] Pokemon type(s) display (handles single and dual types)
- [ ] HP stat displays
- [ ] Attack stat displays
- [ ] Defense stat displays
- [ ] Speed stat displays
- [ ] Height displays in feet and inches
- [ ] Weight displays in pounds

### Error Handling

- [ ] Empty input displays error message
- [ ] Invalid Pokemon name displays error message
- [ ] Error messages include helpful suggestions
- [ ] Errors clear on subsequent searches
- [ ] Previous Pokemon info clears when showing errors

### User Experience

- [ ] Search is case-insensitive
- [ ] Search trims whitespace from input
- [ ] Pokemon info replaces previous results
- [ ] No page refresh required between searches
- [ ] Interface remains responsive during API calls

---

## Testing Guide

### Functional Tests

Run these tests to verify your application works correctly:

1. **Standard search:**
   - Enter "pikachu" and click Search
   - Verify all information displays correctly
   - Compare stats with [official Pokemon data](https://www.pokemon.com/us/pokedex/pikachu)

2. **Case insensitivity:**
   - Search "CHARIZARD" (all uppercase)
   - Verify the search succeeds
   - Search "BuLbAsAuR" (mixed case)
   - Verify the search succeeds

3. **Whitespace handling:**
   - Search " eevee " (with leading/trailing spaces)
   - Verify the search succeeds

4. **Empty input:**
   - Leave the search field empty
   - Click Search
   - Verify an error message appears

5. **Invalid Pokemon:**
   - Search "asdfgh"
   - Verify an error message appears with suggestions

6. **Enter key:**
   - Type "squirtle" in the search field
   - Press Enter (don't click the button)
   - Verify the search executes

7. **Sequential searches:**
   - Search "pikachu"
   - Note the displayed information
   - Search "charizard"
   - Verify Charizard's info replaces Pikachu's info completely

8. **Dual-type Pokemon:**
   - Search "charizard"
   - Verify both types display: "Type: fire, flying"

### Browser Compatibility Tests

Test your application in multiple browsers:

- [ ] Chrome/Chromium
- [ ] Firefox
- [ ] Safari (if available)
- [ ] Edge

### Recommended Test Pokemon

**Single-type Pokemon:**

- pikachu (Electric)
- charmander (Fire)
- squirtle (Water)
- bulbasaur (Grass)

**Dual-type Pokemon:**

- charizard (Fire/Flying)
- butterfree (Bug/Flying)
- gyarados (Water/Flying)

**Edge cases:**

- mewtwo (Legendary Pokemon)
- 25 (Pokemon ID instead of name - should work)
- mr-mime (name with hyphen)

---

## API Reference

### Endpoint

```json
GET https://pokeapi.co/api/v2/pokemon/{name-or-id}
```

**Parameters:**
- `name-or-id` (string|number): Pokemon name (lowercase) or Pokedex number

**Example request:**

```javascript
fetch('https://pokeapi.co/api/v2/pokemon/pikachu')
    .then(response => response.json())
    .then(data => console.log(data));
```

### Response Structure

The API returns a JSON object with the following relevant fields:

```javascript
{
    "name": "pikachu",                    // String: Pokemon name
    "height": 4,                          // Number: Height in decimeters
    "weight": 60,                         // Number: Weight in hectograms
    "sprites": {
        "front_default": "https://..."    // String: Image URL
    },
    "types": [                            // Array: Pokemon types
        {
            "type": {
                "name": "electric"        // String: Type name
            }
        }
    ],
    "stats": [                            // Array: Pokemon statistics
        {
            "base_stat": 35,              // Number: Stat value
            "stat": {
                "name": "hp"              // String: Stat name
            }
        }
        // ... more stats
    ]
}
```

### Data Conversions

**Height:** The API returns height in decimeters. Convert to feet and inches:
```javascript
const heightInFeet = pokemon.height * 0.328084;
const feet = Math.floor(heightInFeet);
const inches = Math.round((heightInFeet - feet) * 12);
// Display as: feet + "' " + inches + "\""
// Example: "1' 4"" for Pikachu
```

**Weight:** The API returns weight in hectograms. Convert to pounds:
```javascript
const weightInPounds = pokemon.weight * 0.220462;
// Round to one decimal place
const displayWeight = Math.round(weightInPounds * 10) / 10;
// Display as: displayWeight + " lbs"
// Example: "13.2 lbs" for Pikachu
```

**Stat names:** Match these stat names from the API:
- `"hp"` → HP
- `"attack"` → Attack
- `"defense"` → Defense
- `"speed"` → Speed

---

## Troubleshooting

### Common Issues

**Problem:** "Pokemon not found" error for valid Pokemon  
**Solution:** Check your spelling. Pokemon names must be lowercase. Try "charizard" not "Charizard".

**Problem:** Image doesn't display  
**Solution:** Verify you're accessing `pokemon.sprites.front_default` correctly. Check the console for errors.

**Problem:** Stats show as "undefined"  
**Solution:** Loop through the `pokemon.stats` array and match the `stat.name` property. Log the stats array to inspect its structure.

**Problem:** Nothing happens when clicking Search  
**Solution:** Check that your button has an `onclick` attribute or event listener attached. Open the console to check for JavaScript errors.

**Problem:** API request fails  
**Solution:** Open the Network tab in developer tools (F12). Verify the request URL is formatted correctly: `https://pokeapi.co/api/v2/pokemon/pikachu`

### Debugging Tips

1. **Use console.log() liberally:**
   ```javascript
   console.log('Pokemon name:', pokemonName);
   console.log('API response:', pokemon);
   console.log('Stats array:', pokemon.stats);
   ```

2. **Check the browser console (F12):**
   - Look for red error messages
   - Expand objects to inspect their structure
   - Verify your API requests in the Network tab

3. **Test incrementally:**
   - Don't write all the code at once
   - Test each function as you write it
   - Verify each feature works before moving to the next

4. **Compare with the wireframe:**
   - Reference the provided `pokemon-finder_final_wireframe` file
   - Compare your code structure to the working example
   - Look for differences in syntax or logic

---

## Enhancement Ideas

After completing the core project, consider adding these features:

### Beginner Enhancements

- Add a "Random Pokemon" button that fetches a random Pokemon (1-151)
- Display Pokemon abilities from the API response
- Add Special Attack and Special Defense stats
- Style different Pokemon types with different colors

### Intermediate Enhancements

- Save favorite Pokemon to localStorage
- Display Pokemon evolution chain
- Add a comparison feature (compare two Pokemon side-by-side)
- Implement autocomplete for Pokemon names

### Advanced Enhancements

- Create a grid view showing multiple Pokemon
- Add filters (by type, generation, stats)
- Build a team builder (select up to 6 Pokemon)
- Add animations when Pokemon appear
- Implement pagination for browsing all Pokemon

---

## Best Practices

### Code Organization

**Use descriptive function names:**

```javascript
// Good
function searchPokemon() { }
function displayPokemon(data) { }

// Avoid
function doThing() { }
function x(y) { }
```

**Add comments for complex logic:**
```javascript
// Convert height from decimeters to meters
const heightInMeters = pokemon.height / 10;

// Loop through stats array to find and display each stat
for (let i = 0; i < pokemon.stats.length; i++) {
    // ...
}
```

**Keep functions focused:**
Each function should do one thing well. Avoid creating functions that try to do too much.

### Error Handling

Always handle potential errors:
```javascript
fetch(apiUrl)
    .then(response => {
        if (!response.ok) {
            throw new Error('Pokemon not found');
        }
        return response.json();
    })
    .then(data => displayPokemon(data))
    .catch(error => showError(error.message));
```

### User Experience

- Provide immediate feedback for user actions
- Clear previous errors before new searches
- Disable the search button during API requests (optional)
- Add loading indicators for slow connections (optional)

---

## Resources

### Documentation
- [PokeAPI Documentation](https://pokeapi.co/docs/v2) - Complete API reference
- [MDN Web Docs](https://developer.mozilla.org/) - HTML, CSS, and JavaScript documentation
- [MDN Fetch API Guide](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) - Learn about Fetch

### Learning Materials
- [JavaScript Promises Explained](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [Working with JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [DOM Manipulation Guide](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents)

### Tools
- Browser Developer Tools (F12) - Inspect, debug, and test
- [JSONView Browser Extension](https://jsonview.com/) - Format JSON responses
- [Can I Use](https://caniuse.com/) - Check browser compatibility

---

## Project Structure

```text
project-folder/
├── pokemon-finder.html          # Your main HTML file
└── README.md                    # Optional: Document your project
```

**Note:** This project uses inline CSS and JavaScript for simplicity. For larger projects, separate these into individual files:

```text
project-folder/
├── index.html
├── styles.css
└── script.js
```

---

## Completion Criteria

Consider your project complete when:

- [ ] All core features work as specified
- [ ] All tests pass successfully
- [ ] Error handling covers edge cases
- [ ] Code includes clear comments
- [ ] The interface looks clean and professional
- [ ] No errors appear in the browser console
- [ ] You can confidently explain how the code works

---

## Next Steps

After completing this project:

1. **Share your work:**
   - Deploy to GitHub Pages
   - Share with friends and get feedback
   - Add to your portfolio

2. **Extend your learning:**
   - Implement enhancement ideas
   - Try building a similar project with a different API
   - Learn about React or other frameworks

3. **Practice variations:**
   - Build a weather app with the OpenWeather API
   - Create a movie search with the OMDB API
   - Make a recipe finder with the Spoonacular API

---

**Version:** 1.0  
**Last Updated:** November 12, 2025  
**License:** Use this guide freely for learning purposes
