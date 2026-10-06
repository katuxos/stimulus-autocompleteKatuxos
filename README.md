# stimulus-autocompleteKatuxos

Lightweight Stimulus controller for local autocomplete and entity selection using a preloaded JSON dataset.

Unlike AJAX-based autocompletes, this controller performs all searches directly in the browser. The dataset is provided once by the backend and no additional server requests are made while the user types.

Fully compatible with Symfony, Turbo, Tailwind, and any Stimulus setup. No dependencies — just clean, modern JavaScript.

---

## Features

- Local search over a preloaded JSON dataset
- Debounced search (250ms)
- Entity selection
- Custom event dispatching
- Click outside to close
- Multiple instances supported
- Turbo compatible
- No AJAX
- No dependencies

---

## Expected JSON Structure

```json
[
    {
        "id": 1,
        "nombre": "John Doe"
    },
    {
        "id": 2,
        "nombre": "Jane Doe"
    }
]
```

The component performs searches against the `nombre` property.

---

## Installation

Copy the controller into your Stimulus controllers directory.

```javascript
import AutocompleteKatuxosController from "./autocompletekatuxos_controller";

application.register(
    "autocompletekatuxos",
    AutocompleteKatuxosController
);
```

---

## Basic Usage

```html
<div
    data-controller="autocompletekatuxos"
    data-autocompletekatuxos-min-length-value="3">

    <input
        type="hidden"
        data-autocompletekatuxos-target="list"
        value="{{ namesData|json_encode|e('html_attr') }}">

    <input
        type="text"
        data-action="input->autocompletekatuxos#buscar"
        data-autocompletekatuxos-target="input">

    <div
        data-autocompletekatuxos-target="results">
    </div>

</div>
```

---

## Listening for Selection Events

```html
<div
    data-controller="autocompletekatuxos items"
    data-action="autocompletekatuxos:selected->items#applySelection">
```

```javascript
applySelection(event) {
    const { id, nombre, item } = event.detail;

    console.log(id);
    console.log(nombre);
}
```

---

## When to Use It

Perfect for small and medium datasets already available in the page:

- Customers
- Suppliers
- Products
- Categories
- Contacts
- Internal entity selectors

---

## Why No AJAX?

This controller was intentionally designed for scenarios where the data is already available on the page.

For many business applications, loading a few dozen or even a few hundred records once is simpler and more efficient than performing a server request on every keystroke.

If you need server-side searching, pagination, or very large datasets, consider an AJAX-based solution instead.

--- 

## Quick access 
You can also grab the controller directly from this Gist: 

 **https://gist.github.com/katuxos/f43bff8b10f0d418fc079a6cbd338e69.js**

---

## License

MIT
