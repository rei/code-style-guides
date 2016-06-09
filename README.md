# REI Code Style Guides

> Code style guides for programming languages at REI

- [General](/docs/general.md) (Applies to all languages)
- [HTML](/docs/html.md)
- [Less](/docs/less.md)
- [JavaScript](/docs/javascript.md)

## FAQs

### Why? Isn't code formatting up to personal preference?

Consistent code formatting increases readability, and reduces the overhead of understanding each other's code. A coder should be able to pick up any arbitrary file, and understand it quickly. Ideally, our codebase should look as though it were written by a single coder. You are not coding for yourself; you are coding for REI.

### How do I propose a change?

A developer who would like to propose a change to a code style guide must:

1. Create a PR with the proposed changes.
1. Email the team requesting review, including a link to the PR.
1. Present your suggested update at the next team meeting for an open discussion.
    - If needed, modify your PR per team recommendations and notify team of updates.
1. Email the team requesting a vote, open for 1 week.
1. Merge the PR after:
    - A minimum of 2/3 of team indicate approval<sup>1</sup>, at least one of whom must be a senior<sup>2</sup>, and
    - At least 1 week's time has passed from request-vote email<sup>3</sup>.
1. Email the team with the update.

<sup>1</sup>Abstains will not be included in the vote approval calculation.<br>
<sup>2</sup>Due to the team-wide impact<br>
<sup>3</sup>To give everyone a chance to review<br>

### What about code with old formatting?

There's no need to make a specific effort to re-format old code, but if you're modifying a file with outdated formatting, please update what you can while you're in there.

### Editor Configuration

Set up your editor to automatically format code per our style guide:

- **Intellij**
  - Import [settings](./rei_standard_intellij_settings.jar).
  - In Settings, select Editor->Code Style and select "REI IT" scheme from the drop-down menu.
  - To format code, select Code->Reformat Code.

- **Sublime Text**
  - Install [JS Beautify](https://github.com/enginespot/js-beautify-sublime).
  - Update settings using [this config](./.jsbeautifyrc).
  - Code is formatted automatically on save by default. You can turn this off in the .jsbeautifyrc file and format on demand using CNTL-OPTION-F (mac) CNTL-ALT-F (win).