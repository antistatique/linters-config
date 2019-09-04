# Antistatique Linter Config

> Antistatique truth source and **opinionated** linters configuration.

Currently **supports**:
- [🔹 ESLint](https://eslint.org/)
- [🌈 Prettier](https://eslint.org/) ([only for JavaScript](https://github.com/prettier/prettier/issues/5948))
- [👔 Stylelint](https://stylelint.io/)

## What it does
- **Lints** JavaScript and CSS based on the latest standards
- Manage **pre-commit** git hook to prevent 💩 commits
- Ensure decent **code quality** at [Antistatique](https://antistatique.net/)

## Install

⚠️ Because [🐶Husky](https://github.com/typicode/husky) will be our main git hooks manager, the following process may rewrite/remove all your existing hooks. **Save them before continuing**

**Requirement**:
- [📗 NodeJS 10+](https://nodejs.org/en/)
- [🐈 Yarn](https://yarnpkg.com/lang/en/)
- [📦 npx](https://github.com/npm/npx)

First, you'll need to **install** required dependencies and **get** the linters configuration files (`.eslintrc` & `.stylelintrc`):


```bash
$ npx install-peerdeps --dev antistatique-linters-config
$ wget https://raw.githubusercontent.com/antistatique/linters-config/master/.eslintrc
$ wget https://raw.githubusercontent.com/antistatique/linters-config/master/.stylelintrc
```

Then, to enable pre-commit hook, you'll need to **add (and edit)** the following code to your `./package.json`:

```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "src/**/*.{js,jsx}": "eslint --ext .js,.jsx --max-warnings=0",
    "src/**/*.{css,scss,styles.js,styles.jsx}": "stylelint"
  }
}
```

This will lint only the staged files (NOT the entire project) to ensure a fast check of your commit's content.

You can also add the following npm scripts to `./package.json` to **manually \*trigger linters**:

```json
{
  "scripts": {
    "lint:css": "stylelint ./**/*.{css,scss,styles.js,styles.jsx}",
    "lint:js": "eslint . --ext .js,.jsx --max-warnings=0"
  }
}
```

```bash
$ yarn lint:js
$ yarn lint:csss
```

*\*Don't use those scripts to update the `lint-staged` configuration. This will not work properly*

## IDE

The process above has been to ensure consistent quality of our code, regardless of the project. If you want to **make your life easier** and not always have surprises when you try to commit, **make sure that your IDE is properly configured to handle those linters** to highlight (and even fix) warnings and errors when editing a file. It's just a friendly advice.

Some **ressources**:
- [Wes Bos VSCode recipe](https://github.com/wesbos/eslint-config-wesbos#with-vs-code)
- [ESLint for VSCode](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Stylelint for VSCode](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint)

And just in case, ask your colleagues, they surely have great tips for you 😉

## Contribute

There is not a lot to do to maintain this module. Those are the things to keep in mind while changing stuff:
- In the `./package.json`, `peerDependencies` **must always be the same** as the `devDependencies`
- You muse be logged as `antistatique-dev` to **publish a new version** on NPM
