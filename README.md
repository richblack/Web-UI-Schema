# Web UI Component Schema

## 緣起 / Background

當我們與 AI 溝通時，例如請 AI 幫忙產生網頁，甚至描述整個網站或 Web App 的規劃，若使用自然語言，容易因為語意模糊產生誤解，導致重複修改的成本。因此，我希望使用 YAML 作為結構化的描述方式，清楚定義每個網頁的組成元素，從而避免這類問題。

目前，大多數前端使用 Figma 等 prototyping 工具，但這類工具產生的多為圖片，僅適用於人類查看，對於與 AI 的雙向溝通並不友好。而 YAML 提供了一種簡單且清晰的方式，適合用於描述網頁結構。

雖然後端技術，例如 OpenAPI 和資料庫規劃，都有 YAML 的標準規範，但前端部分似乎缺乏類似的通用標準。因此，我制定了這個 Web UI Component Schema，並搭配 lint 工具使用，以確保使用者不會遺漏必要的欄位，從而提升效率。

> [English Version](./README_english.md)

---

## 如何使用 / How to Use

### 1. 在 VSCode 中使用 Lint 工具

#### 步驟：

1. **下載 JSON Schema**
   將本 Repository 的 `web_ui_schema.json` 下載至本地，或直接引用遠端 URL，例如：

   ```
   https://raw.githubusercontent.com/richblack/Web-UI-Schema/main/web-ui-components-schema.json
   ```

2. **安裝 VSCode 的 YAML 擴展工具**
   - 搜尋並安裝 `YAML` 擴展（由 Red Hat 提供）。

3. **設定 JSON Schema**
   - 在 VSCode 的工作區新增或編輯 `.vscode/settings.json`，添加以下內容：

     ```json
     {
       "yaml.schemas": {
         "https://raw.githubusercontent.com/richblack/Web-UI-Schema/main/web-ui-components-schema.json": "*.yaml"
       }
     }
     ```

   - 這將允許 VSCode 自動對 `.yaml` 文件進行驗證並提供語法提示。

4. **編寫 YAML 文件**
   - 使用 YAML 描述您的網頁結構，並確保符合 Schema 的規範。

### 2. 範例 YAML 文件

#### 範例描述

以下是一個描述登入頁與忘記密碼頁的 YAML 範例：

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

## Schema 結構 / Schema Structure

此 JSON Schema 定義了常用的 Web UI 元件，包括：

- **Text Input (文字輸入框)**
- **Text Area (多行文字區域)**
- **Checkbox (核取方塊)**
- **Radio Button (單選按鈕)**
- **Select (下拉選單)**
- **Date Picker (日期選擇器)**
- **Time Picker (時間選擇器)**
- **File Upload (檔案上傳)**
- **Button (按鈕)**
- **Link (超連結)**
- **Image (圖片)**
- **Table (表格)**

每個元件都有對應的屬性，例如 `id`, `label`, `type`, `style` 等，詳細定義請參考 `web_ui_schema.json` 文件。

---

## 範例生成 HTML / Example Generated HTML

以下是根據上述 YAML 產生的 HTML 範例，並整合 Bootstrap 美化：

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

## 未來規劃 / Future Plans

- 添加更多元件支持，例如導航列、模態框、進度條等。
- 優化 YAML 的語法提示，提升開發效率。
- 提供範例工具，將 YAML 自動轉換為 HTML 或其他前端框架代碼。

---

## 貢獻 / Contribution

歡迎提交 Issues 或 Pull Requests！我們期待與社群合作，共同完善這個項目。

---

## 授權 / License

本項目採用 [MIT License](LICENSE) 授權。
