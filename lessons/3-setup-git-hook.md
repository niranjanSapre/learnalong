# Set up git hooks with [Husky](https://typicode.github.io/husky/) to force commit lint's format

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
