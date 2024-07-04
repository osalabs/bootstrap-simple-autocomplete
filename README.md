# Bootstrap Simple Autocomplete

A super simple and lightweight autocomplete component for Bootstrap 5, designed for easy integration and remote data fetching.
Created to replace legacy [Twitter's Typeahead.js](https://github.com/twitter/typeahead.js) when you just need remote autocomplete.

## Features

- Lightweight and easy to use
- Supports remote data fetching via AJAX
- Fully compatible with Bootstrap 5
- Keyboard navigation (up/down arrows, enter, escape)

## Installation

### Via npm

```bash
npm install bootstrap-simple-autocomplete
```

### Via script tag

Download the bootstrap-simple-autocomplete.js file and include it in your HTML.

<script src="path_to/bootstrap-simple-autocomplete.js"></script>

## Usage

### HTML Setup

Add the `data-autocomplete` attribute to your input elements with the URL for fetching suggestions.

```html
  <input type="text" data-autocomplete="https://localhost?q=" class="form-control">
  ...
  <script src="path_to/bootstrap-simple-autocomplete.js"></script>
```

When user start typing into the input - user's text will be added to the URL and fetched via GET with `Accept:application/json` header.
Server expect to return json array of strings which are the suggestions to be displayed in the dropdown:
```json
[
  "alpha",
  "bravo",
  "charlie",
  "delta"
]
```

The component then displays these suggestions in a Bootstrap-styled dropdown menu. The user can navigate through the suggestions using the up and down arrow keys, and select a suggestion by pressing the Enter or Tab key. Pressing the Escape key will close the dropdown.

If the user's input matches the beginning of the first suggestion, the suggestion will be pre-filled as muted text underneath the user's text, indicating the suggestion that will be selected if the user presses the Tab key.

The dropdown will be closed if the input is cleared or if a selection is made. In case of an error during the fetch request, an error message will be displayed in the dropdown using the Bootstrap danger class.

This component ensures a smooth and intuitive user experience for providing autocomplete functionality to input fields in Bootstrap 5-based projects.

### JavaScript Module Usage

If you are using ES6 modules, import the class and initialization function:

```javascript
import { BootstrapSimpleAutocomplete, initializeAutocomplete } from 'bootstrap-simple-autocomplete';

// Initialize all inputs with data-autocomplete attribute
initializeAutocomplete();

// Or initialize a specific input manually
const input = document.querySelector('input[data-autocomplete]');
if (input) {
    new BootstrapSimpleAutocomplete(input);
}
```
