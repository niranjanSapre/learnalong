# Add commit lint and Husky for git hooks

In this lesson, you will learn how to add commit-lint and use husky to force conventional commits format for commits.

## Add [Commit Lint](https://commitlint.js.org/) to force [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) as a commit message format

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

You can add everything done up until now and commit it under something like `feat(commit): add commitlint`. Then simply push it to your repo !

## Set up git hooks with [Husky](https://typicode.github.io/husky/) to force commit lint's format

Husky allows us to add git hooks to enforce tasks we want to run before allowing a contributor to commit or push code.

We will use it to set up a basic pre-commit hook that checks the commit message before allowing anyone to commit their changes.

To do so, first run the following command to add husky with bun:

```bash
bun add -d husky
```

Then run the following bunx command to initialize husky, this will add a prepare script to the package.json that will be run anytime you run a bun install command:

```bash
bunx husky init
```

You should now see a hidden folder named `.husky` containing one `pre-commit` hook that runs `bun test` by default.

We can for now remove that pre-commit hook and replace it with a commit-msg hook.

For that, run the following commands to create and make an executable file named `commit-msg`:

```bash
touch .husky/commit-msg
chmod +x .husky/commit-msg
```

Then add the following contents to the `commit-msg` file, which runs the commitlint cli we installed previously and checks that your commit message follows the conventional commit conventions:

```sh
bunx --no -- commitlint --edit "$1"
```

That's it, you've now forced all commits to match the conventional commits norm.

Add all changed files, try to commit them with the following example `git commit -m "test"` and you should get the following output:

```
⧗   input: test
✖   subject may not be empty [subject-empty]
✖   type may not be empty [type-empty]

✖   found 2 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

husky - commit-msg script failed (code 1)
```

Now try commiting them with a message that matches the convention, something like `git commit -m "feat(commit): add commit-msg hook to force conventional commits"` and you should see it being committed.

Then simply push your changes to your repository !

That's it for this lesson !
