# Component Documentation

## `MyApp.js`: Core Application Component

This file serves as the root component for the application. It is responsible for orchestrating the overall application structure and managing the primary state.

### Responsibilities

{% cardGroup cols=3 %}
{% card title="State Management" icon="database" %}
`MyApp` holds the central list of character data. All modifications to this list, such as adding or removing characters, are handled by functions within this component. This centralized approach ensures a single source of truth.
{% /card %}
{% card title="Component Composition" icon="component" %}
It renders the primary child components, `Table` and `Form`, and arranges them to create the complete user interface.
{% /card %}
{% card title="Data Flow" icon="git-branch" %}
`MyApp` facilitates communication between its child components. It passes the character data down to the `Table` component for display and passes state-updating functions to both the `Table` (for deletions) and `Form` (for additions).
{% /card %}
{% /cardGroup %}

### Key Functions

{% cardGroup cols=2 %}
{% card title="removeCharacter(index)" icon="function-square" %}
Removes a character from the state based on their index. This function is passed as a prop to the `Table` component.
{% /card %}
{% card title="handleSubmit(character)" icon="function-square" %}
Adds a new character to the state. This function is passed as a prop to the `Form` component to handle form submissions.
{% /card %}
{% /cardGroup %}

***

## `Table.js`: Data Display Component

The `Table.js` component is a presentational component designed to display a collection of character data in a tabular format. It receives all its data and functionality via props from a parent component.

### Structure

The `Table` is composed of two main sub-components:

{% cardGroup cols=2 %}
{% card title="TableHeader" icon="layout-list" %}
A static component that renders the header row for the table (e.g., "Name", "Job").
{% /card %}
{% card title="TableBody" icon="list-ordered" %}
A dynamic component that iterates over the character data and renders a table row for each character.
{% /card %}
{% /cardGroup %}

### Props

{% parameterField name="characterData" type="Array" required=true %}
The list of character objects to be displayed in the table.
{% /parameterField %}

{% parameterField name="removeCharacter" type="Function" required=true %}
A callback function that is invoked when a row's "Delete" button is clicked. The function is called with the index of the character to be removed.
{% /parameterField %}

***

## `Form.js`: Data Entry Component

This component provides the user interface for adding new characters to the application. It is a controlled form that manages its own internal state for the input fields.

### Responsibilities

{% cardGroup cols=3 %}
{% card title="User Input" icon="edit-3" %}
Renders a form with controlled input fields for a character's name and job.
{% /card %}
{% card title="State Management" icon="database" %}
Uses local component state to track the user's input in real-time.
{% /card %}
{% card title="Data Submission" icon="send" %}
On submission, it invokes a callback prop from the parent component, passing the new character data from its internal state. After submission, the form's input fields are cleared.
{% /card %}
{% /cardGroup %}

### Props

{% parameterField name="handleSubmit" type="Function" required=true %}
A callback function invoked when the form is submitted. It receives the new character object, assembled from the form's local state, as its only argument.
{% /parameterField %}