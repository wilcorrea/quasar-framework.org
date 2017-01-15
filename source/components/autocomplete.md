title: Autocomplete
---
Autocomplete component binds to a text field and offers suggestions to the user while typing based on a static list of results or an Ajax call.
<input type="hidden" data-fullpage-demo="form/autocomplete">

## Basic Usage
As long as this component is rendered by Vue it will capture all Ajax calls.
``` html
<!-- Fills with its own input field -->
<q-autocomplete v-model="terms" @search="search"></q-autocomplete>

<!-- Binds to a specified textfield -->
<q-autocomplete v-model="terms" @search="search">
  <input v-model="terms" class="full-width" placeholder="Type 'fre'" />
</q-autocomplete>

<!-- Binds to a textfield from a component, like Search -->
<q-autocomplete v-model="terms" @search="search" set-width :max-results="2">
  <q-search v-model="terms"></q-search>
</q-autocomplete>
```

## Vue Properties
| Vue Property | Type | Default Value | Description |
| --- | --- | --- | --- |
| `min-characters` | Number | 1 | How many minimum characters can trigger component to suggest something? |
| `max-results` | Number | 6 | How many results can we display at a time? |
| `delay` | Number | 500 | How many milliseconds to wait before triggering a suggestion? |
| `static-data` | Array | *None* | Use static suggestions. No need to do an Ajax call. Filtering is provided by Autocomplete component. |
| `set-width` | Boolean | false | Suggestions popover should have at least the width of the binded text field. |
| `delimiter` | Boolean | false | Should suggestions popover display a delimiter between results? |

When using static data, specify an array like this (notice that it uses [ListItem component props](/components/list-item.html)):
``` js
// static-data
[
  {
    value: 'Romania', // what gets Autocompleted with
    label: 'Romania', // what gets displayed as main label for this suggestion

    secondLabel: 'Continent: Europe', // optional
    icon: 'location_city', // optional
    stamp: '18 mil', // optional
    ...
  },
  ...
]
```

## Vue Methods
Only if you want to also trigger it manually. Ajax calls trigger these methods automatically.

| Vue Method | Description |
| --- | --- |
| `trigger()` | Trigger suggestions. |
| `close()` | Close suggestions popover. |
| `setValue()` | Set textfield string to the value supplied. |
| `move(offset)` | Move selection cursor on suggestions popover by offset (Number, example: 3 for three selections down, -1 for one selection up). |

## Vue Events
| Vue Event | Description |
| --- | --- |
| `@search(terms, Function done)` | Triggered by the component when a search should start and offer some results. |
| `@input(value)` | At change the value of component this event is fired sending the value what was assigned (even if it is done by setValue). |
| `@selected(item)` | It is fired when one item of list is selected and send the entire item selected (note what `selected` is always triggered after `input`). |

Example for `search` event:

``` js
function search (terms, done) {
  // do something with terms, like an Ajax call for example
  // then call done(Array results)

  // DO NOT forget to call done! When no results, just call with empty array as param
  // Example: done([])
}
```
