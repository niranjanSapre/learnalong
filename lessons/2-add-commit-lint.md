# Add [Commit Lint](https://commitlint.js.org/) to force [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) as a commit message format

Commit messages in a shared project are better if you have a common convention in place.

Image, you like to commit something along the lines of "add dashboard page", while your colleague might write something like "feature dashboard", or any variation of that.

Conventional commits already defines a great set of scopes depending on the type of work being done (feature, fix, docs, etc) and a format that also enables automatically generating version of your application that follows [SemVer]() with the same format of commit messages.

You can also automate creating changelog, and more if everyone follows the same naming conventions for commit messages.

Commit lint enables you to force that convention.

To add commitlint, run the following command with bun :

```bash
bun add -d @commitlint/cli @commitlint/config-conventional
```

Then add the following content in a file named `commitlint.config.js` at the root of your project, on the same level as `package.json`:

```js
export default { extends: ['@commitlint/config-conventional'] };
```

That's it for commit lint, right now, it's pretty useless as we're not enforcing the commit messages to respect it, but that will be done on the next lesson !

You can add everything done up until now and commit it under something like `feat(commit): add commitlint`. Then simply push it to your repo !
