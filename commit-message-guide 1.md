# Commit Message Guidelines

Tài liệu này được viết để hướng đẫn cách viết commit message trong dự án. Nó được mở rông dựa trên [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) cung cấp một bộ quy tắc để dàng tạo commit hitory rõ ràng bằng cách mô tả feature, fixes và breaking changes được thự hiện trong commit

- [Goals](#goals)
- [Format of the commit message](#format-of-the-commit-message)
  - [`<type>`](#type)
  - [`[optional scope]`](#scope-optional)
  - [`<description>`](#description)
  - [`[optional meta]`](#optional-meta)
  - [`[optional body]`](#optional-body)
  - [`[optional footer`](#optional-footer)
    - [Breaking changes](#breaking-changes)
    - [Referencing issues](#referencing-issues)
  * [Examples](#examples)
  * [Revert](#revert)
- [Generating CHANGELOG.md](#generating-changelogmd)

## Goals

- allow generating CHANGELOG.md by script
- allow ignoring commits by git bisect (not important commits like formatting)
- provide better information when browsing the history

## Format of the commit message

The commit message should be structured as follows:

```
<type>[optional scope]: <description> [optional meta]

[optional body]

[optional footer(s)]
```

The first line of a commit message should not be longer than 72 characters, and all the other lines should have a maximum of 100 characters!
This allows the message to be easier to read on Github as well as in various git tools.

> Subject line may be prefixed for continuous integration purposes.
> For example, [JIRA](https://bigbrassband.com/git-for-jira.html)
> requires ticket in the beggining of commit message message:
> "[LHJ-16] fix(compile): add unit tests for windows"

The usage of markup that can be read as plain text (e.g. markdown, reST, etc),
specially in body and footer is optional, but useful when auto generating
changelogs.

#### `<type>`

The `<type>` of a commit message should be a single word or abbreviation drawn
from an ontology, according to the nature of the project.
This document specifies a **programming ontology**, with the following elements:

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing tests
- **build**: Changes to the build/compilation/packaging process or auxiliary tools such as documentation generation
- **ci**: Changes in the continuous integration/delivery setup
- **deps**: Update or remove library/package dependencies

An example of ontology for a book writing project is: **typo**,
**restructure**, **write**, **move**, etc…

#### `[optional scope]`

Usually it is convenient to mention exactly which part of the code base changed.
The `<scope>` token is responsible for providing that information.
For example, imagine that a webserver introduces OAuth login via Facebook, a
valid commit message would be:

```
feat(auth): introduce sign in via Facebook
```

Please notice that here `auth` might refer to a conceptual architectural component
or even the basename of an file in the repository. While the granularity of the
scope can vary, it is important for it to be a part of the "common language"
spoken in the project.

Please notice that in some cases the scope is naturally _too broad_, and
therefore not worthy to mention. Examples of this special case:

```
docs: replace old website URL
refactor: move folder structure to `src` directory layout
```

#### `<description>`

Subject line should contains succinct description of the change.

- use imperative, present tense: “change” not “changed” nor “changes”
- don't capitalize first letter
- no dot (.) at the end

#### `[optional meta]`

Additionally, the end of subject-line may contain _hashtags_ to facilitate changelog generation and bissecting.

- `#wip` - indicate for contributors the feature being implemented is not complete yet. Should not be included in changelogs (just the last commit for a feature goes to the changelog).
- `#irrelevant` - the commit does not add useful information. Used when fixing typos, etc... Should not be included in changelogs.

#### `[optional body]`

- just as in `<subject>` use imperative, present tense: “change” not “changed” nor “changes”
- includes motivation for the change and contrasts with previous behavior

* http://365git.tumblr.com/post/3308646748/writing-git-commit-messages
* http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

#### `[optional footer]`

##### Breaking changes

All breaking changes have to be mentioned in footer with the description of the change, justification and migration notes

```
BREAKING CHANGE: isolate scope bindings definition has changed and
the inject option for the directive controller injection was removed.

To migrate the code follow the example below:

Before:

   scope: {
     myAttr: 'attribute',
     myBind: 'bind',
     myExpression: 'expression',
     myEval: 'evaluate',
     myAccessor: 'accessor'
   }

After:

   scope: {
     myAttr: '@',
     myBind: '@',
     myExpression: '&',
     // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
     myAccessor: '=' // in directive's template change myAccessor() to myAccessor
   }

The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

##### Referencing issues

Closed bugs should be listed on a separate line in the footer prefixed with "Closes" keyword like this:

```
Closes #234
```

or in case of multiple issues:

```
Closes #123, #245, #992
```

### Revert

If the commit reverts a previous commit, it should begin with revert:, followed by the header of the reverted commit. In the body it should say: This reverts commit <hash>., where the hash is the SHA of the commit being reverted.

### Examples

```
feat($browser): add onUrlChange event (popstate/hashchange/polling)

New $browser event:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```
fix($compile): add unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
```

```
feat(directive): add directives disabled/checked/multiple/readonly/selected

New directives for proper binding these attributes in older browsers (IE).
Added coresponding description, live examples and e2e tests.

Closes #351
```

```
style($location): add couple of missing semi colons
```

```
docs(guide): update fixed docs from Google Docs

Couple of typos fixed:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```

```
feat($compile): simplify isolate scope bindings

Change the isolate scope binding options to:
  - @attr - attribute binding (including interpolation)
  - =model - by-directional model binding
  - &expr - expression execution binding

This change simplifies the terminology as well as
number of choices available to the developer. It
also supports local name aliasing from the parent.

BREAKING CHANGE: isolate scope bindings definition has changed and
the inject option for the directive controller injection was removed.

To migrate the code follow the example below:

Before:

   scope: {
     myAttr: 'attribute',
     myBind: 'bind',
     myExpression: 'expression',
     myEval: 'evaluate',
     myAccessor: 'accessor'
   }

After:

   scope: {
     myAttr: '@',
     myBind: '@',
     myExpression: '&',
     // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
     myAccessor: '=' // in directive's template change myAccessor() to myAccessor
   }

The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

## Generating CHANGELOG.md

Changelogs may contain three sections: new features, bug fixes, breaking changes.
This list could be generated by script when doing a release, along with links to related commits.
Of course you can edit this change log before actual release, but it could generate the skeleton.

List of all subjects (first lines in commit message) since last release:

```bash
git log <last tag> HEAD --pretty=format:%s
```

New features in this release

```bash
git log <last release> HEAD --grep feat
```

---
