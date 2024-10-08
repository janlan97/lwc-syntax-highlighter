# LWC Syntax Highlighter

The SyntaxHighlighter component is designed to transform plain code or JSON text into readable and visually appealing outputs with proper formatting and syntax coloring. It leverages both Prism.js for syntax highlighting and js-beautify for code formatting.

<p align="center">
  <img src="https://github.com/user-attachments/assets/dd6630a8-4697-4e33-8ab4-c5d33fcf24c3">
</p>
</br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/92e79fd3-4317-4097-b412-d3144e0c2e1f">
</p>
<p align="center">Standard long text area...</p>
</br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/ef2feb1a-6775-499f-9e5c-79643bc25e1a">
</p>
<p align="center">Transformed to SyntaxHighlighter output</p>
</br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/4606d03d-c204-4a5b-93a6-5c4cefa7ec40">
</p>
<p align="center">Modal</p>
</br>

## Key Features

- **Multi-Language Support**: Easily highlight code in various languages like JavaScript, HTML, Apex, and more by simply setting the `language` attribute.
- **Prism.js Integration**: Utilizes Prism.js for robust and customizable syntax highlighting.
- **js-beautify Integration**: Automatically formats your code according to the specified language, making it more readable and maintainable. You can include your own formatting options.
- **Dynamic Code Rendering**: The component dynamically renders the `code` with reflected syntax highlighting and formatting according to the language.
- **Edit / Read**: Component can be used either in read or edit mode.
- **Modal Included**: Supports modals for code editing and copying, making it versatile for both display and interaction.

## Components

- **`SyntaxHighlighter`**: A base component that emulates code snippet.
- **`CodeInput`**: A wrapper component that mimics the styling of a standard Salesforce record form field, allowing for seamless integration with standard Salesforce UI.
- **`CodeInputModal`**: A modal component that presents the code in a larger view, with the added functionality to copy and edit the code directly from the modal.

# Usage

To use the `SyntaxHighlighter` component, simply include it in your Lightning Web Component with the desired language and code:

## **Base component usage:**
<p align="center">
  <img src="https://github.com/user-attachments/assets/2c0f61c9-045d-46e4-84a0-77a963e40d1a">
</p>

```html
<c-syntax-highlighter language="json" code="{"a":1,"b":2}"></c-syntax-highlighter>
```

## **Record Form Field Wrapper (Read Mode):**
<p align="center">
  <img src="https://github.com/user-attachments/assets/c383a078-91b3-42b0-9a00-a908bf89cce9">
</p>

```html
<c-code-input data-key={field.apiName} language="json" code={field.value} label={label} read-only field-name={field.apiName}>
```

## **Record Form Field Wrapper (Edit Mode):**
<p align="center">
  <img src="https://github.com/user-attachments/assets/ecedfc93-2388-4b0e-9c68-f4e5f85ceabb">
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3ca931ea-3ccf-4b95-a452-89a22875821c">
</p>

```html
<c-code-input data-key={field.apiName} language="json" code={field.value} label={field.label} read-only="false" field-name={field.apiName} oncodeinputchanged={handleCodeInputChange}></c-code-input>
```
> [!IMPORTANT]
> Parent component (ex. custom form) must handle `codeinputchanged` event to propagate `codeInput` changes to sobject record


# LWC Component Documentation

## CodeInput
A wrapper component that mimics the styling of a standard Salesforce record form field, allowing for seamless integration with standard Salesforce UI.

### Properties

| Property           | Type    | Default          | Description                                                                                 |
|--------------------|---------|------------------|---------------------------------------------------------------------------------------------|
| `@api language`    | String  | `'javascript'`   | Code language for the input.                                                                |
| `@api label`       | String  | Optional         | Label for input.                                                                            |
| `@api fieldName`   | String  | Optional         | Associates the code input with a specific field.                                            |
| `@api readOnly`    | Boolean | `false`          | Flag for turn on / off read-only mode.                                                      |

### Events
## codeinputchanged
Event generated after changing code in modal, it's dispatched to codeInput and then propagated higher in hierarchy
| Parameter Name       | Type    | Description    |
|----------------------|---------|----------------|
| fieldName            | String  | Field API name |
| value                | String  | New value      |

example:
```html
<c-code-input data-key={field.apiName} language="json" code={field.value} label={field.label} read-only={readOnly} field-name={field.apiName} oncodeinputchanged={handleCodeInputChange}></c-code-input>
```
```javascript
    handleCodeInputChange(e) {
        const result = e.detail.result;
        const value = result.value;
        const field = result.fieldName;
        // propagate value to record in Salesforce...
    }
```

## CodeInputModal
A modal component that presents the code in a larger view, with the added functionality to copy and edit the code directly from the modal.
To open modal double click on input or click edit pencil.

### Properties

| Property           | Type    | Default          | Description                                                                                 |
|--------------------|---------|------------------|---------------------------------------------------------------------------------------------|
| `@api language`    | String  | `'javascript'`   | Code language for the input.                                                                |
| `@api code`        | String  | `''`             | Displayed code context.                                                                     |
| `@api label`       | String  | Optional         | Label for input.                                                                            |
| `@api readOnly`    | Boolean | `false`          | Flag for turn on / off read-only mode.                                                      |
| `@api fieldName`   | String  | Optional         | Associates the code input with a specific field.                                            |

## SyntaxHighlighter
A base component that emulates code snippet.

### Properties

| Property           | Type    | Default      | Description                                                                                  |
|--------------------|---------|--------------|----------------------------------------------------------------------------------------------|
| `@api language`    | String  | `'json'`     | Code language for the input.                                                                 |
| `@api code`        | String  |              | Displayed code context.                                                                      |

