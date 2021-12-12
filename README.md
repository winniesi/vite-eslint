# Install and configure ESLint, Prettier, and Tailwind CSS using Vite (in VS Code)

## The First Step

Create a new Vite project through `yarn`:

```
yarn create vite 
```

Add ESLint, Prettier, and other integration packages to the project:

```
yarn add -D eslint \
    eslint-config-prettier \
    eslint-plugin-prettier \
    eslint-plugin-vue \
    eslint-plugin-html \
    prettier 
```

## Instructions

[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier) to turn off all rules that are unnecessary or might conflict with Prettier.

Make modifications to `.eslintrc.js` (if not, create one):

```
{
  "extends": [
    "some-other-config-you-use",
    "prettier"
  ]
}
```

Make sure to put `"prettier"` last, so it gets the chance to override other configs.

[eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier) runs Prettier as an ESLint rule and reports differences as individual ESLint issues.

Add these to the `.eslintrc.js`:

```
{
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

[eslint-plugin-vue](https://github.com/vuejs/eslint-plugin-vue) is an official ESLint plugin for vue.

My final configuration file looks like this:

```
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  extends: ["plugin:vue/vue3-recommended", "prettier"],
  parserOptions: {
    ecmaVersion: 13,
    sourceType: "module",
  },
  plugins: ["vue", "html", "prettier"],
  rules: {
    "prettier/prettier": "error", 
  },
};
```

## In VS Code

To integrate ESLint into VS Code, we need to install the ESLint extension and Prettier extension for VS Code. To configure ESLint to automatically fix syntax and formatting issues, we need to create the file .vscode/settings.json:

```
{
    "editor.codeActionsOnSave": {
        "source.fixAll": true,
        "source.fixAll.eslint": true
    },
    "eslint.alwaysShowStatus": true,
    "eslint.validate": [
        "vue",
        "javascript",
        "javascriptreact",
        "html",
    ],
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
}
```

It can also be used as a global configuration for vscode.

Now, whenever we save a vue file or a HTML file, it should automatically be formatted.