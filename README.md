# 📚 Learn Along !

Welcome to this humble Github repository where I will share some of the best practices, tips, and more about many topics on how to set up a good project.

You'll learn how to:
- Initialise a basic [Bun](https://bun.sh/) project
- Add [Commit Lint](https://commitlint.js.org/) to force [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) as a commit message format
- Set up pre-commit hooks with [Husky]() to force commit lint's format
- Add [Biome](https://biomejs.dev/) as a formatter and linter for js/ts
- Add [Husky](https://typicode.github.io/husky/) to simplify git hooks management
- Set up a [lint-staged](https://github.com/lint-staged/lint-staged) and a pre-commit hook to automatically lint and format code before committing
- Make a basic [bun server](https://bun.sh/docs/api/http) with some tests using bun's testing API
- Add a pre-push hook that automatically runs tests and fails if a test isn't passing
- How to dockerize the bun server
- Add a [Bruno](https://www.usebruno.com/) API collection to test a running server
- Add a CI/CD pipeline that tests for formatting and linting issues
- Add a CI/CD pipeline that tests the code
- Add a CI/CD pipeline that automatically builds a docker image of your application and pushes it to a registry
- Add a CI/CD pipeline that tests the vulnerability of the constructed docker image using [Trivy](https://trivy.dev/latest/), and uploads the results as artefacts
- Add a CI/CD pipeline that tests the vulnerability that checks vulnerabilities of your code, and uploads the results as artefacts
- Add a CI/CD pipeline that runs the Bruno API collection automatically on each push
- How to optimize the docker image size to the maximum

