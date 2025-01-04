# Web UI Component Schema

## Background

Natural language communication with AI for web development tasks, especially front-end/back-end planning, often suffers from ambiguity, leading to incorrect outputs. Structured documents are a far superior alternative. This project proposes using YAML to precisely define web page elements, mitigating this issue.

While prototyping tools like Figma are common, their image-based outputs are inefficient for AI processing, consuming excessive tokens, potentially misrepresenting details, and hindering bidirectional communication. YAML offers a simpler, clearer, machine- and human-readable solution, resembling bracketless JSON with its "feature: value" notation.

Existing YAML standards effectively address back-end aspects like OpenAPI and database schema definition. However, a comparable front-end standard is lacking. Therefore, this project defines a Web UI Component Schema, specifying required fields for each component. This complex information, difficult for humans to memorize, can be readily managed with linting tools, providing auto-completion in VS Code and ensuring no required fields are omitted.

> [中文版說明 (Chinese Version)](./README.md)

---

## How to Use

### 1. Using Lint Tools in VSCode

#### Steps

1. **Download the JSON Schema**
   Download the `web_ui_schema.json` file from this repository to your local machine, or reference it directly via a remote URL, such as:

    ```Bash
    https://raw.githubusercontent.com/richblack/Web-UI-Schema/main/web-ui-components-schema.json
    ```

2. **Install the YAML Extension in VSCode**
   - Search for and install the `YAML` extension (provided by Red Hat).

3. **Configure the JSON Schema**
   - Add or edit `.vscode/settings.json` in your workspace with the following content:

     ```json
     {
       "yaml.schemas": {
           "https://raw.githubusercontent.com/richblack/Web-UI-Schema/main/web-ui-components-schema.json": ["*.yaml", "*.yml"]
           // For local file usage, use:
           // "./web-ui-components-schema.json": ["*.yaml", "*.yml"]
       },
       "yaml.completion": true,
       "yaml.validate": true,
       "yaml.format.enable": true,
       "yaml.customTags": [],
       "[yaml]": {
           "editor.insertSpaces": true,
           "editor.tabSize": 2,
           "editor.autoIndent": "keep",
           "editor.formatOnType": true,
           "editor.formatOnSave": true
       }
     }
     ```

   - This allows VSCode to automatically validate and provide syntax suggestions for both `.yaml` and `.yml` files
   - Supports formatting and auto-completion features
   - You can choose to use either remote or local schema files

4. **Write YAML Files**
   - Use YAML to describe your web page structure and ensure it complies with the schema standards.

### 2. Example YAML File

#### Example Description

Below is an example describing a login page and a forgot password page:

```yaml
$schema: "https://raw.githubusercontent.com/richblack/Web-UI-Schema/main/web-ui-components-schema.json"

pages:
  - id: "login"
    label: "Login Page"
    components:
      - type: "text_input"
        id: "username"
        label: "Username"
        placeholder: "Enter your username"
      - type: "text_input"
        id: "password"
        label: "Password"
        inputType: "password"
        placeholder: "Enter your password"
      - type: "button"
        id: "login_button"
        label: "Login"
        action: "/login"
  - id: "forgot_password"
    label: "Forgot Password Page"
    components:
      - type: "text_input"
        id: "email"
        label: "Email"
        inputType: "email"
        placeholder: "Enter your email"
      - type: "button"
        id: "submit_button"
        label: "Submit"
        action: "/forgot-password"
```

---

## Schema Structure

This JSON Schema defines common Web UI components, including:

- **Text Input**
- **Text Area**
- **Checkbox**
- **Radio Button**
- **Select**
- **Date Picker**
- **Time Picker**
- **File Upload**
- **Button**
- **Link**
- **Image**
- **Table**

Each component has corresponding properties, such as `id`, `label`, `type`, `style`, etc. For detailed definitions, please refer to the `web_ui_schema.json` file.

---

## Example Generated HTML

Below is an example of HTML generated from the above YAML, styled with Bootstrap:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mt-5">
        <h1 class="text-center">Login Page</h1>
        <form action="/login" method="POST">
            <div class="mb-3">
                <label for="username" class="form-label">Username</label>
                <input type="text" id="username" name="username" class="form-control" placeholder="Enter your username" required>
            </div>
            <div class="mb-3">
                <label for="password" class="form-label">Password</label>
                <input type="password" id="password" name="password" class="form-control" placeholder="Enter your password" required>
            </div>
            <button type="submit" class="btn btn-primary w-100">Login</button>
        </form>
    </div>
</body>
</html>
```

---

## Future Plans

- Add support for more components, such as navigation bars, modals, progress bars, etc.
- Optimize YAML syntax suggestions to enhance development efficiency.
- Provide example tools to automatically convert YAML into HTML or other frontend framework code.

---

## Contribution

Feel free to submit Issues or Pull Requests! We look forward to collaborating with the community to improve this project.

---

## License

This project is licensed under the [MIT License](LICENSE).
