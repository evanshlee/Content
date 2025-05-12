---
tags: [dependabot, incremental, comprehensive]
---

# Two Development Approaches I Contemplated While Setting Up Dependabot

After only observing Dependabot already set up in open source projects, I had to implement dependabot[^1] from scratch in an open source project I was directly participating in. With the mindset of "Let's finish it perfectly in one go!", I submitted an extensive PR, but through that process, I clearly recognized two contrasting development approaches. This post is a reflection to document that insight.

## Countless Options, Wouldn't It Be Better to Consider Everything from the Start?

The [dependabot setup PR](https://github.com/DaleStudy/daleui/commit/dedb235c2cb9128ab3ca0b4633bb4c0215295c29) I initially submitted was excessively comprehensive.

### Key dependabot.yml Configuration Summary

- **Update Targets**

  - npm packages (root directory)
  - GitHub Actions workflows (`/.github/workflows`)

- **Update Frequency**

  - npm: weekly
  - GitHub Actions: monthly

- **Common Settings**

  - Automatic PR label: `dependencies`
  - Maximum open PRs at once: 10
  - Auto-assigned reviewers: `DaleStudy/daleui`

- **Package Group Settings**

  - `storybook`: `@storybook*`, `chromatic`, etc.
  - `react`: `react`, `react-dom`, `@types/react*`
  - `testing`: `@testing-library*`, `vitest`, `happy-dom`
  - `eslint`: `eslint*`, `@eslint*`, `typescript-eslint`
  - `typescript`: `typescript`, `@types/*`
  - `vite`: `vite`, `@vitejs/*`, `vite-plugin-*`
  - `ui-components`: `@radix-ui/*`, `lucide-react`
  - `css`: `@pandacss/*`
  - All allowing only `minor` and `patch` updates

- **Additional GitHub Actions Labels**
  - `github-actions`

I considered various aspects. I used an LLM to generate a Dependabot draft considering the current project dependencies. After reviewing the configuration, I thought it was sufficient and created a PR with the changes.

However, a [single comment](https://github.com/DaleStudy/daleui/pull/88#discussion_r2011058936) from the maintainer turned everything around.

> "Shouldn't we use the default values and configure them later when needed? Convention over configuration! 😉"

After receiving this feedback, I [changed](https://github.com/DaleStudy/daleui/compare/dedb235c2cb9128ab3ca0b4633bb4c0215295c29..a7cc22b47481d63bbacce1ec59a3030d398843f5) the configuration file as follows:

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"

  - package-ecosystem: "github-actions"
    directory: "/.github/workflows"
    schedule:
      interval: "daily"
```

And in reality, we [continuously modified](https://github.com/DaleStudy/daleui/commits/main/.github/dependabot.yml) the dependabot configuration file. Observing these changes, I thought about the following topic.

## Starting with Minimal Configuration and Expanding Incrementally vs. Designing Well from the Beginning

### Starting with Minimal Configuration and Expanding Incrementally

- **Advantages**

  - Smaller PR size makes review and merging faster.
  - Adding only options that are actually used results in fewer 'dead settings'.

- **Disadvantages**

  - During configuration gaps, unexpected inconveniences or risks may arise.
  - Frequent customization PRs can increase the total amount of communication.

### Designing Well from the Beginning

- **Advantages**

  - Even with one-time deployment, major structural changes are rare.
  - In the medium to long term, review/meeting costs can be reduced.

- **Disadvantages**

  - Initial agreement and review time is extended, slowing the 'starting speed'.
  - Over-designed options risk becoming legacy.

## In the End, Which Choice is Right?

**There is no definitive answer.** The balance between the two strategies varies depending on the situation and team maturity.

- **Starting with minimal configuration and expanding incrementally** provides flexibility in _early stages with high uncertainty_.
- **Designing well from the beginning** reduces maintenance costs in _mature stages where stability is important_.

Ultimately, I think it's important to make "the minimum decision that fits our team now" and periodically revalidate the strategy based on **actual data** (PR notification frequency, merge delay times, etc.).

[^1]: Dependabot is a GitHub-integrated bot that automatically scans your repository's dependency files (e.g., package.json, pom.xml, Gemfile) and raises pull requests (PRs) to keep those dependencies up to date and patch known vulnerabilities.
