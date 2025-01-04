# Web UI Component Schema

## Background

When communicating with AI, for instance, to generate web pages or describe the planning of an entire website or web app, using natural language can often lead to misunderstandings due to its ambiguity. This results in higher costs due to repeated modifications. To avoid such issues, I propose using YAML as a structured description method to clearly define the components of each web page.

Currently, most frontend developers use prototyping tools like Figma, which produce images suitable for human viewing but not for effective two-way communication with AI. YAML offers a straightforward and clear method for describing web structures, making it ideal for this purpose.

While backend technologies, such as OpenAPI and database planning, have YAML-based standards, the frontend seems to lack a similar universal standard. Therefore, I created this Web UI Component Schema and paired it with linting tools to ensure users do not miss necessary fields, thereby improving efficiency.

> [中文版說明 (Chinese Version)](./README.md)

---

## How to Use

### 1. Using Lint Tools in VSCode

#### Steps:
1. **Download the JSON Schema**
   Download the `web_ui_schema.json` file from this repository to your local machine, or reference it directly via a remote URL, such as:
   ```
   https://raw.githubusercontent.com/richblack/Web-UI-Schema/refs/heads/main/web-ui-components-schema.json
   ```

2. **Install the YAML Extension in VSCode**
   - Search for and install the `YAML` extension (provided by Red Hat).

3. **Configure the JSON Schema**
   - Add or edit `.vscode/settings.json` in your workspace with the following content:
     ```json
     {
       "yaml.schemas": {
         "https://raw.githubusercontent.com/richblack/Web-UI-Schema/refs/heads/main/web-ui-components-schema.json": "*.yaml"
       }
     }
     ```
   - This allows VSCode to automatically validate and provide syntax suggestions for `.yaml` files.

4. **Write YAML Files**
   - Use YAML to describe your web page structure and ensure it complies with the schema standards.

### 2. Example YAML File

#### Example Description
Below is an example describing a login page and a forgot password page:

```yaml
$schema: "https://raw.githubusercontent.com/<your_username>/web-ui-schema/main/web_ui_schema.json"

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

