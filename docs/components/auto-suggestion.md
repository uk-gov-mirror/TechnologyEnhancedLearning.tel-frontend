---
title: Auto-suggestion
description: An enhanced text input that provides real-time search suggestions and matching results as users type.
layout: layouts/component.njk
tags:
  - component
---

## Summary

Use the auto-suggestion component to display selectable options based on typed input. As users type, it filters and displays matching suggestions directly below the input field, reducing typing effort and preventing spelling errors.

Auto-suggestion is intended for scenarios with known datasets—such as location lookups, course searches, or medical condition finders—where helping users select a standardized value improves data accuracy and speed.

{% example "auto-suggestion/page.njk" %}

This is the simplest variation of the auto-suggest page pattern where suggestions are offered directly as the user types.

## When to use

Use auto-suggestion when users need to find a specific item from a large or complex list.

It is useful when:
- the list of available choices is too long for a standard select element or radio list
- users might not know the exact spelling or precise name of what they are looking for
- standardizing the entered data is important for backend processing
- speeding up input on mobile devices is beneficial

## When not to use

Do not use auto-suggestion as a replacement for simple input controls when choices are limited.

It should not be used:
- when there are fewer than 5–10 options (use radio buttons or a select dropdown instead)
- for free-text inputs where suggestions could restrict or confuse the user
- when users are likely to enter unique or unpredictable text that won't match a fixed list
- during high-speed, minimal-interaction entry where predictive popups distract from completion

## How it works

The auto-suggestion component overlays dynamic matching results directly beneath the text input field as the user types.

The component supports:
- matching query strings against display titles, synonyms, or codes
- keyboard navigation (using Up/Down arrow keys and Enter to select)
- status text announcement for screen readers (e.g., "5 results available")
- an optional conditional reveal panel for user input when an item is not found

On smaller screens, the suggestion list scales to fit the viewport width to maintain touch target sizing.

### Configuration

#### Common properties

- `id` (string, required) - Unique HTML identifier for the input element
- `input_name` (string, required) - Name attribute applied to the input field
- `type` (string, required) - `"page"`, `"radio"` or `"checkbox"` 
- `placeholder` (string) - Input field placeholder text 
- `search_text` (string) - Load component with pre-determined search string
- `menu_items` (array) - Array of suggestion items rendered by the component

#### Suggestion menu item properties (`menu_items`)

- `text` (string, required) - Item text
- `href` (string) - Destination URL when the item is selected (used in page patterns)
- `type` (string) - Item subtext displayed below main text
- `value` (string) - Radio button or checkbox submitted form value 
- `category` (string) - Category identifier associated with quick filters
- `hint` (string) - Secondary text below radio or checkbox items
- `icon` (string) - Set to `"search"` for magnifying glass indicating search completion rather than link

#### Page search properties

- `show_search_button` (boolean) - Determines whether search button is displayed next to the input field; defaults to `false`
- `show_filters` (boolean) - Toggles quick-filters integration; defaults to `false`
- `filters` (object) - Configuration object for quick-filters tags:
  - `heading` (string) - Heading text preceding the filter buttons
  - `showAll` (boolean) - Enables an "All" filter toggle option
  - `allLabel` (string) - Display text for the "All" filter option (e.g. `"All"`)
  - `activeTags` (array) - Array of currently active filter tag value strings (e.g. `["all"]`)
  - `tags` (array) - List of filter tag objects:
    - `label` (string) - Visible display label for the filter tag
    - `value` (string) - Value used to filter menu items

#### Radio button and checkbox properties

- `show_other` (boolean) - Enables a fallback option for users to manually enter an unlisted choice
- `other_text` (string) - Hint text displayed between main list and **other** list item
- `other_buttontext` (string) - Radio button display text; defaults to `"Other"`
- `other_label` (string) - Label text for the other text input
- `selected_items` (array) - Array of pre-selected values when rendering radio or checkbox options

#### Pagination properties

- `pagination` (boolean) - Determines whether pagination controls are rendered below the results; defaults to `false`
- `pagination_previous_url` (string) - Target URL for the "Previous" page link
- `pagination_previous_page` (string) - Accessible label or link text for the "Previous" page control
- `pagination_next_url` (string) - Target URL for the "Next" page link
- `pagination_next_page` (string) - Accessible label or link text for the "Next" page control
- `pagination_items` (array) - Array of page number objects and truncators:
  - `number` (number) - Page number value
  - `href` (string) - Target URL for the specific page link
  - `current` (boolean) - Set to `true` to highlight the current active page
  - `ellipsis` (boolean) - Set to `true` to render a pagination ellipsis (`...`) visual separator

### Examples, variants and states including code and design assets

Below are the framework-specific macros and design file paths for the respective variations.

### Page patterns with search

#### Default page pattern

{% example "auto-suggestion/page.njk" %}

Use this variation for standard page layouts where users select a suggestion directly from the input without needing an explicit search submit button.

#### Page pattern with search button

{% example "auto-suggestion/page-search.njk" %}

Use this variation when the auto-suggest input sits within an explicit search form. The search button allows users to submit a query manually if they choose not to select a suggested item or want to view full search results on a dedicated page.

#### Page pattern with search button and filters

{% example "auto-suggestion/page-search-filters.njk" %}

Use this variation for complex search interfaces where users need to narrow down suggestions using specific filters alongside the auto-suggest input field.

### Radio button patterns

#### Radio button auto-suggestion

{% example "auto-suggestion/radio-button.njk" %}

Use this variation to implement the auto-suggest pattern within a radio button selection flow, allowing users to filter down a list of mutually exclusive choices as radio options.

#### Radio button with "other" option

{% example "auto-suggestion/radio-button-other.njk" %}

Use this variation when using radio buttons with auto-suggestion while providing a fallback option for users to enter their own custom response if their choice is not listed in the suggestions.

#### Radio button with pagination

{% example "auto-suggestion/radio-button-pagination.njk" %}

Use this variation when auto-suggested radio button choices span multiple pages, giving users controls to page through results when a search returns a large number of options.

#### Radio button with pagination and "other" option

{% example "auto-suggestion/radio-button-pagination-other.njk" %}

Use this variation to combine paginated radio button results with an option for users to manually enter their own response if the paginated options do not cover their selection.

## Content guidance

Input labels and instructions should be clear and concise.

Use labels that:
- clearly state what the user is searching for (e.g., "Search for your GP surgery")
- use hint text to explain how suggestions work if necessary (e.g., "Type at least 3 letters to search")
- keep option text concise and easy to scan
- ensure synonym matches are intuitive and accurate

Avoid using technical terms or internal codes in user-facing suggestion results unless users actively search with them.

