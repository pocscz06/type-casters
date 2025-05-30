# Contributing to Type Casters

As this will be a personal project involving just the two of us in its conception, development, testing, debugging, and deployment, this file will serve as our guidelines for development workflow and standards.

We *should* see the repository as a source/version control history log. That being said, it should be easy for anyone, especially us months later, to look through the repository and be able to understand its history. The standards outlined below should aid in facilitating that.

## Table of Contents

- [Development Workflow](#development-workflow)
  - [Creating Branches](#when-to-create-a-branch)
  - [Branch Lifecycle](#branch-lifecycle)
    - [Branch Types](#branch-types)
  - [Commit Messages](#commit-messages)
    - [Commit Types](#commit-types)
    - [When to Commit](#when-to-commit)
    - [Commit Message Rules](#commit-message-rules)
  - [PR Process](#pull-request-process)
    - [Before Opening a PR](#before-opening-a-pr)
    - [PR Title Formatting](#pr-title-format)
    - [PR Description Template](#pr-description-template)
    - [Before Merging a PR](#before-merging-a-pr)
  - [Issue Reporting](#issue-reporting)
    - [Bug Reporting](#bug-reporting)
  - [Code Standards](#code-standards)
    - [Best Practices](#best-practices)
    - [File Organization](#file-organization)
    - [Testing](#testing)
- [Resources Referenced](#resources-referenced)

## Development Workflow

### When to Create a Branch

Create new branches for:

- Features
- Bug fixes
- Refactoring

> [!WARNING]
> Avoid committing directly to main.

### Branch Lifecycle

1. Create branch from `develop`
   - `develop` is the integration branch. It will be where all features get integrated and tested together. Thus, when features are complete, they are merged back into `develop` when their PRs are resolved. Periodically, `develop` will subsequently be merged into `main` for releases.
      - This allows us to ensure `main` stays stable, while `develop` contains the latest development. We are then able to deal with any integration issues before they reach production in `main`.
2. When creating your branch, make sure to give it a pertinent *type*. See [Branch Types](#branch-types).  The branch-naming format should be as follows:
   - `type/branch-name`
   - Here are some examples:
      - `feature/auth`
      - `bugfix/login-error`
3. Make changes and commit following our standards outlined in [Commit Messages](#commit-messages).
4. Open pull request to `develop`. See [PR Process](#pull-request-process) to see our PR standards.
5. Address review feedback. 
   - When you create a PR request, the other person should be the one to merge it after review. If you are that *other person*, and you have questions/concerns/etc., comment about it in the PR, and once everything is resolved, the PR can be merged.
6. Branch is merged.

#### Branch Types

- `feature/`
- `bugfix/`
- `docs/`
- `refactor/`
- `test/`

> [!NOTE]
> Avoid 'nesting' branches beyond the develop branch. If you don't, your nested branch will be based on its parent branch, which at that point, may be stale (not up-to-date). Create children branches from develop or main.

### Commit Messages

We will follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) specification.

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

#### Commit Types

- `fix` - Bug fix
- `feat` - Features
- `chore` - Maintenance tasks (i.e., modifying .gitignore, package installation, configurations, etc.)
- `docs` - Documentation changes
- `refactor` - Code refactoring
- `perf` - Performance improvements
- `test` - Testing

#### WHEN to Commit

We want a clean, linear commit history. We want to break down commits by logical units rather than **entire** features. That's what branches are for—not commits. There have been many different arguments on *what* this looks like, and *how* it should be done. With that said, we won't have any strict defined format/template for how it should be done. 

Just put *some* thought into what you should be committing and *when*. There are so many benefits to this that outweigh not doing it. To not commit to thoughtful commits is to just be lazy. Read [Kenny Ballou's blog post](https://kennyballou.com/blog/2021/03/commit-granularity/index.html) to see more.

Consider the development of a single page—the HTML, CSS, JavaScript, etc. Here's an example of how I'd *ideally* approach this:

1. Build HTML structure &rarr; commit
2. Add CSS, layer by layer, or just all of the CSS itself

   a. Reset Layer &rarr; commit

   b. Initialization Layer &rarr; commit
   
   c. Layout/Styling &rarr; commit
3. Add JavaScript script(s) &rarr; commit
4. Bug fixes/refinements/refactoring &rarr; separate commits for each

That doesn't have to be, or perhaps shouldn't be strictly followed—as you don't want this to end up impeding your progress—but the key is that each commit should represent one logical unit that can be described in a single sentence. So long as they follow the same logic, if there are multiple changes within a commit, that's *okay*.

```example
feat(auth): add Firebase Authentication

- Add Firebase Auth setup
- Create login and signup components
- Add user state management

Closes #123
```

#### Commit Message Rules

- Use present tense ("add feature" not "added feature")
  - Think of a GitHub Repo as a log of the software's changes. Each individual commit represents a change and what it *will do* when applied.
- Limit first line to 50 chars (standard)
- Reference issues and PRs when applicable
  - This is mainly for bug fixes. We will be logging bugs/issues with [GitHub Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues).
  - Referencing issues in a commit that addresses that issue helps with traceability. It makes our repo "self-documenting." It allows us to refer back to the issue's "origin" to understand its context, the discussion around it, etc.
  - Referencing PRs is less common, but is done in commits that merge PRs, for example. Though GitHub handles that automatically. You may reference PRs to link to contextual dicussion, other files changed pertinent to your current commit, etc.

### Pull Request Process

#### Before Opening a PR

- **Ensure your branch is up-to-date with the `develop` branch.** We don't want to be dealing with merge conflicts stemming from attempting to merge a branch that has been worked on for weeks when the `develop` branch has been updated dozens of times since then.
- **Ensure your branch passes ALL tests (we will automate them with GitHub Actions).** Why merge breaking changes?
- **Run ESLint and fix any issues.** This is to help ensure our code follows a certain standard/format.

#### PR Title Format

Use the same format as commit messages.

```
<type>[optional scope]: <description>
```

#### PR Description Template

Follow this template for all applicable PRs. There will probably be merges that will not necessitate this level of detail (i.e., `docs`).

```markdown
## Description

Brief description of changes made

## Type of Change

- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update

## Related Issues

Closes #issueNumber
Related to #issueNumber or #prNumber

## Testing

Describe the tests you ran and provide instructions for reproduction (if applicable).

## Notes

Anything you want to address? Is this PR's logic dependent on another feature? Is there still more to add for *complete* functionality?
```

#### Before Merging a PR

- Any discussion within the PR should be resolved
- The other person should have conducted a code review
- Preferably, the other person should be the one merging the PR
- Squash and merge whenever possible. This keeps our main branch clean and traceable

Keep in mind that while squashing and merging is definitely preferable for keeping the main branch clean, it shows as one singular commit to main. The branch you are merging from will still show each individual commit, unsquashed. This means GitHub will recognize that branch as being ahead of main by `x` amount of commits, and behind by `y` squashed commit(s). 

We have a few options to remedy this:

- Ignore it, and keep the branch for future work. 
  - This is ugly, but it "works".
  - There is still a fairly big issue with this, though. Eventually, that branch will be working on an "outdated" version of the project. Future PRs could then result in merge conflicts.
- Delete branches after they have been merged.
  - This is preferable. In fact, we can even configure this to occur automatically on GitHub. If you had more work you intended to do on that branch, that's fine. Once the PR has been merged, you can just create a new branch, perhaps even with the same name, and it'll be up-to-date with the new change(s) you just added. 

### Issue Reporting

#### Bug Reporting

We will be using GitHub Issues for bug reports. When you create a new issue, **make sure to specify its label as `bug`**. We will be using GitHub issues almost solely for bug reports. Follow this template when issuing a bug report:

```template
**Bug Description**

A clear description of the bug.

**Steps to Reproduce**

A numbered list of steps to reproduce the bug.

**Expected Behavior**

What you expected to happen (that didn't end up happening).

**Screenshots**

Add screenshots to explain your problem if applicable.

**Environment**

Add details on your development environment to give context to your issues.

- OS: Windows 11
- Browser: Chrome 136.0.7103.116 (Official Build) (64-bit)
- IDE Version: VSC 1.100.2

**Notes**

Add any other contextual information.
```

You can attempt to resolve the bug yourself, just be sure to issue it on the repository for logging purposes.

### Code Standards

> [!NOTE]
> This section may be updated as needed.

Most of our code formatting/syntax will be enforced by our ESLint configuration. Many find ESLint bothersome to work with, as it may feel rather "strict" in its enforcement of code standards. But there are great benefits to enforcing a code standard—many people have opinionated ways of writing code. This can make a codebase difficult to read, and thus difficult to maintain and update when needed.

Although this project is a personal project, and subsequently, practice, the issue of maintenance actually applies to us to a degree. We will be working almost *solely* on the frontend initially, and return later to add backend logic and a database.

> [!NOTE]
> To see our actual code standard rules, check our ESLint configuration.

#### Best Practices

- Write self-documenting code.
  - Adhere to the principle of single function, single purpose as much as you are able. This makes it very obvious what a function does and allows for possible reusability if needed. In some cases, this may be an unreasonable expectation. Don't sweat it, just do your best.
- Add comments for more complex logic.
  - If your code is self-documenting—adherent to the first rule, this shouldn't be needed. In some cases, however, it *will* be needed. In which case, write comments following [JSDoc](https://jsdoc.app/) standards.
- Avoid global variables as much as you are able.
  - Global variables can cause unnecessary bloat. These variables will be present within the entire runtime of our application, even when they are not needed. Modern garbage collectors are efficient at managing memory, but following this rule is still good for readability, and subsequently, maintainability.
  - Global variables may still be necessary in some instances. 
    - Application-wide configuration (environment vars)
    - Logging utilities
    - Persistent cache
- Follow the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle as much as you are able.
  - The DRY principle states "don't repeat yourself." Reuse code whenever you can. 
  - This is a fairly heavily debated principle today. Again, only adhere when able, don't sweat it.

#### File Organization

This section will be updated with a defined file structure after we've bootstrapped the Svelte framework with Vite for our project.

We will generally be following the Svelte convention for file organization (possibly with some minor changes of our own). It's important to ensure everything is in its "right" place, so we don't have to do any guesswork and sift through the codebase to locate different files.

#### Testing

We are using [Jest](https://jestjs.io/) for testing. We recognize the importance of testing, but we are unfamiliar with the practice at the moment. I believe, in a professional setting, a company may outline a minimum percentage of code testing coverage (they should, if not). We will not be enforcing a minimum percentage, but just create tests as much as we are able, for wherever we think they may be needed, even if slightly. 

Once we have tests, we can automate them with GitHub Actions to run with every commit to ensure no new additions have broken any previous code.

## Resources Referenced

- [Conventional Commits Specification](https://www.conventionalcommits.org/en/v1.0.0/#summary)
- [Kenny Ballou's blog post](https://kennyballou.com/blog/2021/03/commit-granularity/index.html) 
- [GitHub Issues Docs](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)
- [JSDoc](https://jsdoc.app/) 
- [DRY Wiki Article](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [Jest Docs](https://jestjs.io/)