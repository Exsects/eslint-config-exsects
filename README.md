# VSCode with ESLint, Prettier, and EditorConfig

These are my settings for ESLint, Prettier, and EditorConfig

## What it does

- Lints JavaScript based on the latest standards
- Fixes issues and formatting errors with Prettier
- Lints + Fixes JavaScript inside of HTML script tags
- Lints + Fixes JavaScript via `eslint-config-airbnb-base`
- You can see all the style guidelines `eslint-config-airbnb-base` follows through [this link here](https://github.com/airbnb/javascript)
- Defines and maintains a consistent coding style among all the IDEs and editors used within a team of developers.

## Local / Per Project Installation

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```
npx install-peerdeps --dev eslint-config-airbnb-base
```

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc.json` file in the root of your project's directory (it should live where package.json does). Your `.eslintrc.json` file should look like this:

```json
{
  "extends": ["airbnb-base", "prettier"],
  "plugins": ["prettier"],
  "rules": {
    "no-console": "off",
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 120,
        "tabWidth": 8
      }
    ]
  }
}
```

5. Now create a file named `.editorconfig.` in the root of your project's directory (it should live where package.json does). Your `.editorconfig` file should look like this:

```
root = true

[*]
charset = utf-8
end_of_line = lf
trim_trailing_whitespace = true
insert_final_newline = true

[{.,}*.{js{,*},y{a,}ml}]
indent_style = space
indent_size = 2

[*.{md,txt}]
indent_style = space
indent_size = 2
trim_trailing_whitespace = false
```

## VSCode Configuration

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

2. Click on the gear icon at bottom left of VSCode and go to Settings.

3. At the top right corner of VSCode click on the file icon as shown in the image below.

   !["Open Settings in JSON"](https://user-images.githubusercontent.com/38166320/82932854-0f8b9b00-9f57-11ea-912a-e60c649d8d27.png)

4. Enter the following configurations to `settings.json` and hit save.

```js
// These are all my auto-save configs
"editor.formatOnSave": true,
// Turn it off for JS, we will do this via ESLint
  "[javascript]": {
    "editor.formatOnSave": false
  },
// Tells the ESLint plugin to run and format on save
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
// Optional (If you have Prettier extension installed): Turns off VSCode's Prettier Extension for JS files only since ESLint already formats JS files for us.
  "prettier.disableLanguages": ["javascript"],
```
