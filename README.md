# VSCode with ESLint, Prettier, and EditorConfig

_Adapted from Wes Bos's [No-Sweat™ Eslint and Prettier Setup - with or without VS Code](https://github.com/wesbos/eslint-config-wesbos)_

These are my settings for ESLint, Prettier, and EditorConfig.

## What it does

- Lints JavaScript based on the latest standards
- Fixes issues and formatting errors with Prettier
- Lints + Fixes JavaScript inside of HTML script tags
- Lints + Fixes JavaScript via `eslint-config-airbnb-base`
- You can see all the style guidelines `eslint-config-airbnb-base` follows through [this link here](https://github.com/airbnb/javascript)
- Defines and maintains a consistent coding style among all the IDEs and editors used within a team of developers.

## Local / Per Project Installation

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install the Airbnb config for ESLint:

```
npx install-peerdeps --dev eslint-config-airbnb-base
```

3. We also have to install the Prettier config for ESLint as well:

```
npm install -D prettier eslint-config-prettier eslint-plugin-prettier
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
        "printWidth": 80
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

1. Install both the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) and the [EditorConfig for VScode extension](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)

2. Go to VSCode's settings using the command `CTRL` + `,` (for Windows users) or `⌘` + `,` (for MacOS users).

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
