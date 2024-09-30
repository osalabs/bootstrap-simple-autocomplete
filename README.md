# Bootstrap Simple Autocomplete

A super simple and lightweight autocomplete component for Bootstrap 5, designed for easy integration and remote data fetching. Created to replace the legacy [Twitter's Typeahead.js](https://github.com/twitter/typeahead.js) when you just need a remote autocomplete.

## Features

- **Lightweight and easy to use**
- Supports remote data fetching via AJAX
- Fully compatible with Bootstrap 5
- Keyboard navigation (up/down arrows, enter, escape)
- Replicates Typeahead.js UX behavior
- Customizable rendering of dropdown items
- Accessibility supported

## Installation

### Via npm

```bash
npm install bootstrap-simple-autocomplete
```

### Via script tag

Include the script in your HTML file:

```html
<script src="https://unpkg.com/bootstrap-simple-autocomplete/bootstrap-simple-autocomplete.js"></script>
```

## Usage

### Basic Usage

Add the `data-autocomplete` attribute to your input elements with the URL endpoint for fetching suggestions.

```html
<input
  type="text"
  data-autocomplete="https://your-api-endpoint?q="
  class="form-control"
/>
```

Include the script and initialize the autocomplete (auto-initialization occurs if you include the script after the input element):

```html
<script src="bootstrap-simple-autocomplete.js"></script>
```

### ES6 Module Usage
Load .mjs version:
```html
<script src="https://unpkg.com/bootstrap-simple-autocomplete/bootstrap-simple-autocomplete.mjs"></script>
```

```javascript
import {
  BootstrapSimpleAutocomplete,
  initializeAutocomplete,
} from 'bootstrap-simple-autocomplete';

// Auto-initialize all elements with data-autocomplete attribute
initializeAutocomplete();

// Or initialize a specific element
const inputElement = document.querySelector('input[data-autocomplete]');
const autocomplete = new BootstrapSimpleAutocomplete(inputElement);
```

### Custom Fetch Function

You can provide a custom function for fetching data, which allows integration with various data sources or additional processing.

```javascript
const autocomplete = new BootstrapSimpleAutocomplete(inputElement, {
  fetchFunction: function (query) {
    // Custom data fetching logic
    return fetch(`https://your-api-endpoint?q=${encodeURIComponent(query)}`)
      .then((response) => response.json())
      .then((data) => {
        // Process data if needed
        return data;
      });
  },
});
```

### Custom Rendering of Dropdown Items

Customize how each dropdown item is rendered by providing a `renderItem` function.

```javascript
const autocomplete = new BootstrapSimpleAutocomplete(inputElement, {
  renderItem: function (option, query, index) {
    const item = document.createElement('a');
    item.className = 'dropdown-item';
    item.setAttribute('role', 'option');
    item.setAttribute('aria-selected', 'false');
    item.id = `autocomplete-item-${this.id}-${index}`;

    // Example: Highlight the query in the option text
    const regex = new RegExp(`(${query})`, 'gi');
    item.innerHTML = option.replace(regex, '<strong>$1</strong>');

    item.addEventListener('click', () => this.selectOption(option));
    return item;
  },
});
```

### Event Handling

Listen for the `autocomplete.select` event to perform actions when a user selects an option.

```javascript
inputElement.addEventListener('autocomplete.select', (event) => {
  console.log('Selected value:', event.detail.value);
  // Update your model or perform other actions
});
```

### Options

Configure the component using data attributes or constructor options.

#### Data Attributes

- `data-debounce`: Debounce delay in milliseconds (default: `300`)
- `data-minlength`: Minimum input length to trigger autocomplete (default: `1`)

#### Constructor Options

- `debounceDelay`: Number (milliseconds)
- `minQueryLength`: Number
- `fetchFunction`: Function for custom data fetching
- `renderItem`: Function for custom rendering of dropdown items

**Example:**

```javascript
const autocomplete = new BootstrapSimpleAutocomplete(inputElement, {
  debounceDelay: 200,
  minQueryLength: 2,
});
```

### Accessibility

The component includes ARIA attributes for better accessibility:

- `aria-autocomplete="list"`
- `aria-controls`
- `aria-activedescendant`

## License

This project is licensed under the [MIT License](LICENSE).

