
2025-09-26 17:47

Status:

Tags:

---
# Yarn installation
https://yarnpkg.com/getting-started\

- Yarn is a open-source package manager like npm.
- It is used to manage dependencies in a JavaScript projects.

run as system admin

`npm install -g corepack`
`corepack enable`

intialize new project

`yarn init -2`


### Usage


If you're coming from npm, the main changes are:

- Running `yarn` is enough to run an install! It's an alias to `yarn [install](https://yarnpkg.com/cli/install)`.
- Adding or updating a dependency to a single package is done with `yarn [add](https://yarnpkg.com/cli/add)`.
- Upgrading a dependency across the whole project is done with `yarn [up](https://yarnpkg.com/cli/up)`.
- Your scripts are aliased. Calling `yarn build` is the same as `yarn [run](https://yarnpkg.com/cli/run) build`! 
- Most registry-related commands are moved behind `yarn npm` (ex: `yarn [npm audit](https://yarnpkg.com/cli/npm/audit)`).

To see the full list of commands, check the [CLI reference](https://yarnpkg.com/cli).




---
## References