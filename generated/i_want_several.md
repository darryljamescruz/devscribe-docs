# CSC-308 Application Documentation

This documentation provides a comprehensive overview of the `darryljamescruz/csc-308-app` codebase, its architecture, and its core functionalities.

## Overview

### Introduction

The `csc-308-app` is a single-page web application for managing a list of characters. It features a clean user interface for creating, viewing, and deleting character entries. Data persists for the duration of a user's session.

### Core Features

The application is built around three key capabilities:

{% cardGroup cols=3 gap="md" %}
{% card title="Display Characters" icon="list" %}
All existing characters are rendered in a clear, tabular format, showing their name and job.
{% /card %}
{% card title="Add New Characters" icon="plus-circle" %}
A dedicated form allows users to input a name and a job for a new character and add them to the list.
{% /card %}
{% card title="Remove Characters" icon="trash-2" %}
Each character in the table has an associated control to remove them from the list.
{% /card %}
{% /cardGroup %}

{% callout type="info" %}
The user interface provides immediate feedback, instantly reflecting changes such as adding or removing a character.
{% /callout %}

## Architecture

### Component-Based Design

The application is built using a modern, component-based architecture. The UI is broken down into logical, reusable, and independent pieces, which simplifies development and maintenance by isolating concerns.

The primary components are:

{% cardGroup cols=3 gap="md" %}
{% card title="`App`" icon="component" %}
The main application container that manages state and orchestrates child components.
{% /card %}
{% card title="`CharacterTable`" icon="table" %}
A component dedicated to displaying the list of characters.
{% /card %}
{% card title="`AddCharacterForm`" icon="file-plus-2" %}
A form for capturing user input to create new characters.
{% /card %}
{% /cardGroup %}

### State Management

The application employs a centralized state management pattern. The top-level `App` component is responsible for holding and managing the list of characters, acting as the "single source of truth" to ensure data consistency.

Data flows in a predictable, unidirectional manner:

{% cardGroup cols=2 gap="md" %}
{% card title="State is passed down" icon="arrow-down-circle" %}
The `App` component passes the character list as a prop to child components that need to display it.
{% /card %}
{% card title="Actions are passed up" icon="arrow-up-circle" %}
Child components use callback functions (passed as props) to notify the `App` component that the state needs to change, such as when a user adds or removes a character.
{% /card %}
{% /cardGroup %}

{% callout type="tip" %}
This design leads to a more maintainable and debuggable codebase.
{% /callout %}

## Data Flow

Understanding how data moves through the application is key to understanding its functionality. All operations follow a clear, unidirectional flow.

### Adding a New Character

{% steps %}
{% step title="User Interaction" %}
The user interacts with the `AddCharacterForm`, entering a name and a job.
{% /step %}
{% step title="Callback Invocation" %}
Upon submission, the `AddCharacterForm` invokes a callback function passed down from the `App` component, sending the new character's data as an argument.
{% /step %}
{% step title="State Update" %}
The `App` component receives this data and updates its central state by adding the new character to the list.
{% /step %}
{% step title="UI Re-render" %}
This state update automatically triggers a re-render of the `CharacterTable`, which now displays the newly added character.
{% /step %}
{% /steps %}

### Deleting an Existing Character

{% steps %}
{% step title="User Action" %}
The user clicks the "Delete" button next to a character within the `CharacterTable`.
{% /step %}
{% step title="Callback Trigger" %}
This action triggers a callback function, signaling to the `App` component which character to remove (identified by its index).
{% /step %}
{% step title="State Update" %}
The `App` component updates its state by filtering out the specified character from the list.
{% /step %}
{% step title="UI Re-render" %}
The state change causes the `CharacterTable` to re-render, and the deleted character is no longer visible in the UI.
{% /step %}
{% /steps %}