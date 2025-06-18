# Add Biome and lint-staged

Biome is a linter, formatter and is written in Rust for better performances than Prettier or ESLint.
lint-staged allows you to define tasks to run on certain files, such as linters, formatters, etc.
We'll combine the both of them with Husky with a pre-commit hook to automatically trigger a formatting of the code before committing.

## Add [Biome](https://biomejs.dev/) as a formatter and linter for js/ts

To add Biome using bun, run the following command:

```bash
bun add -D -E @biomejs/biome
```

Initialise a `biome.json` config using the following command:

```bash
bunx --bun biome init
```

Then run the following command to check for linting and formatting errors:

```bash
bunx biome check
```

You should see a few files already getting recommendations for formatting.

You can try the same command with `--write` as an argument to automatically format the code:

```bash
bunx biome check --write
```

You can run it again and see that there's no linting or formatting issues now.

## Set up a [lint-staged](https://github.com/lint-staged/lint-staged) and a pre-commit hook to automatically lint and format code before committing

Run the following command to add lint-staged as a dependency:

```bash
bun add -d lint-staged
```

Add the following to your `package.json` at the same level as the `scripts`:

```json
"lint-staged": {
    "*.{js,ts,json}": ["bunx biome check --write"]
}
```

This config tells lint-staged to only run `bunx biome check --write` on files with the extension `js`, `ts` and `json`.

Then test it before staging any files in Git by running:

```bash
bunx lint-staged
```

Which should output something like:

```
→ No staged files found.
```

If you update the `index.ts` file, add in a few tabs like so:

```ts
      console.log("Hello via Bun!");
```

Then stage the file with `git add index.ts`, and run the same command `bunx lint-staged`, you should see something like this now:

```
✔ Backed up original state in git stash (6cf14e8)
✔ Running tasks for staged files...
✔ Applying modifications from tasks...
✔ Cleaning up temporary files...
```

If you check `index.ts` again, you should see the tabs have been removed and the file is still staged in git.

Now all that's left to do is automate this process by adding a `pre-commit` file under `.husky` containing:

```bash
bunx lint-staged
```

Then add modify the formatting of `index.ts`, add everything we did in this lesson with `git add .` and commit it with something like `git commit -m "feat(formatting): added pre-commit hook to run lint-staged using biome as a formatter"`.

You should see something along the lines of these logs from git:

```
[STARTED] Backing up original state...
[COMPLETED] Backed up original state in git stash (e7349a4)
[STARTED] Running tasks for staged files...
[STARTED] package.json — 8 files
[STARTED] *.{js,ts} — 2 files
[STARTED] bunx biome check --write
[COMPLETED] bunx biome check --write
[COMPLETED] *.{js,ts} — 2 files
[COMPLETED] package.json — 8 files
[COMPLETED] Running tasks for staged files...
[STARTED] Applying modifications from tasks...
[COMPLETED] Applying modifications from tasks...
[STARTED] Cleaning up temporary files...
[COMPLETED] Cleaning up temporary files...
[main 7fc11a2] feat(formatting): added pre-commit hook to run lint-staged using biome as a formatter
 8 files changed, 255 insertions(+), 54 deletions(-)
 create mode 100644 .husky/pre-commit
 create mode 100644 lessons/3-biome-lint-staged.md
 rewrite package.json (98%)
 rewrite tsconfig.json (98%)
```

Now all that's left to do is to push it.

Now you know how to use a formatter, force it to run before each commit, and ensures you have a consistent codebase.
I many times see people run formatting and linting as part of a CI/CD, but I feel like doing it this way makes it simpler and gives a better dev experience.
Instead of pushing your code, opening a pr, seeing that the pr is rejected because of formatting and linting issues, your code is simply formatted before each commit and won't allow you to commit if the linting fails.

Also, to make it even better, you can configure your IDE to use said formatter by either installing the extension for that formatter (or configuring it if using something like LazyVim etc).

And that's it for today's lesson !
