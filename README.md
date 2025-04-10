# Wform Documentation

## Introduction

Wform is a lightweight, attribute-driven multi-step form solution for Webflow developed by https://hubstic.com. It allows you to create multi-step forms using simple data attributes without requiring any coding knowledge.

## Table of Contents

1. [Installation](#installation)
2. [Core Attributes](#core-attributes)
   - [Enable Wform](#enable-Wform)
   - [Steps](#steps)
   - [Navigation Buttons](#navigation-buttons)
   - [Submit Button](#submit-button)
3. [Validation](#validation)
   - [Required Fields](#required-fields)
   - [Disabled States](#disabled-states)
   - [Email Validation](#email-validation)
4. [Progress Indicators](#progress-indicators)
   - [Automatic Progress Indicators](#automatic-progress-indicators)
   - [Custom Progress Indicators](#custom-progress-indicators)
5. [Additional Features](#additional-features)
   - [Step Text Display](#step-text-display)
   - [Intro Cards](#intro-cards)
   - [Phone Number Formatting](#phone-number-formatting)
   - [Keyboard Shortcuts](#keyboard-shortcuts)
   - [Scroll to Top](#scroll-to-top)
6. [Error Handling](#error-handling)
7. [Limitations](#limitations)
8. [Examples](#examples)

## Installation

To use Wform in your Webflow project, add the following script to your project's custom code section:

```html
<script src="https://cdn.jsdelivr.net/gh/faustodimarco/wform@main/wform.min.js"></script>
```

## Core Attributes

### Enable Wform

To enable Wform on your form, add the `data-form="multistep"` attribute to the Form element:

```html
<form data-form="multistep">
  <!-- Form content -->
</form>
```

**Note:** You can only have one multi-step form per page.

### Steps

Each step in your form should be indicated with the `data-form="step"` attribute:

```html
<div data-form="step">
  <!-- Step 1 content -->
</div>

<div data-form="step">
  <!-- Step 2 content -->
</div>

<div data-form="step">
  <!-- Step 3 content -->
</div>
```

**Note:** You do not need to hide the individual steps in the Webflow designer. They are automatically hidden on the published site.

### Navigation Buttons

To create navigation buttons, use the following attributes:

#### Next Button

```html
<a data-form="next-btn" href="#">Next</a>
```

#### Back Button

```html
<a data-form="back-btn" href="#">Back</a>
```

You can use either Button elements or Link Blocks for these buttons. Do not use the Form Submit Button for navigation.

**Notes:**
- Navigation buttons can be placed anywhere on the page, not necessarily inside the Form element.
- You can have multiple instances of next and back buttons (for example, a pair of back and next buttons inside each step).

### Submit Button

For the submit button, use the Form Submit Button with the `data-form="submit-btn"` attribute:

```html
<input type="submit" value="Submit" data-form="submit-btn">
```

**Note:** The submit button must be inside the Form element.

## Validation

### Required Fields

Wform uses Webflow's native required field functionality. Simply mark fields as required in Webflow's designer:

```html
<input type="text" required>
```

The next button will be automatically disabled if required fields in the current step are not completed.

### Disabled States

When a button is disabled (e.g., the next button when required fields are not filled), Wform adds a `disabled` class to the button. You can style this class in Webflow:

```css
.disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Email Validation

Email inputs are automatically validated to ensure they contain a valid email format:

```html
<input type="email" required>
```

## Progress Indicators

### Automatic Progress Indicators

To create progress indicators, add the following attributes:

```html
<div data-form="progress">
  <div data-form="progress-indicator"></div>
  <div data-form="progress-indicator"></div>
  <div data-form="progress-indicator"></div>
</div>
```

Wfrom will automatically add the `current` class to the current step indicator and the `completed` class to completed step indicators.

### Custom Progress Indicators

You can create custom progress indicators anywhere on the page:

```html
<div data-form="custom-progress-indicator"></div>
<div data-form="custom-progress-indicator"></div>
<div data-form="custom-progress-indicator"></div>
```

## Additional Features

### Step Text Display

You can display the current step number and total steps using these attributes:

```html
<span>Step <span data-text="current-step"></span> of <span data-text="total-steps"></span></span>
```

### Intro Cards

For steps without inputs (like intro or confirmation cards), add the `data-card="true"` attribute:

```html
<div data-form="step" data-card="true">
  <!-- Intro content with no inputs -->
</div>
```

### Phone Number Formatting

To automatically format phone numbers, add the `data-phone-autoformat` attribute with a format pattern:

```html
<input type="tel" data-phone-autoformat="xxx-xxx-xxxx">
```

Format patterns use `x` to represent digits. You can use other characters for formatting:

```html
<input type="tel" data-phone-autoformat="(xxx) xxx-xxxx">
```

### Keyboard Shortcuts

#### CMD/CTRL + Enter to Submit

To enable form submission with CMD/CTRL + Enter, add the `data-submit="true"` attribute to the form:

```html
<form data-form="multistep" data-submit="true">
  <!-- Form content -->
</form>
```

#### Enter to Progress

To enable progressing to the next step with the Enter key, add the `data-enter="true"` attribute to the form:

```html
<form data-form="multistep" data-enter="true">
  <!-- Form content -->
</form>
```

### Scroll to Top

To automatically scroll to the top of the form when navigating between steps, add the `data-scroll-top="true"` attribute to the form:

```html
<form data-form="multistep" data-scroll-top="true">
  <!-- Form content -->
</form>
```

## Error Handling

Wform displays validation errors in the console and adds the `error` class to invalid inputs. You can style this class in Webflow:

```css
.error {
  border-color: red;
}
```

For more detailed error messages, you can add an error message element after each input:

```html
<div class="form-input-wrapper">
  <input type="text" required>
  <div class="error-message"></div>
</div>
```

## Limitations

- Only one multi-step form per page is supported
- The submit button must be inside the Form element
- Navigation buttons can be placed anywhere on the page

## Examples

### Basic Multi-Step Form

```html
<form data-form="multistep">
  <!-- Step 1 -->
  <div data-form="step">
    <h2>Step 1: Personal Information</h2>
    <label>Name</label>
    <input type="text" required>
    <label>Email</label>
    <input type="email" required>
    <a data-form="next-btn" href="#">Next</a>
  </div>
  
  <!-- Step 2 -->
  <div data-form="step">
    <h2>Step 2: Contact Information</h2>
    <label>Phone</label>
    <input type="tel" data-phone-autoformat="(xxx) xxx-xxxx" required>
    <a data-form="back-btn" href="#">Back</a>
    <a data-form="next-btn" href="#">Next</a>
  </div>
  
  <!-- Step 3 -->
  <div data-form="step">
    <h2>Step 3: Confirmation</h2>
    <p>Please review your information and submit the form.</p>
    <a data-form="back-btn" href="#">Back</a>
    <input type="submit" value="Submit" data-form="submit-btn">
  </div>
</form>

<!-- Progress Indicators -->
<div data-form="progress">
  <div data-form="progress-indicator"></div>
  <div data-form="progress-indicator"></div>
  <div data-form="progress-indicator"></div>
</div>

<!-- Step Counter -->
<div>
  Step <span data-text="current-step"></span> of <span data-text="total-steps"></span>
</div>
```

### Form with Intro Card

```html
<form data-form="multistep" data-scroll-top="true" data-enter="true">
  <!-- Intro Card -->
  <div data-form="step" data-card="true">
    <h2>Welcome to our Survey</h2>
    <p>This survey will take approximately 5 minutes to complete.</p>
    <a data-form="next-btn" href="#">Start Survey</a>
  </div>
  
  <!-- Step 1 -->
  <div data-form="step">
    <h2>Question 1</h2>
    <label>How did you hear about us?</label>
    <select required>
      <option value="">Please select</option>
      <option value="search">Search Engine</option>
      <option value="social">Social Media</option>
      <option value="friend">Friend</option>
    </select>
    <a data-form="back-btn" href="#">Back</a>
    <a data-form="next-btn" href="#">Next</a>
  </div>
  
  <!-- Step 2 -->
  <div data-form="step">
    <h2>Question 2</h2>
    <label>Would you recommend us to a friend?</label>
    <input type="radio" name="recommend" value="yes" required> Yes
    <input type="radio" name="recommend" value="no"> No
    <a data-form="back-btn" href="#">Back</a>
    <input type="submit" value="Submit" data-form="submit-btn">
  </div>
</form>
```
