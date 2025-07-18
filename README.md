[![npm version](https://img.shields.io/npm/v/eslint.svg)](https://www.npmjs.com/package/eslint)
[![Downloads](https://img.shields.io/npm/dm/eslint.svg)](https://www.npmjs.com/package/eslint)
[![Build Status](https://github.com/eslint/eslint/workflows/CI/badge.svg)](https://github.com/eslint/eslint/actions)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Feslint%2Feslint.svg?type=shield)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Feslint%2Feslint?ref=badge_shield)
<br />
[![Open Collective Backers](https://img.shields.io/opencollective/backers/eslint)](https://opencollective.com/eslint)
[![Open Collective Sponsors](https://img.shields.io/opencollective/sponsors/eslint)](https://opencollective.com/eslint)
[![Follow us on Twitter](https://img.shields.io/twitter/follow/geteslint?label=Follow&style=social)](https://twitter.com/intent/user?screen_name=geteslint)

# ESLint

[Website](https://eslint.org) |
[Configure ESLint](https://eslint.org/docs/latest/use/configure) |
[Rules](https://eslint.org/docs/rules/) |
[Contribute to ESLint](https://eslint.org/docs/latest/contribute) |
[Report Bugs](https://eslint.org/docs/latest/contribute/report-bugs) |
[Code of Conduct](https://eslint.org/conduct) |
[Twitter](https://twitter.com/geteslint) |
[Discord](https://eslint.org/chat) |
[Mastodon](https://fosstodon.org/@eslint)

ESLint is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code. In many ways, it is similar to JSLint and JSHint with a few exceptions:

* ESLint uses [Espree](https://github.com/eslint/espree) for JavaScript parsing.
* ESLint uses an AST to evaluate patterns in code.
* ESLint is completely pluggable, every single rule is a plugin and you can add more at runtime.

## Table of Contents

1. [Installation and Usage](#installation-and-usage)
2. [Configuration](#configuration)
3. [Code of Conduct](#code-of-conduct)
4. [Filing Issues](#filing-issues)
5. [Frequently Asked Questions](#frequently-asked-questions)
6. [Releases](#releases)
7. [Security Policy](#security-policy)
8. [Semantic Versioning Policy](#semantic-versioning-policy)
9. [Stylistic Rule Updates](#stylistic-rule-updates)
10. [License](#license)
11. [Team](#team)
12. [Sponsors](#sponsors)
13. [Technology Sponsors](#technology-sponsors)

## Installation and Usage

Prerequisites: [Node.js](https://nodejs.org/) (`^18.18.0`, `^20.9.0`, or `>=21.1.0`) built with SSL support. (If you are using an official Node.js distribution, SSL is always built in.)

You can install and configure ESLint using this command:

```shell
npm init @eslint/config
```

After that, you can run ESLint on any file or directory like this:

```shell
./node_modules/.bin/eslint yourfile.js
```

## Configuration

After running `npm init @eslint/config`, you'll have an `.eslintrc` file in your directory. In it, you'll see some rules configured like this:

```json
{
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "double"]
    }
}
```

The names `"semi"` and `"quotes"` are the names of [rules](https://eslint.org/docs/rules) in ESLint. The first value is the error level of the rule and can be one of these values:

* `"off"` or `0` - turn the rule off
* `"warn"` or `1` - turn the rule on as a warning (doesn't affect exit code)
* `"error"` or `2` - turn the rule on as an error (exit code will be 1)

The three error levels allow you fine-grained control over how ESLint applies rules (for more configuration options and details, see the [configuration docs](https://eslint.org/docs/latest/use/configure)).

## Code of Conduct

ESLint adheres to the [JS Foundation Code of Conduct](https://eslint.org/conduct).

## Filing Issues

Before filing an issue, please be sure to read the guidelines for what you're reporting:

* [Bug Report](https://eslint.org/docs/latest/contribute/report-bugs)
* [Propose a New Rule](https://eslint.org/docs/latest/contribute/propose-new-rule)
* [Proposing a Rule Change](https://eslint.org/docs/latest/contribute/propose-rule-change)
* [Request a Change](https://eslint.org/docs/latest/contribute/request-change)

## Frequently Asked Questions

### I'm using JSCS, should I migrate to ESLint?

Yes. [JSCS has reached end of life](https://eslint.org/blog/2016/07/jscs-end-of-life) and is no longer supported.

We have prepared a [migration guide](https://eslint.org/docs/latest/use/migrating-from-jscs) to help you convert your JSCS settings to an ESLint configuration.

We are now at or near 100% compatibility with JSCS. If you try ESLint and believe we are not yet compatible with a JSCS rule/configuration, please create an issue (mentioning that it is a JSCS compatibility issue) and we will evaluate it as per our normal process.

### Does Prettier replace ESLint?

No, ESLint and Prettier have different jobs: ESLint is a linter (looking for problematic patterns) and Prettier is a code formatter. Using both tools is common, refer to [Prettier's documentation](https://prettier.io/docs/en/install#eslint-and-other-linters) to learn how to configure them to work well with each other.

### Why can't ESLint find my plugins?

* Make sure your plugins (and ESLint) are both in your project's `package.json` as devDependencies (or dependencies, if your project uses ESLint at runtime).
* Make sure you have run `npm install` and all your dependencies are installed.
* Make sure your plugins' peerDependencies have been installed as well. You can use `npm view eslint-plugin-myplugin peerDependencies` to see what peer dependencies `eslint-plugin-myplugin` has.

### Does ESLint support JSX?

Yes, ESLint natively supports parsing JSX syntax (this must be enabled in [configuration](https://eslint.org/docs/latest/use/configure)). Please note that supporting JSX syntax *is not* the same as supporting React. React applies specific semantics to JSX syntax that ESLint doesn't recognize. We recommend using [eslint-plugin-react](https://www.npmjs.com/package/eslint-plugin-react) if you are using React and want React semantics.

### What ECMAScript versions does ESLint support?

ESLint has full support for ECMAScript 3, 5, and every year from 2015 up until the most recent stage 4 specification (the default). You can set your desired ECMAScript syntax and other settings (like global variables) through [configuration](https://eslint.org/docs/latest/use/configure).

### What about experimental features?

ESLint's parser only officially supports the latest final ECMAScript standard. We will make changes to core rules in order to avoid crashes on stage 3 ECMAScript syntax proposals (as long as they are implemented using the correct experimental ESTree syntax). We may make changes to core rules to better work with language extensions (such as JSX, Flow, and TypeScript) on a case-by-case basis.

In other cases (including if rules need to warn on more or fewer cases due to new syntax, rather than just not crashing), we recommend you use other parsers and/or rule plugins. If you are using Babel, you can use [@babel/eslint-parser](https://www.npmjs.com/package/@babel/eslint-parser) and [@babel/eslint-plugin](https://www.npmjs.com/package/@babel/eslint-plugin) to use any option available in Babel.

Once a language feature has been adopted into the ECMAScript standard (stage 4 according to the [TC39 process](https://tc39.github.io/process-document/)), we will accept issues and pull requests related to the new feature, subject to our [contributing guidelines](https://eslint.org/docs/latest/contribute). Until then, please use the appropriate parser and plugin(s) for your experimental feature.

### Which Node.js versions does ESLint support?

ESLint updates the supported Node.js versions with each major release of ESLint. At that time, ESLint's supported Node.js versions are updated to be:

1. The most recent maintenance release of Node.js
1. The lowest minor version of the Node.js LTS release that includes the features the ESLint team wants to use.
1. The Node.js Current release

ESLint is also expected to work with Node.js versions released after the Node.js Current release.

Refer to the [Quick Start Guide](https://eslint.org/docs/latest/use/getting-started#prerequisites) for the officially supported Node.js versions for a given ESLint release.

### Where to ask for help?

Open a [discussion](https://github.com/eslint/eslint/discussions) or stop by our [Discord server](https://eslint.org/chat).

### Why doesn't ESLint lock dependency versions?

Lock files like `package-lock.json` are helpful for deployed applications. They ensure that dependencies are consistent between environments and across deployments.

Packages like `eslint` that get published to the npm registry do not include lock files. `npm install eslint` as a user will respect version constraints in ESLint's `package.json`. ESLint and its dependencies will be included in the user's lock file if one exists, but ESLint's own lock file would not be used.

We intentionally don't lock dependency versions so that we have the latest compatible dependency versions in development and CI that our users get when installing ESLint in a project.

The Twilio blog has a [deeper dive](https://www.twilio.com/blog/lockfiles-nodejs) to learn more.

## Releases

We have scheduled releases every two weeks on Friday or Saturday. You can follow a [release issue](https://github.com/eslint/eslint/issues?q=is%3Aopen+is%3Aissue+label%3Arelease) for updates about the scheduling of any particular release.

## Security Policy

ESLint takes security seriously. We work hard to ensure that ESLint is safe for everyone and that security issues are addressed quickly and responsibly. Read the full [security policy](https://github.com/eslint/.github/blob/master/SECURITY.md).

## Semantic Versioning Policy

ESLint follows [semantic versioning](https://semver.org). However, due to the nature of ESLint as a code quality tool, it's not always clear when a minor or major version bump occurs. To help clarify this for everyone, we've defined the following semantic versioning policy for ESLint:

* Patch release (intended to not break your lint build)
    * A bug fix in a rule that results in ESLint reporting fewer linting errors.
    * A bug fix to the CLI or core (including formatters).
    * Improvements to documentation.
    * Non-user-facing changes such as refactoring code, adding, deleting, or modifying tests, and increasing test coverage.
    * Re-releasing after a failed release (i.e., publishing a release that doesn't work for anyone).
* Minor release (might break your lint build)
    * A bug fix in a rule that results in ESLint reporting more linting errors.
    * A new rule is created.
    * A new option to an existing rule that does not result in ESLint reporting more linting errors by default.
    * A new addition to an existing rule to support a newly-added language feature (within the last 12 months) that will result in ESLint reporting more linting errors by default.
    * An existing rule is deprecated.
    * A new CLI capability is created.
    * New capabilities to the public API are added (new classes, new methods, new arguments to existing methods, etc.).
    * A new formatter is created.
    * `eslint:recommended` is updated and will result in strictly fewer linting errors (e.g., rule removals).
* Major release (likely to break your lint build)
    * `eslint:recommended` is updated and may result in new linting errors (e.g., rule additions, most rule option updates).
    * A new option to an existing rule that results in ESLint reporting more linting errors by default.
    * An existing formatter is removed.
    * Part of the public API is removed or changed in an incompatible way. The public API includes:
        * Rule schemas
        * Configuration schema
        * Command-line options
        * Node.js API
        * Rule, formatter, parser, plugin APIs

According to our policy, any minor update may report more linting errors than the previous release (ex: from a bug fix). As such, we recommend using the tilde (`~`) in `package.json` e.g. `"eslint": "~3.1.0"` to guarantee the results of your builds.

## Stylistic Rule Updates

Stylistic rules are frozen according to [our policy](https://eslint.org/blog/2020/05/changes-to-rules-policies) on how we evaluate new rules and rule changes.
This means:

* **Bug fixes**: We will still fix bugs in stylistic rules.
* **New ECMAScript features**: We will also make sure stylistic rules are compatible with new ECMAScript features.
* **New options**: We will **not** add any new options to stylistic rules unless an option is the only way to fix a bug or support a newly-added ECMAScript feature.

## License

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Feslint%2Feslint.svg?type=large)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Feslint%2Feslint?ref=badge_large)

## Team

These folks keep the project moving and are resources for help.

<!-- NOTE: This section is autogenerated. Do not manually edit.-->

<!--teamstart-->

### Technical Steering Committee (TSC)

The people who manage releases, review feature requests, and meet regularly to ensure ESLint is properly maintained.

<table><tbody><tr><td align="center" valign="top" width="11%">
<a href="https://github.com/nzakas">
<img src="https://github.com/nzakas.png?s=75" width="75" height="75" alt="Nicholas C. Zakas's Avatar"><br />
Nicholas C. Zakas
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/fasttime">
<img src="https://github.com/fasttime.png?s=75" width="75" height="75" alt="Francesco Trotta's Avatar"><br />
Francesco Trotta
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/mdjermanovic">
<img src="https://github.com/mdjermanovic.png?s=75" width="75" height="75" alt="Milos Djermanovic's Avatar"><br />
Milos Djermanovic
</a>
</td></tr></tbody></table>

### Reviewers

The people who review and implement new features.

<table><tbody><tr><td align="center" valign="top" width="11%">
<a href="https://github.com/aladdin-add">
<img src="https://github.com/aladdin-add.png?s=75" width="75" height="75" alt="唯然's Avatar"><br />
唯然
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/snitin315">
<img src="https://github.com/snitin315.png?s=75" width="75" height="75" alt="Nitin Kumar's Avatar"><br />
Nitin Kumar
</a>
</td></tr></tbody></table>

### Committers

The people who review and fix bugs and help triage issues.

<table><tbody><tr><td align="center" valign="top" width="11%">
<a href="https://github.com/JoshuaKGoldberg">
<img src="https://github.com/JoshuaKGoldberg.png?s=75" width="75" height="75" alt="Josh Goldberg ✨'s Avatar"><br />
Josh Goldberg ✨
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/Tanujkanti4441">
<img src="https://github.com/Tanujkanti4441.png?s=75" width="75" height="75" alt="Tanuj Kanti's Avatar"><br />
Tanuj Kanti
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/lumirlumir">
<img src="https://github.com/lumirlumir.png?s=75" width="75" height="75" alt="루밀LuMir's Avatar"><br />
루밀LuMir
</a>
</td></tr></tbody></table>

### Website Team

Team members who focus specifically on eslint.org

<table><tbody><tr><td align="center" valign="top" width="11%">
<a href="https://github.com/amareshsm">
<img src="https://github.com/amareshsm.png?s=75" width="75" height="75" alt="Amaresh  S M's Avatar"><br />
Amaresh  S M
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/harish-sethuraman">
<img src="https://github.com/harish-sethuraman.png?s=75" width="75" height="75" alt="Harish's Avatar"><br />
Harish
</a>
</td><td align="center" valign="top" width="11%">
<a href="https://github.com/kecrily">
<img src="https://github.com/kecrily.png?s=75" width="75" height="75" alt="Percy Ma's Avatar"><br />
Percy Ma
</a>
</td></tr></tbody></table>

<!--teamend-->

## Sponsors

The following companies, organizations, and individuals support ESLint's ongoing maintenance and development. [Become a Sponsor](https://opencollective.com/eslint) to get your logo on our README and website.

<!-- NOTE: This section is autogenerated. Do not manually edit.-->
<!--sponsorsstart-->
<h3>Platinum Sponsors</h3>
<p><a href="https://automattic.com"><img src="https://images.opencollective.com/automattic/d0ef3e1/logo.png" alt="Automattic" height="undefined"></a> <a href="https://www.airbnb.com/"><img src="https://images.opencollective.com/airbnb/d327d66/logo.png" alt="Airbnb" height="undefined"></a></p><h3>Gold Sponsors</h3>
<p><a href="https://qlty.sh/"><img src="https://images.opencollective.com/qltysh/33d157d/logo.png" alt="Qlty Software" height="96"></a> <a href="https://trunk.io/"><img src="https://images.opencollective.com/trunkio/fb92d60/avatar.png" alt="trunk.io" height="96"></a> <a href="https://shopify.engineering/"><img src="https://avatars.githubusercontent.com/u/8085" alt="Shopify" height="96"></a></p><h3>Silver Sponsors</h3>
<p><a href="https://vite.dev/"><img src="https://images.opencollective.com/vite/e6d15e1/logo.png" alt="Vite" height="64"></a> <a href="https://liftoff.io/"><img src="https://images.opencollective.com/liftoff/5c4fa84/logo.png" alt="Liftoff" height="64"></a> <a href="https://americanexpress.io"><img src="https://avatars.githubusercontent.com/u/3853301" alt="American Express" height="64"></a> <a href="https://stackblitz.com"><img src="https://avatars.githubusercontent.com/u/28635252" alt="StackBlitz" height="64"></a></p><h3>Bronze Sponsors</h3>
<p><a href="https://cybozu.co.jp/"><img src="https://images.opencollective.com/cybozu/933e46d/logo.png" alt="Cybozu" height="32"></a> <a href="https://sentry.io"><img src="https://github.com/getsentry.png" alt="Sentry" height="32"></a> <a href="https://www.crosswordsolver.org/anagram-solver/"><img src="https://images.opencollective.com/anagram-solver/2666271/logo.png" alt="Anagram Solver" height="32"></a> <a href="https://icons8.com/"><img src="https://images.opencollective.com/icons8/7fa1641/logo.png" alt="Icons8" height="32"></a> <a href="https://discord.com"><img src="https://images.opencollective.com/discordapp/f9645d9/logo.png" alt="Discord" height="32"></a> <a href="https://www.gitbook.com"><img src="https://avatars.githubusercontent.com/u/7111340" alt="GitBook" height="32"></a> <a href="https://nx.dev"><img src="https://avatars.githubusercontent.com/u/23692104" alt="Nx" height="32"></a> <a href="https://opensource.mercedes-benz.com/"><img src="https://avatars.githubusercontent.com/u/34240465" alt="Mercedes-Benz Group" height="32"></a> <a href="https://herocoders.com"><img src="https://avatars.githubusercontent.com/u/37549774" alt="HeroCoders" height="32"></a> <a href="https://www.lambdatest.com"><img src="https://avatars.githubusercontent.com/u/171592363" alt="LambdaTest" height="32"></a></p>
<!--sponsorsend-->

## Technology Sponsors

* Site search ([eslint.org](https://eslint.org)) is sponsored by [Algolia](https://www.algolia.com)
* Hosting for ([eslint.org](https://eslint.org)) is sponsored by [Netlify](https://www.netlify.com)
* Password management is sponsored by [1Password](https://www.1password.com)
